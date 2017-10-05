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
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: e40d152821b36852c447d5a3adfd39114edbbace
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="run-pig-jobs-using-the-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="da0e9-103">Esecuzione di processi Pig con .NET SDK per Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="da0e9-103">Run Pig jobs using the .NET SDK for Hadoop in HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="da0e9-104">Informazioni su come usare .NET SDK per Hadoop per inviare processi Apache Pig a Hadoop in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="da0e9-104">Learn how to use the .NET SDK for Hadoop to submit Apache Pig jobs to Hadoop on Azure HDInsight.</span></span>

<span data-ttu-id="da0e9-105">HDInsight .NET SDK fornisce librerie client .NET che semplificano l'utilizzo dei cluster HDInsight da .NET.</span><span class="sxs-lookup"><span data-stu-id="da0e9-105">The HDInsight .NET SDK provides .NET client libraries that makes it easier to work with HDInsight clusters from .NET.</span></span> <span data-ttu-id="da0e9-106">Pig consente di creare operazioni MapReduce modellando una serie di trasformazioni di dati.</span><span class="sxs-lookup"><span data-stu-id="da0e9-106">Pig allows you to create MapReduce operations by modeling a series of data transformations.</span></span> <span data-ttu-id="da0e9-107">Questo articolo illustra come usare un'applicazione di base C# per inviare un processo Pig a un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="da0e9-107">In this document, you learn how to use a basic C# application to submit a Pig job to an HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da0e9-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="da0e9-108">Prerequisites</span></span>

<span data-ttu-id="da0e9-109">Per seguire la procedura descritta in questo articolo, sono necessari gli elementi seguenti.</span><span class="sxs-lookup"><span data-stu-id="da0e9-109">To complete the steps in this article, you need the following.</span></span>

* <span data-ttu-id="da0e9-110">Un cluster Azure HDInsight (Hadoop in HDInsight) basato su Windows o su Linux.</span><span class="sxs-lookup"><span data-stu-id="da0e9-110">An Azure HDInsight (Hadoop on HDInsight) cluster (either Windows or Linux-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="da0e9-111">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="da0e9-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="da0e9-112">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="da0e9-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="da0e9-113">Visual Studio 2012, 2013, 2015 o 2017.</span><span class="sxs-lookup"><span data-stu-id="da0e9-113">Visual Studio 2012, 2013, 2015 or 2017.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="da0e9-114">Creazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="da0e9-114">Create the application</span></span>

<span data-ttu-id="da0e9-115">HDInsight .NET SDK fornisce librerie client .NET che semplificano l'uso dei cluster HDInsight da .NET.</span><span class="sxs-lookup"><span data-stu-id="da0e9-115">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span>

1. <span data-ttu-id="da0e9-116">In Visual Studio scegliere **Nuovo** dal menu **File**, quindi fare clic su **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="da0e9-116">From the **File** menu in Visual Studio, select **New** and then select **Project**.</span></span>

2. <span data-ttu-id="da0e9-117">Nella finestra di dialogo Nuovo progetto digitare o selezionare i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="da0e9-117">For the new project, type or select the following values:</span></span>

   | <span data-ttu-id="da0e9-118">Proprietà</span><span class="sxs-lookup"><span data-stu-id="da0e9-118">Property</span></span> | <span data-ttu-id="da0e9-119">Valore</span><span class="sxs-lookup"><span data-stu-id="da0e9-119">Value</span></span> |
   | ------ | ------ |
   | <span data-ttu-id="da0e9-120">Categoria</span><span class="sxs-lookup"><span data-stu-id="da0e9-120">Category</span></span> | <span data-ttu-id="da0e9-121">Templates/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="da0e9-121">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="da0e9-122">Modello</span><span class="sxs-lookup"><span data-stu-id="da0e9-122">Template</span></span> | <span data-ttu-id="da0e9-123">Applicazione console</span><span class="sxs-lookup"><span data-stu-id="da0e9-123">Console Application</span></span> |
   | <span data-ttu-id="da0e9-124">Nome</span><span class="sxs-lookup"><span data-stu-id="da0e9-124">Name</span></span> | <span data-ttu-id="da0e9-125">SubmitPigJob</span><span class="sxs-lookup"><span data-stu-id="da0e9-125">SubmitPigJob</span></span> |

3. <span data-ttu-id="da0e9-126">Fare clic su **OK** per creare il progetto.</span><span class="sxs-lookup"><span data-stu-id="da0e9-126">Click **OK** to create the project.</span></span>

4. <span data-ttu-id="da0e9-127">Selezionare **Library Package Manager** (Gestione pacchetti libreria) o **Gestione pacchetti NuGet** dal menu **Strumenti** e quindi scegliere **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="da0e9-127">From the **Tools** menu, select **Library Package Manager** or **Nuget Package Manager**, and then select **Package Manager Console**.</span></span>

5. <span data-ttu-id="da0e9-128">Per installare i pacchetti .NET SDK, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="da0e9-128">To install the .NET SDK packages, use the following command:</span></span>

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. <span data-ttu-id="da0e9-129">In Esplora soluzioni fare doppio clic su **Program.cs** per aprirlo.</span><span class="sxs-lookup"><span data-stu-id="da0e9-129">From Solution Explorer, double-click **Program.cs** to open it.</span></span> <span data-ttu-id="da0e9-130">Replace Sostituire il codice esistente con il seguente.</span><span class="sxs-lookup"><span data-stu-id="da0e9-130">Replace the existing code with the following.</span></span>

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

7. <span data-ttu-id="da0e9-131">Per avviare l'applicazione, premere **F5**.</span><span class="sxs-lookup"><span data-stu-id="da0e9-131">To start the application, press **F5**.</span></span>

8. <span data-ttu-id="da0e9-132">Per uscire dall'applicazione, premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="da0e9-132">To exit the application, press **ENTER**.</span></span>

## <a name="summary"></a><span data-ttu-id="da0e9-133">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="da0e9-133">Summary</span></span>

<span data-ttu-id="da0e9-134">Come si può notare, .NET SDK per Hadoop consente di creare applicazioni .NET che inviano processi Pig a un cluster HDInsight e di monitorare lo stato del processo.</span><span class="sxs-lookup"><span data-stu-id="da0e9-134">As you can see, the .NET SDK for Hadoop allows you to create .NET applications that submit Pig jobs to an HDInsight cluster, and monitor the job status.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da0e9-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="da0e9-135">Next steps</span></span>

<span data-ttu-id="da0e9-136">Per informazioni su Pig in HDInsight, vedere [Usare Pig con Hadoop in HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="da0e9-136">For information on Pig in HDInsight, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

<span data-ttu-id="da0e9-137">Per altre informazioni sull'uso di Hadoop con HDInsight, vedere i documenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="da0e9-137">For more information on using Hadoop on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="da0e9-138">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="da0e9-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="da0e9-139">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="da0e9-139">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
