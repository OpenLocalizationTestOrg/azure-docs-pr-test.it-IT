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
# <a name="run-pig-jobs-using-hello-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="0a7f3-103">Eseguire i processi Pig utilizzando hello .NET SDK per Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="0a7f3-103">Run Pig jobs using hello .NET SDK for Hadoop in HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="0a7f3-104">Informazioni su come toouse hello .NET SDK per Hadoop toosubmit Apache Pig processi tooHadoop in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0a7f3-104">Learn how toouse hello .NET SDK for Hadoop toosubmit Apache Pig jobs tooHadoop on Azure HDInsight.</span></span>

<span data-ttu-id="0a7f3-105">Hello HDInsight .NET SDK fornisce librerie client .NET che rende più semplice toowork con i cluster HDInsight da .NET.</span><span class="sxs-lookup"><span data-stu-id="0a7f3-105">hello HDInsight .NET SDK provides .NET client libraries that makes it easier toowork with HDInsight clusters from .NET.</span></span> <span data-ttu-id="0a7f3-106">Pig consente operazioni MapReduce toocreate modellando una serie di trasformazioni di dati.</span><span class="sxs-lookup"><span data-stu-id="0a7f3-106">Pig allows you toocreate MapReduce operations by modeling a series of data transformations.</span></span> <span data-ttu-id="0a7f3-107">In questo documento, viene illustrato come toouse base c# applicazione toosubmit un Pig processo cluster HDInsight tooan.</span><span class="sxs-lookup"><span data-stu-id="0a7f3-107">In this document, you learn how toouse a basic C# application toosubmit a Pig job tooan HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a7f3-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0a7f3-108">Prerequisites</span></span>

<span data-ttu-id="0a7f3-109">passaggi di hello toocomplete in questo articolo, è necessario seguente hello.</span><span class="sxs-lookup"><span data-stu-id="0a7f3-109">toocomplete hello steps in this article, you need hello following.</span></span>

* <span data-ttu-id="0a7f3-110">Un cluster Azure HDInsight (Hadoop in HDInsight) basato su Windows o su Linux.</span><span class="sxs-lookup"><span data-stu-id="0a7f3-110">An Azure HDInsight (Hadoop on HDInsight) cluster (either Windows or Linux-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="0a7f3-111">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="0a7f3-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0a7f3-112">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="0a7f3-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="0a7f3-113">Visual Studio 2012, 2013, 2015 o 2017.</span><span class="sxs-lookup"><span data-stu-id="0a7f3-113">Visual Studio 2012, 2013, 2015 or 2017.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="0a7f3-114">Creare un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="0a7f3-114">Create hello application</span></span>

<span data-ttu-id="0a7f3-115">Hello HDInsight .NET SDK fornisce librerie client .NET, che rende più semplice toowork con i cluster HDInsight da .NET.</span><span class="sxs-lookup"><span data-stu-id="0a7f3-115">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span>

1. <span data-ttu-id="0a7f3-116">Da hello **File** menu in Visual Studio, selezionare **New** e quindi selezionare **progetto**.</span><span class="sxs-lookup"><span data-stu-id="0a7f3-116">From hello **File** menu in Visual Studio, select **New** and then select **Project**.</span></span>

2. <span data-ttu-id="0a7f3-117">Per hello nuovo progetto di tipo o seleziona hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="0a7f3-117">For hello new project, type or select hello following values:</span></span>

   | <span data-ttu-id="0a7f3-118">Proprietà</span><span class="sxs-lookup"><span data-stu-id="0a7f3-118">Property</span></span> | <span data-ttu-id="0a7f3-119">Valore</span><span class="sxs-lookup"><span data-stu-id="0a7f3-119">Value</span></span> |
   | ------ | ------ |
   | <span data-ttu-id="0a7f3-120">Categoria</span><span class="sxs-lookup"><span data-stu-id="0a7f3-120">Category</span></span> | <span data-ttu-id="0a7f3-121">Templates/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="0a7f3-121">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="0a7f3-122">Modello</span><span class="sxs-lookup"><span data-stu-id="0a7f3-122">Template</span></span> | <span data-ttu-id="0a7f3-123">Applicazione console</span><span class="sxs-lookup"><span data-stu-id="0a7f3-123">Console Application</span></span> |
   | <span data-ttu-id="0a7f3-124">Nome</span><span class="sxs-lookup"><span data-stu-id="0a7f3-124">Name</span></span> | <span data-ttu-id="0a7f3-125">SubmitPigJob</span><span class="sxs-lookup"><span data-stu-id="0a7f3-125">SubmitPigJob</span></span> |

3. <span data-ttu-id="0a7f3-126">Fare clic su **OK** progetto hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="0a7f3-126">Click **OK** toocreate hello project.</span></span>

4. <span data-ttu-id="0a7f3-127">Da hello **strumenti** dal menu **Gestione pacchetti libreria** o **Gestione pacchetti Nuget**, quindi selezionare **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="0a7f3-127">From hello **Tools** menu, select **Library Package Manager** or **Nuget Package Manager**, and then select **Package Manager Console**.</span></span>

5. <span data-ttu-id="0a7f3-128">i pacchetti hello .NET SDK tooinstall, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0a7f3-128">tooinstall hello .NET SDK packages, use hello following command:</span></span>

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. <span data-ttu-id="0a7f3-129">Da Esplora soluzioni fare doppio clic su **Program.cs** tooopen è.</span><span class="sxs-lookup"><span data-stu-id="0a7f3-129">From Solution Explorer, double-click **Program.cs** tooopen it.</span></span> <span data-ttu-id="0a7f3-130">Sostituire il codice esistente hello con seguenti hello.</span><span class="sxs-lookup"><span data-stu-id="0a7f3-130">Replace hello existing code with hello following.</span></span>

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

7. <span data-ttu-id="0a7f3-131">un'applicazione hello toostart, premere **F5**.</span><span class="sxs-lookup"><span data-stu-id="0a7f3-131">toostart hello application, press **F5**.</span></span>

8. <span data-ttu-id="0a7f3-132">un'applicazione hello tooexit, premere **invio**.</span><span class="sxs-lookup"><span data-stu-id="0a7f3-132">tooexit hello application, press **ENTER**.</span></span>

## <a name="summary"></a><span data-ttu-id="0a7f3-133">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="0a7f3-133">Summary</span></span>

<span data-ttu-id="0a7f3-134">Come si può notare, hello .NET SDK per Hadoop consente applicazioni .NET toocreate che invia i cluster di HDInsight tooan processi Pig e monitorare lo stato del processo hello.</span><span class="sxs-lookup"><span data-stu-id="0a7f3-134">As you can see, hello .NET SDK for Hadoop allows you toocreate .NET applications that submit Pig jobs tooan HDInsight cluster, and monitor hello job status.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a7f3-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0a7f3-135">Next steps</span></span>

<span data-ttu-id="0a7f3-136">Per informazioni su Pig in HDInsight, vedere [Usare Pig con Hadoop in HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="0a7f3-136">For information on Pig in HDInsight, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

<span data-ttu-id="0a7f3-137">Per ulteriori informazioni sull'utilizzo di Hadoop in HDInsight, vedere hello seguenti documenti:</span><span class="sxs-lookup"><span data-stu-id="0a7f3-137">For more information on using Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="0a7f3-138">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="0a7f3-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="0a7f3-139">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="0a7f3-139">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
