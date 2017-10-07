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
# <a name="run-hive-queries-using-hdinsight-net-sdk"></a>Eseguire query Hive con HDInsight .NET SDK
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Informazioni su come toosubmit Hive query che utilizzano HDInsight .NET SDK. Scrivere una query Hive per elencare le tabelle Hive di toosubmit un programma c# e visualizzare i risultati di hello.

> [!NOTE]
> passaggi di Hello in questo articolo devono essere eseguiti da un client di Windows. Per informazioni sull'uso di un Linux, OS X o toowork client Unix con Hive, usare il selettore di scheda hello visualizzato nella parte superiore di hello di articolo hello.
> 
> 

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questo articolo, è necessario disporre di hello seguenti elementi:

* **Un cluster Hadoop in HDInsight**. Vedere [Introduzione all'uso di Hadoop basato su Linux in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).
* **Visual Studio 2013/2015/2017**.

## <a name="submit-hive-queries-using-hdinsight-net-sdk"></a>Inviare query Hive con HDInsight .NET SDK
Hello HDInsight .NET SDK fornisce librerie client .NET, che rende più semplice toowork con i cluster HDInsight da .NET. 

**processi tooSubmit**

1. Creare un'applicazione console C# in Visual Studio.
2. Nella Console di gestione pacchetti Nuget hello, eseguire hello comando seguente:
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. Utilizzare hello seguente codice:

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
4. Premere **F5** toorun un'applicazione hello.

output di Hello di un'applicazione hello deve essere simile a:

![Output processo Hive Hadoop di HDInsight](./media/hdinsight-hadoop-use-hive-dotnet-sdk/hdinsight-hadoop-use-hive-net-sdk-output.png)

## <a name="next-steps"></a>Passaggi successivi
In questo articolo sono state fornite diverse modi toocreate un cluster HDInsight. toolearn informazioni, vedere hello seguenti articoli:

* [Introduzione ad Azure HDInsight][hdinsight-get-started]
* [Creare cluster Hadoop in HDInsight][hdinsight-provision]
* [Gestire i cluster Hadoop in HDInsight con hello portale di Azure](hdinsight-administer-use-management-portal.md)
* [Riferimento a HDInsight .NET SDK](https://msdn.microsoft.com/library/mt271028.aspx)
* [Usare Pig con HDInsight](hdinsight-use-pig.md)
* [Usare Sqoop con Hadoop in HDInsight](hdinsight-use-sqoop-mac-linux.md)
* [Creare applicazioni .NET HDInsight di autenticazione non interattive](hdinsight-create-non-interactive-authentication-dotnet-applications.md)

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md


