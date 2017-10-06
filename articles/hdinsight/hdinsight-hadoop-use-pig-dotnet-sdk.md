---
title: processi di aaaRun Apache Pig con .NET SDK per Hadoop - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come toouse hello .NET SDK per tooHadoop i processi di Hadoop toosubmit Pig in HDInsight.
services: hdinsight
documentationcenter: .net
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: fa11d49a-328c-47e7-b16d-e7ed2a453195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 1d4ceebd7c168372d23fe29a088f04676686de30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-using-hello-net-sdk-for-hadoop-in-hdinsight"></a>Eseguire i processi Pig utilizzando hello .NET SDK per Hadoop in HDInsight

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Informazioni su come toouse hello .NET SDK per Hadoop toosubmit Apache Pig processi tooHadoop in Azure HDInsight.

Hello HDInsight .NET SDK fornisce librerie client .NET che rende più semplice toowork con i cluster HDInsight da .NET. Pig consente operazioni MapReduce toocreate modellando una serie di trasformazioni di dati. In questo documento, viene illustrato come toouse base c# applicazione toosubmit un Pig processo cluster HDInsight tooan.

## <a name="prerequisites"></a>Prerequisiti

passaggi di hello toocomplete in questo articolo, è necessario seguente hello.

* Un cluster Azure HDInsight (Hadoop in HDInsight) basato su Windows o su Linux.

  > [!IMPORTANT]
  > Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Visual Studio 2012, 2013, 2015 o 2017.

## <a name="create-hello-application"></a>Creare un'applicazione hello

Hello HDInsight .NET SDK fornisce librerie client .NET, che rende più semplice toowork con i cluster HDInsight da .NET.

1. Da hello **File** menu in Visual Studio, selezionare **New** e quindi selezionare **progetto**.

2. Per hello nuovo progetto di tipo o seleziona hello seguenti valori:

   | Proprietà | Valore |
   | ------ | ------ |
   | Categoria | Templates/Visual C#/Windows |
   | Modello | Applicazione console |
   | Nome | SubmitPigJob |

3. Fare clic su **OK** progetto hello toocreate.

4. Da hello **strumenti** dal menu **Gestione pacchetti libreria** o **Gestione pacchetti Nuget**, quindi selezionare **Package Manager Console**.

5. i pacchetti hello .NET SDK tooinstall, utilizzare hello comando seguente:

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. Da Esplora soluzioni fare doppio clic su **Program.cs** tooopen è. Sostituire il codice esistente hello con seguenti hello.

    ```csharp
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

                SubmitPigJob();

                System.Console.WriteLine("Press ENTER toocontinue ...");
                System.Console.ReadLine();
            }

            private static void SubmitPigJob()
            {
                var parameters = new PigJobSubmissionParameters
                {
                    Query = @"LOGS = LOAD '/example/data/sample.log';
                                LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
                                FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
                                GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
                                FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
                                RESULT = order FREQUENCIES by COUNT desc;
                                DUMP RESULT;"
                };

                System.Console.WriteLine("Submitting hello Pig job toohello cluster...");
                var response = _hdiJobManagementClient.JobManagement.SubmitPigJob(parameters);
                System.Console.WriteLine("Validating that hello response is as expected...");
                System.Console.WriteLine("Response status code is " + response.StatusCode);
                System.Console.WriteLine("Validating hello response object...");
                System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
            }
        }
    }
    ```

7. un'applicazione hello toostart, premere **F5**.

8. un'applicazione hello tooexit, premere **invio**.

## <a name="summary"></a>Riepilogo

Come si può notare, hello .NET SDK per Hadoop consente applicazioni .NET toocreate che invia i cluster di HDInsight tooan processi Pig e monitorare lo stato del processo hello.

## <a name="next-steps"></a>Passaggi successivi

Per informazioni su Pig in HDInsight, vedere [Usare Pig con Hadoop in HDInsight](hdinsight-use-pig.md).

Per ulteriori informazioni sull'utilizzo di Hadoop in HDInsight, vedere hello seguenti documenti:

* [Usare Hive con Hadoop in HDInsight](hdinsight-use-hive.md)
* [Usare MapReduce con Hadoop in HDInsight](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
