---
title: Usare .NET con Hadoop MapReduce in HDInsight basato su Linux - Azure | Microsoft Docs
description: Informazioni su come usare le applicazioni .NET per lo streaming di MapReduce in HDInsight basato su Linux.
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 6ad188fb752474ff5c7d8a3fb9d609eefe8c7a9a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="migrate-net-solutions-for-windows-based-hdinsight-to-linux-based-hdinsight"></a><span data-ttu-id="b1246-103">Eseguire la migrazione di soluzioni .NET per HDInsight basato su Windows a HDInsight basato su Linux</span><span class="sxs-lookup"><span data-stu-id="b1246-103">Migrate .NET solutions for Windows-based HDInsight to Linux-based HDInsight</span></span>

<span data-ttu-id="b1246-104">I cluster HDInsight basati su Linux usano [Mono (https://mono-project.com)](https://mono-project.com) per eseguire le applicazioni .NET.</span><span class="sxs-lookup"><span data-stu-id="b1246-104">Linux-based HDInsight clusters use [Mono (https://mono-project.com)](https://mono-project.com) to run .NET applications.</span></span> <span data-ttu-id="b1246-105">Mono consente di usare i componenti .NET, ad esempio applicazioni MapReduce con HDInsight basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="b1246-105">Mono allows you to use .NET components such as MapReduce applications with Linux-based HDInsight.</span></span> <span data-ttu-id="b1246-106">In questo documento vengono fornite informazioni su come eseguire la migrazione di soluzioni .NET create per fare funzionare i cluster HDInsight basati su Windows con Mono in HDInsight basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="b1246-106">In this document, learn how to migrate .NET solutions created for Windows-based HDInsight clusters to work with Mono on Linux-based HDInsight.</span></span>

## <a name="mono-compatibility-with-net"></a><span data-ttu-id="b1246-107">Compatibilità Mono con .NET</span><span class="sxs-lookup"><span data-stu-id="b1246-107">Mono compatibility with .NET</span></span>

<span data-ttu-id="b1246-108">La versione Mono 4.2.1 è inclusa nella versione 3.5 di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b1246-108">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="b1246-109">Per altre informazioni sulla versione Mono compresa in HDInsight, vedere [Componenti e versioni di Hadoop disponibili in HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="b1246-109">For more information on the version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="b1246-110">Per installare una versione specifica di Mono, vedere il documento [Install or update Mono](hdinsight-hadoop-install-mono.md) (Installare o aggiornare Mono).</span><span class="sxs-lookup"><span data-stu-id="b1246-110">To install a specific version of Mono, see the [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="b1246-111">Per informazioni dettagliate sulla compatibilità tra Mono e .NET, vedere il documento sulla [compatibilità Mono (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="b1246-111">For detailed information on compatibility between Mono and .NET, see the [Mono compatibility (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b1246-112">Il framework SCP.NET è compatibile con Mono.</span><span class="sxs-lookup"><span data-stu-id="b1246-112">The SCP.NET framework is compatible with Mono.</span></span> <span data-ttu-id="b1246-113">Per altre informazioni sull'uso di SCP.NET con Mono, vedere [Sviluppare topologie C# per Apache Storm in HDInsight tramite gli strumenti Hadoop per Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="b1246-113">For more information on using SCP.NET with Mono, see [Use Visual Studio to develop C# topologies for Apache Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

## <a name="automated-portability-analysis"></a><span data-ttu-id="b1246-114">Analisi di portabilità automatizzata</span><span class="sxs-lookup"><span data-stu-id="b1246-114">Automated portability analysis</span></span>

<span data-ttu-id="b1246-115">[.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) può essere usato per generare un rapporto di incompatibilità tra l'applicazione e Mono.</span><span class="sxs-lookup"><span data-stu-id="b1246-115">The [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) can be used to generate a report of incompatibilities between your application and Mono.</span></span> <span data-ttu-id="b1246-116">Per configurare l'analizzatore per il controllo dell'applicazione per la portabilità Mono, usare la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b1246-116">Use the following steps to configure the analyzer to check your application for Mono portability:</span></span>

1. <span data-ttu-id="b1246-117">Installare [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span><span class="sxs-lookup"><span data-stu-id="b1246-117">Install the [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span></span> <span data-ttu-id="b1246-118">Durante l'istallazione, selezionare la versione di Visual Studio da usare.</span><span class="sxs-lookup"><span data-stu-id="b1246-118">During installation, select the version of Visual Studio to use.</span></span>

2. <span data-ttu-id="b1246-119">Da Visual Studio 2015, selezionare __Analizza__ > __Portability Analyzer Settings__ (Impostazioni analizzatore portabilità) e assicurarsi che __4.5__ sia selezionato nella sezione __Mono__.</span><span class="sxs-lookup"><span data-stu-id="b1246-119">From Visual Studio 2015, select __Analyze__ > __Portability Analyzer Settings__, and make sure that __4.5__ is checked in the __Mono__ section.</span></span>

    ![4.5 selezionato nella sezione Mono per le impostazioni di analisi](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    <span data-ttu-id="b1246-121">Selezionare __OK__ per salvare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="b1246-121">Select __OK__ to save the configuration.</span></span>

3. <span data-ttu-id="b1246-122">Selezionare __Analizza__ > __Analyze Assembly Portability__ (Analizza portabilità assembly).</span><span class="sxs-lookup"><span data-stu-id="b1246-122">Select __Analyze__ > __Analyze Assembly Portability__.</span></span> <span data-ttu-id="b1246-123">Selezionare l'assembly che contiene la soluzione e quindi selezionare __Apri__ per iniziare l'analisi.</span><span class="sxs-lookup"><span data-stu-id="b1246-123">Select the assembly that contains your solution, and then select __Open__ to begin analysis.</span></span>

4. <span data-ttu-id="b1246-124">Una volta completata l'analisi, selezionare __Analizza__ > __View analysis reports__ (Visualizza rapporti di analisi).</span><span class="sxs-lookup"><span data-stu-id="b1246-124">Once analysis is complete, select __Analyze__ > __View analysis reports__.</span></span> <span data-ttu-id="b1246-125">In __Portability Analysis Results__ (Risultati analisi di portabilità) selezionare __Open report__ (Apri rapporto) per aprire un rapporto.</span><span class="sxs-lookup"><span data-stu-id="b1246-125">In __Portability Analysis Results__, select __Open report__ to open a report.</span></span>

    ![Finestra di dialogo dei risultati dell'analizzatore di portabilità](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> <span data-ttu-id="b1246-127">L'analizzatore non può intercettare tutti i problemi con la soluzione.</span><span class="sxs-lookup"><span data-stu-id="b1246-127">The analyzer cannot catch every problem with your solution.</span></span> <span data-ttu-id="b1246-128">Ad esempio, un percorso di file di `c:\temp\file.txt` è considerato OK poiché Mono viene eseguito in Windows e il percorso è valido in quel contesto.</span><span class="sxs-lookup"><span data-stu-id="b1246-128">For example, a file path of `c:\temp\file.txt` is considered OK because Mono runs on Windows and the path is valid in that context.</span></span> <span data-ttu-id="b1246-129">Tuttavia, il percorso non è valido in una piattaforma Linux.</span><span class="sxs-lookup"><span data-stu-id="b1246-129">However, the path is not valid on a Linux platform.</span></span>

## <a name="manual-portability-analysis"></a><span data-ttu-id="b1246-130">Analisi di portabilità manuale</span><span class="sxs-lookup"><span data-stu-id="b1246-130">Manual portability analysis</span></span>

<span data-ttu-id="b1246-131">Eseguire un controllo manuale del codice usando le informazioni nel documento sulla [portabilità delle applicazioni (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/).</span><span class="sxs-lookup"><span data-stu-id="b1246-131">Perform a manual audit of your code using the information in the [Application Portability (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) document.</span></span>

## <a name="modify-and-build"></a><span data-ttu-id="b1246-132">Modificare e compilare</span><span class="sxs-lookup"><span data-stu-id="b1246-132">Modify and build</span></span>

<span data-ttu-id="b1246-133">È possibile continuare a usare Visual Studio per creare soluzioni di .NET per HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b1246-133">You can continue to use Visual Studio to build your .NET solutions for HDInsight.</span></span> <span data-ttu-id="b1246-134">Tuttavia, è necessario assicurarsi che il progetto sia configurato per usare .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="b1246-134">However, you must ensure that the project is configured to use .NET Framework 4.5.</span></span>

## <a name="deploy-and-test"></a><span data-ttu-id="b1246-135">Distribuire e testare</span><span class="sxs-lookup"><span data-stu-id="b1246-135">Deploy and test</span></span>

<span data-ttu-id="b1246-136">Dopo aver modificato la soluzione con i consigli forniti da .NET Portability Analyzer o da un'analisi manuale, è necessario eseguirne il test con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b1246-136">Once you have modified your solution using the recommendations from the .NET Portability Analyzer or from a manual analysis, you must test it with HDInsight.</span></span> <span data-ttu-id="b1246-137">Fare il test della soluzione in un cluster HDInsight basato su Linux può rivelare problemi meno evidenti che devono essere corretti.</span><span class="sxs-lookup"><span data-stu-id="b1246-137">Testing the solution on a Linux-based HDInsight cluster may reveal subtle problems that need to be corrected.</span></span> <span data-ttu-id="b1246-138">Si consiglia di abilitare l'accesso aggiuntivo dell'applicazione durante l'esecuzione del test.</span><span class="sxs-lookup"><span data-stu-id="b1246-138">We recommend that you enable additional logging in your application while testing it.</span></span>

<span data-ttu-id="b1246-139">Per altre informazioni sull'accesso ai log, vedere i documenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b1246-139">For more information on accessing logs, see the following documents:</span></span>

* [<span data-ttu-id="b1246-140">Accedere ai log delle applicazioni YARN in HDInsight basato su Linux</span><span class="sxs-lookup"><span data-stu-id="b1246-140">Access YARN application logs on Linux-based HDInsight</span></span>](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a><span data-ttu-id="b1246-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b1246-141">Next steps</span></span>

* <span data-ttu-id="b1246-142">[Use C# with MapReduce on HDInsight](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md) (Usare C# con MapReduce in HDInsight)</span><span class="sxs-lookup"><span data-stu-id="b1246-142">[Use C# with MapReduce on HDInsight](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)</span></span>

* [<span data-ttu-id="b1246-143">Usare le funzioni definite dall'utente C# con lo streaming Hive e Pig in Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b1246-143">Use C# user defined functions with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="b1246-144">Sviluppare topologie C# per Apache Storm in HDInsight tramite gli strumenti Hadoop per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b1246-144">Develop C# topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)