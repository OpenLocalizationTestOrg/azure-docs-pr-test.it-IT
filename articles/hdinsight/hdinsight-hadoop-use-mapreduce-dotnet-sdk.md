---
title: Inviare processi MapReduce con HDInsight .NET SDK - Azure | Microsoft Docs
description: Informazioni su come inviare processi MapReduce ad Azure HDInsight Hadoop con HDInsight .NET SDK.
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
ms.openlocfilehash: 015435270c31bafea0ebf5303b459338755c1410
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="0d2f2-103">Eseguire processi MapReduce con HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="0d2f2-103">Run MapReduce jobs using HDInsight .NET SDK</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="0d2f2-104">Informazioni su come inviare processi MapReduce con HDInsight .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="0d2f2-104">Learn how to submit MapReduce jobs using HDInsight .NET SDK.</span></span> <span data-ttu-id="0d2f2-105">I cluster HDInsight includono un file JAR con alcuni esempi di MapReduce.</span><span class="sxs-lookup"><span data-stu-id="0d2f2-105">HDInsight clusters come with a jar file with some MapReduce samples.</span></span> <span data-ttu-id="0d2f2-106">Il file JAR è */example/jars/hadoop-mapreduce-examples.jar*.</span><span class="sxs-lookup"><span data-stu-id="0d2f2-106">The jar file is */example/jars/hadoop-mapreduce-examples.jar*.</span></span>  <span data-ttu-id="0d2f2-107">Uno degli esempi è *wordcount*.</span><span class="sxs-lookup"><span data-stu-id="0d2f2-107">One of the samples is *wordcount*.</span></span> <span data-ttu-id="0d2f2-108">Per inviare un processo wordcount, è necessario sviluppare un'applicazione console C#.</span><span class="sxs-lookup"><span data-stu-id="0d2f2-108">You develop a C# console application to submit a wordcount job.</span></span>  <span data-ttu-id="0d2f2-109">Il processo legge il file */example/data/gutenberg/davinci.txt* e restituisce i risultati in */example/data/davinciwordcount*.</span><span class="sxs-lookup"><span data-stu-id="0d2f2-109">The job reads the */example/data/gutenberg/davinci.txt* file, and outputs the results to */example/data/davinciwordcount*.</span></span>  <span data-ttu-id="0d2f2-110">Se si vuole eseguire di nuovo l'applicazione, è necessario pulire la cartella di output.</span><span class="sxs-lookup"><span data-stu-id="0d2f2-110">If you want to rerun the application, you must clean up the output folder.</span></span>

> [!NOTE]
> <span data-ttu-id="0d2f2-111">I passaggi descritti in questo articolo devono essere eseguiti da un client Windows.</span><span class="sxs-lookup"><span data-stu-id="0d2f2-111">The steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="0d2f2-112">Per informazioni sull'uso di un client Linux, OS X o Unix con Hive, usare il selettore di schede visualizzato all'inizio dell'articolo.</span><span class="sxs-lookup"><span data-stu-id="0d2f2-112">For information on using a Linux, OS X, or Unix client to work with Hive, use the tab selector shown on the top of the article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="0d2f2-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0d2f2-113">Prerequisites</span></span>
<span data-ttu-id="0d2f2-114">Per eseguire le procedure descritte nell'articolo sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0d2f2-114">Before you begin this article, you must have the following items:</span></span>

* <span data-ttu-id="0d2f2-115">**Un cluster Hadoop in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="0d2f2-115">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="0d2f2-116">Vedere [Introduzione all'uso di Hadoop basato su Linux in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0d2f2-116">See [Get started using Linux-based Hadoop in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="0d2f2-117">**Visual Studio 2013/2015/2017**.</span><span class="sxs-lookup"><span data-stu-id="0d2f2-117">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="0d2f2-118">Inviare processi MapReduce mediante HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="0d2f2-118">Submit MapReduce jobs using HDInsight .NET SDK</span></span>
<span data-ttu-id="0d2f2-119">HDInsight .NET SDK fornisce librerie client .NET che semplificano l'uso dei cluster HDInsight da .NET.</span><span class="sxs-lookup"><span data-stu-id="0d2f2-119">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="0d2f2-120">**Inviare i processi**</span><span class="sxs-lookup"><span data-stu-id="0d2f2-120">**To Submit jobs**</span></span>

1. <span data-ttu-id="0d2f2-121">Creare un'applicazione console C# in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0d2f2-121">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="0d2f2-122">Dalla console di Gestione pacchetti NuGet eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0d2f2-122">From the Nuget Package Manager Console, run the following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="0d2f2-123">Usare il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="0d2f2-123">Use the following code:</span></span>
   
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
                    System.Console.WriteLine("The application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = existingClusterUsername, Password = existingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(existingClusterUri, clusterCredentials);
   
                    SubmitMRJob();
   
                    System.Console.WriteLine("Press ENTER to continue ...");
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
   
                    System.Console.WriteLine("Submitting the MR job to the cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitMapReduceJob(paras);
                    var jobId = jobResponse.JobSubmissionJsonResponse.Id;
                    System.Console.WriteLine("Response status code is " + jobResponse.StatusCode);
                    System.Console.WriteLine("JobId is " + jobId);
   
                    System.Console.WriteLine("Waiting for the job completion ...");
   
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
                        // Create the storage account object
                        CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=" + 
                            defaultStorageAccountName + 
                            ";AccountKey=" + defaultStorageAccountKey);
        
                        // Create the blob client.
                        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
        
                        // Retrieve reference to a previously created container.
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
4. <span data-ttu-id="0d2f2-124">Premere **F5** per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0d2f2-124">Press **F5** to run the application.</span></span>

<span data-ttu-id="0d2f2-125">Per eseguire nuovamente il processo, è necessario cambiare il nome della cartella di output del processo, che nell'esempio è: "/example/data/davinciwordcount".</span><span class="sxs-lookup"><span data-stu-id="0d2f2-125">To run the job again, you must change the job output folder name, in the sample, it is "/example/data/davinciwordcount".</span></span>

<span data-ttu-id="0d2f2-126">Al completamento del processo, l'applicazione stampa il contenuto del file di output "part-r-00000".</span><span class="sxs-lookup"><span data-stu-id="0d2f2-126">When the job completes successfully, the application prints the content of the output file "part-r-00000".</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d2f2-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0d2f2-127">Next steps</span></span>
<span data-ttu-id="0d2f2-128">Questo articolo ha spiegato vari modi per creare un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0d2f2-128">In this article, you have learned several ways to create an HDInsight cluster.</span></span> <span data-ttu-id="0d2f2-129">Per altre informazioni, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="0d2f2-129">To learn more, see the following articles:</span></span>

* <span data-ttu-id="0d2f2-130">Per l'invio di un processo Hive, vedere [Eseguire query Hive con HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="0d2f2-130">For submitting a Hive job, see [Run Hive queries using HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>
* <span data-ttu-id="0d2f2-131">Per creare cluster HDInsight, vedere [Creare cluster Hadoop basati su Linux in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="0d2f2-131">For creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="0d2f2-132">Per gestire cluster HDInsight, vedere [Gestire cluster Hadoop in HDInsight](hdinsight-administer-use-portal-linux.md).</span><span class="sxs-lookup"><span data-stu-id="0d2f2-132">For managing HDInsight clusters, see [Manage Hadoop clusters in HDInsight](hdinsight-administer-use-portal-linux.md).</span></span>
* <span data-ttu-id="0d2f2-133">Per informazioni su HDInsight .NET SDK, vedere [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx) (Informazioni di riferimento su HDInsight .NET SDK).</span><span class="sxs-lookup"><span data-stu-id="0d2f2-133">For learning the HDInsight .NET SDK, see [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>
* <span data-ttu-id="0d2f2-134">Per usare l'autenticazione non interattiva in Azure, vedere [Creare applicazioni .NET HDInsight di autenticazione non interattive](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="0d2f2-134">For non-interactive authenticate to Azure, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

