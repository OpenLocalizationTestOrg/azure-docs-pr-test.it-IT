---
title: Eseguire processi Apache Pig con .NET SDK per Hadoop - Azure HDInsight | Microsoft Docs
description: Informazioni su come usare .NET SDK per Hadoop per inviare processi Pig a Hadoop in HDInsight.
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
ms.date: 11/08/2017
ms.author: larryfr
ms.openlocfilehash: c828a7b63e70669ed38ecea898442a3978e67ba7
ms.sourcegitcommit: 93902ffcb7c8550dcb65a2a5e711919bd1d09df9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/09/2017
---
# <a name="run-pig-jobs-using-the-net-sdk-for-hadoop-in-hdinsight"></a>Esecuzione di processi Pig con .NET SDK per Hadoop in HDInsight

[!INCLUDE [pig-selector](../../../includes/hdinsight-selector-use-pig.md)]

Informazioni su come usare .NET SDK per Hadoop per inviare processi Apache Pig a Hadoop in Azure HDInsight.

HDInsight .NET SDK fornisce librerie client .NET che semplificano l'utilizzo dei cluster HDInsight da .NET. Pig consente di creare operazioni MapReduce modellando una serie di trasformazioni di dati. Questo articolo illustra come usare un'applicazione di base C# per inviare un processo Pig a un cluster HDInsight.

## <a name="prerequisites"></a>Prerequisiti

Per seguire la procedura descritta in questo articolo, sono necessari gli elementi seguenti.

* Un cluster Azure HDInsight (Hadoop in HDInsight) basato su Windows o su Linux.

  > [!IMPORTANT]
  > Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Visual Studio 2012, 2013, 2015 o 2017.

## <a name="create-the-application"></a>Creazione dell'applicazione

HDInsight .NET SDK fornisce librerie client .NET che semplificano l'uso dei cluster HDInsight da .NET.

1. In Visual Studio scegliere **Nuovo** dal menu **File**, quindi fare clic su **Progetto**.

2. Nella finestra di dialogo Nuovo progetto digitare o selezionare i valori seguenti:

   | Proprietà | Valore |
   | ------ | ------ |
   | Categoria | Templates/Visual C#/Windows |
   | Modello | Applicazione console |
   | Nome | SubmitPigJob |

3. Fare clic su **OK** per creare il progetto.

4. Selezionare **Gestione pacchetti libreria**  o **Gestione pacchetti NuGet** dal menu **Strumenti** e quindi scegliere **Console di Gestione pacchetti**.

5. Per installare i pacchetti .NET SDK, usare il comando seguente:

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. In Esplora soluzioni fare doppio clic su **Program.cs** per aprirlo. Replace Sostituire il codice esistente con il seguente.

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
                System.Console.WriteLine("The application is running ...");

                var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);

                SubmitPigJob();

                System.Console.WriteLine("Press ENTER to continue ...");
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

                System.Console.WriteLine("Submitting the Pig job to the cluster...");
                var response = _hdiJobManagementClient.JobManagement.SubmitPigJob(parameters);
                System.Console.WriteLine("Validating that the response is as expected...");
                System.Console.WriteLine("Response status code is " + response.StatusCode);
                System.Console.WriteLine("Validating the response object...");
                System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
            }
        }
    }
    ```

7. Per avviare l'applicazione, premere **F5**.

8. Per uscire dall'applicazione, premere **INVIO**.

## <a name="next-steps"></a>Passaggi successivi

Per informazioni su Pig in HDInsight, vedere [Usare Pig con Hadoop in HDInsight](hdinsight-use-pig.md).

Per altre informazioni sull'uso di Hadoop con HDInsight, vedere i documenti seguenti:

* [Usare Hive con Hadoop in HDInsight](hdinsight-use-hive.md)
* [Usare MapReduce con Hadoop in HDInsight](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
