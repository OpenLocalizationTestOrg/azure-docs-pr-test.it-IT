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
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a>Eseguire processi MapReduce con HDInsight .NET SDK
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

Informazioni su come i processi MapReduce toosubmit tramite HDInsight .NET SDK. I cluster HDInsight includono un file JAR con alcuni esempi di MapReduce. file jar Hello è */example/jars/hadoop-mapreduce-examples.jar*.  Uno degli esempi di hello è *wordcount*. Si sviluppa un toosubmit dei applicazione dei console c# un processo wordcount.  processo Hello legge hello */example/data/gutenberg/davinci.txt* file e gli output hello risultati troppo*/example/data/davinciwordcount*.  Se si desidera un'applicazione hello toorerun, è necessario pulire la cartella di output hello.

> [!NOTE]
> passaggi di Hello in questo articolo devono essere eseguiti da un client di Windows. Per informazioni sull'uso di un Linux, OS X o toowork client Unix con Hive, usare il selettore di scheda hello visualizzato nella parte superiore di hello di articolo hello.
> 
> 

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questo articolo, è necessario disporre di hello seguenti elementi:

* **Un cluster Hadoop in HDInsight**. Vedere [Introduzione all'uso di Hadoop basato su Linux in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).
* **Visual Studio 2013/2015/2017**.

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a>Inviare processi MapReduce mediante HDInsight .NET SDK
Hello HDInsight .NET SDK fornisce librerie client .NET, che rende più semplice toowork con i cluster HDInsight da .NET. 

**processi tooSubmit**

1. Creare un'applicazione console C# in Visual Studio.
2. Nella Console di gestione pacchetti Nuget hello, eseguire hello comando seguente:
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. Utilizzare hello seguente codice:
   
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
4. Premere **F5** toorun un'applicazione hello.

il processo di hello toorun nuovamente, è necessario modificare hello output cartella nome del processo, nell'esempio hello, è "/ esempio/data/davinciwordcount".

Quando hello viene completato correttamente, un'applicazione hello stampa contenuto hello del file di output di hello "parte-r-00000".

## <a name="next-steps"></a>Passaggi successivi
In questo articolo sono state fornite diverse modi toocreate un cluster HDInsight. toolearn informazioni, vedere hello seguenti articoli:

* Per l'invio di un processo Hive, vedere [Eseguire query Hive con HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).
* Per creare cluster HDInsight, vedere [Creare cluster Hadoop basati su Linux in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
* Per gestire cluster HDInsight, vedere [Gestire cluster Hadoop in HDInsight](hdinsight-administer-use-portal-linux.md).
* Per l'apprendimento hello HDInsight .NET SDK, vedere [riferimento HDInsight .NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).
* Per non interattivo autenticare tooAzure, vedere [creare applicazioni di HDInsight .NET di autenticazione non interattivo](hdinsight-create-non-interactive-authentication-dotnet-applications.md).

