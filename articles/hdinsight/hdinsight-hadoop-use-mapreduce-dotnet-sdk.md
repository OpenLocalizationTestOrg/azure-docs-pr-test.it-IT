---
title: i processi MapReduce aaaSubmit tramite HDInsight .NET SDK - Azure | Documenti Microsoft
description: Informazioni su come i processi di MapReduce toosubmit tooAzure HDInsight Hadoop tramite HDInsight .NET SDK.
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: c85e44b0-85fd-4185-ad1c-c34a9fe5ef44
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: d00e31400b8fa47982c31d00bfdcdb304bcb0b59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="4ffc3-103">Eseguire processi MapReduce con HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="4ffc3-103">Run MapReduce jobs using HDInsight .NET SDK</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="4ffc3-104">Informazioni su come i processi MapReduce toosubmit tramite HDInsight .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="4ffc3-104">Learn how toosubmit MapReduce jobs using HDInsight .NET SDK.</span></span> <span data-ttu-id="4ffc3-105">I cluster HDInsight includono un file JAR con alcuni esempi di MapReduce.</span><span class="sxs-lookup"><span data-stu-id="4ffc3-105">HDInsight clusters come with a jar file with some MapReduce samples.</span></span> <span data-ttu-id="4ffc3-106">file jar Hello è */example/jars/hadoop-mapreduce-examples.jar*.</span><span class="sxs-lookup"><span data-stu-id="4ffc3-106">hello jar file is */example/jars/hadoop-mapreduce-examples.jar*.</span></span>  <span data-ttu-id="4ffc3-107">Uno degli esempi di hello è *wordcount*.</span><span class="sxs-lookup"><span data-stu-id="4ffc3-107">One of hello samples is *wordcount*.</span></span> <span data-ttu-id="4ffc3-108">Si sviluppa un toosubmit dei applicazione dei console c# un processo wordcount.</span><span class="sxs-lookup"><span data-stu-id="4ffc3-108">You develop a C# console application toosubmit a wordcount job.</span></span>  <span data-ttu-id="4ffc3-109">processo Hello legge hello */example/data/gutenberg/davinci.txt* file e gli output hello risultati troppo*/example/data/davinciwordcount*.</span><span class="sxs-lookup"><span data-stu-id="4ffc3-109">hello job reads hello */example/data/gutenberg/davinci.txt* file, and outputs hello results too*/example/data/davinciwordcount*.</span></span>  <span data-ttu-id="4ffc3-110">Se si desidera un'applicazione hello toorerun, è necessario pulire la cartella di output hello.</span><span class="sxs-lookup"><span data-stu-id="4ffc3-110">If you want toorerun hello application, you must clean up hello output folder.</span></span>

> [!NOTE]
> <span data-ttu-id="4ffc3-111">passaggi di Hello in questo articolo devono essere eseguiti da un client di Windows.</span><span class="sxs-lookup"><span data-stu-id="4ffc3-111">hello steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="4ffc3-112">Per informazioni sull'uso di un Linux, OS X o toowork client Unix con Hive, usare il selettore di scheda hello visualizzato nella parte superiore di hello di articolo hello.</span><span class="sxs-lookup"><span data-stu-id="4ffc3-112">For information on using a Linux, OS X, or Unix client toowork with Hive, use hello tab selector shown on hello top of hello article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="4ffc3-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4ffc3-113">Prerequisites</span></span>
<span data-ttu-id="4ffc3-114">Prima di iniziare questo articolo, è necessario disporre di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="4ffc3-114">Before you begin this article, you must have hello following items:</span></span>

* <span data-ttu-id="4ffc3-115">**Un cluster Hadoop in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="4ffc3-115">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="4ffc3-116">Vedere [Introduzione all'uso di Hadoop basato su Linux in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4ffc3-116">See [Get started using Linux-based Hadoop in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="4ffc3-117">**Visual Studio 2013/2015/2017**.</span><span class="sxs-lookup"><span data-stu-id="4ffc3-117">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="4ffc3-118">Inviare processi MapReduce mediante HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="4ffc3-118">Submit MapReduce jobs using HDInsight .NET SDK</span></span>
<span data-ttu-id="4ffc3-119">Hello HDInsight .NET SDK fornisce librerie client .NET, che rende più semplice toowork con i cluster HDInsight da .NET.</span><span class="sxs-lookup"><span data-stu-id="4ffc3-119">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="4ffc3-120">**processi tooSubmit**</span><span class="sxs-lookup"><span data-stu-id="4ffc3-120">**tooSubmit jobs**</span></span>

1. <span data-ttu-id="4ffc3-121">Creare un'applicazione console C# in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4ffc3-121">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="4ffc3-122">Nella Console di gestione pacchetti Nuget hello, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4ffc3-122">From hello Nuget Package Manager Console, run hello following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="4ffc3-123">Utilizzare hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="4ffc3-123">Use hello following code:</span></span>
   
        using System.Collections.Generic;
        using System.IO;
        using System.Text;
        using System.Threading;
        using Microsoft.Azure.Management.HDInsight.Job;
        using Microsoft.Azure.Management.HDInsight.Job.Models;
        using Hyak.Common;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;

        namespace SubmitHDInsightJobDotNet
        {
            class Program
            {
                private static HDInsightJobManagementClient _hdiJobManagementClient;
   
                private const string existingClusterName = "<Your HDInsight Cluster Name>";
                private const string existingClusterUri = existingClusterName + ".azurehdinsight.net";
                private const string existingClusterUsername = "<Cluster Username>";
                private const string existingClusterPassword = "<Cluster User Password>";
   
                private const string defaultStorageAccountName = "<Default Storage Account Name>"; //<StorageAccountName>.blob.core.windows.net
                private const string defaultStorageAccountKey = "<Default Storage Account Key>";
                private const string defaultStorageContainerName = "<Default Blob Container Name>";

                private const string sourceFile = "/example/data/gutenberg/davinci.txt";  
                private const string outputFolder = "/example/data/davinciwordcount";
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("hello application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = existingClusterUsername, Password = existingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(existingClusterUri, clusterCredentials);
   
                    SubmitMRJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitMRJob()
                {
                    List<string> args = new List<string> { { "/example/data/gutenberg/davinci.txt" }, { "/example/data/davinciwordcount" } };
   
                    var paras = new MapReduceJobSubmissionParameters
                    {
                        JarFile = @"/example/jars/hadoop-mapreduce-examples.jar",
                        JarClass = "wordcount",
                        Arguments = args
                    };
   
                    System.Console.WriteLine("Submitting hello MR job toohello cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitMapReduceJob(paras);
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
                    System.Console.WriteLine("Job output is: ");
                    var storageAccess = new AzureStorageAccess(defaultStorageAccountName, defaultStorageAccountKey,
                        defaultStorageContainerName);
        
                    if (jobDetail.ExitValue == 0)
                    {
                        // Create hello storage account object
                        CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=" + 
                            defaultStorageAccountName + 
                            ";AccountKey=" + defaultStorageAccountKey);
        
                        // Create hello blob client.
                        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
        
                        // Retrieve reference tooa previously created container.
                        CloudBlobContainer container = blobClient.GetContainerReference(defaultStorageContainerName);
        
                        CloudBlockBlob blockBlob = container.GetBlockBlobReference(outputFolder.Substring(1) + "/part-r-00000");
        
                        using (var stream = blockBlob.OpenRead())
                        {
                            using (StreamReader reader = new StreamReader(stream))
                            {
                                while (!reader.EndOfStream)
                                {
                                    System.Console.WriteLine(reader.ReadLine());
                                }
                            }
                        }
                    }
                    else
                    {
                        // fetch stderr output in case of failure
                        var output = _hdiJobManagementClient.JobManagement.GetJobErrorLogs(jobId, storageAccess); 
        
                        using (var reader = new StreamReader(output, Encoding.UTF8))
                        {
                            string value = reader.ReadToEnd();
                            System.Console.WriteLine(value);
                        }
        
                    }
                }
            }
        }
4. <span data-ttu-id="4ffc3-124">Premere **F5** toorun un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="4ffc3-124">Press **F5** toorun hello application.</span></span>

<span data-ttu-id="4ffc3-125">il processo di hello toorun nuovamente, è necessario modificare hello output cartella nome del processo, nell'esempio hello, è "/ esempio/data/davinciwordcount".</span><span class="sxs-lookup"><span data-stu-id="4ffc3-125">toorun hello job again, you must change hello job output folder name, in hello sample, it is "/example/data/davinciwordcount".</span></span>

<span data-ttu-id="4ffc3-126">Quando hello viene completato correttamente, un'applicazione hello stampa contenuto hello del file di output di hello "parte-r-00000".</span><span class="sxs-lookup"><span data-stu-id="4ffc3-126">When hello job completes successfully, hello application prints hello content of hello output file "part-r-00000".</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ffc3-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4ffc3-127">Next steps</span></span>
<span data-ttu-id="4ffc3-128">In questo articolo sono state fornite diverse modi toocreate un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4ffc3-128">In this article, you have learned several ways toocreate an HDInsight cluster.</span></span> <span data-ttu-id="4ffc3-129">toolearn informazioni, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="4ffc3-129">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="4ffc3-130">Per l'invio di un processo Hive, vedere [Eseguire query Hive con HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="4ffc3-130">For submitting a Hive job, see [Run Hive queries using HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>
* <span data-ttu-id="4ffc3-131">Per creare cluster HDInsight, vedere [Creare cluster Hadoop basati su Linux in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="4ffc3-131">For creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="4ffc3-132">Per gestire cluster HDInsight, vedere [Gestire cluster Hadoop in HDInsight](hdinsight-administer-use-portal-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4ffc3-132">For managing HDInsight clusters, see [Manage Hadoop clusters in HDInsight](hdinsight-administer-use-portal-linux.md).</span></span>
* <span data-ttu-id="4ffc3-133">Per l'apprendimento hello HDInsight .NET SDK, vedere [riferimento HDInsight .NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ffc3-133">For learning hello HDInsight .NET SDK, see [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>
* <span data-ttu-id="4ffc3-134">Per non interattivo autenticare tooAzure, vedere [creare applicazioni di HDInsight .NET di autenticazione non interattivo](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="4ffc3-134">For non-interactive authenticate tooAzure, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

