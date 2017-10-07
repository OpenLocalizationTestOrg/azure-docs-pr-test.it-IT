---
title: aaaUse .NET con Hadoop MapReduce in HDInsight basati su Linux - Azure | Documenti Microsoft
description: Informazioni su come le applicazioni .NET toouse per lo streaming MapReduce in HDInsight basati su Linux.
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
ms.openlocfilehash: 5a4e6dc1b4dafa8cc40780e3371fa4b8ba3e3d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-net-solutions-for-windows-based-hdinsight-toolinux-based-hdinsight"></a><span data-ttu-id="9212a-103">La migrazione di soluzioni .NET per HDInsight basati su Windows basato su tooLinux HDInsight</span><span class="sxs-lookup"><span data-stu-id="9212a-103">Migrate .NET solutions for Windows-based HDInsight tooLinux-based HDInsight</span></span>

<span data-ttu-id="9212a-104">Utilizzare i cluster HDInsight basati su Linux [Mono (https://mono-project.com)](https://mono-project.com) toorun le applicazioni .NET.</span><span class="sxs-lookup"><span data-stu-id="9212a-104">Linux-based HDInsight clusters use [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="9212a-105">Mono consente toouse di componenti .NET, ad esempio applicazioni MapReduce con HDInsight basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="9212a-105">Mono allows you toouse .NET components such as MapReduce applications with Linux-based HDInsight.</span></span> <span data-ttu-id="9212a-106">In questo documento, illustrate le modalità di creazione di soluzioni .NET toomigrate per toowork cluster HDInsight basati su Windows con Mono in HDInsight basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="9212a-106">In this document, learn how toomigrate .NET solutions created for Windows-based HDInsight clusters toowork with Mono on Linux-based HDInsight.</span></span>

## <a name="mono-compatibility-with-net"></a><span data-ttu-id="9212a-107">Compatibilità Mono con .NET</span><span class="sxs-lookup"><span data-stu-id="9212a-107">Mono compatibility with .NET</span></span>

<span data-ttu-id="9212a-108">La versione Mono 4.2.1 è inclusa nella versione 3.5 di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9212a-108">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="9212a-109">Per ulteriori informazioni sulla versione di hello di Mono incluso in HDInsight, vedere [versioni dei componenti di HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="9212a-109">For more information on hello version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="9212a-110">tooinstall una versione specifica di Mono, vedere hello [installazione o aggiornamento Mono](hdinsight-hadoop-install-mono.md) documento.</span><span class="sxs-lookup"><span data-stu-id="9212a-110">tooinstall a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="9212a-111">Per informazioni dettagliate sulla compatibilità tra .NET e Mono, vedere hello [compatibilità Mono (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) documento.</span><span class="sxs-lookup"><span data-stu-id="9212a-111">For detailed information on compatibility between Mono and .NET, see hello [Mono compatibility (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9212a-112">framework SCP.NET Hello è compatibile con Mono.</span><span class="sxs-lookup"><span data-stu-id="9212a-112">hello SCP.NET framework is compatible with Mono.</span></span> <span data-ttu-id="9212a-113">Per ulteriori informazioni sull'uso di SCP.NET con Mono, vedere [topologie toodevelop c# utilizzare Visual Studio per Apache Storm in HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="9212a-113">For more information on using SCP.NET with Mono, see [Use Visual Studio toodevelop C# topologies for Apache Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

## <a name="automated-portability-analysis"></a><span data-ttu-id="9212a-114">Analisi di portabilità automatizzata</span><span class="sxs-lookup"><span data-stu-id="9212a-114">Automated portability analysis</span></span>

<span data-ttu-id="9212a-115">Hello [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) può essere utilizzato toogenerate un report di incompatibilità tra l'applicazione e Mono.</span><span class="sxs-lookup"><span data-stu-id="9212a-115">hello [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) can be used toogenerate a report of incompatibilities between your application and Mono.</span></span> <span data-ttu-id="9212a-116">Usare l'applicazione di hello seguendo i passaggi tooconfigure hello analyzer toocheck per garantire la portabilità Mono:</span><span class="sxs-lookup"><span data-stu-id="9212a-116">Use hello following steps tooconfigure hello analyzer toocheck your application for Mono portability:</span></span>

1. <span data-ttu-id="9212a-117">Installare hello [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span><span class="sxs-lookup"><span data-stu-id="9212a-117">Install hello [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span></span> <span data-ttu-id="9212a-118">Durante l'installazione, selezionare la versione hello di Visual Studio toouse.</span><span class="sxs-lookup"><span data-stu-id="9212a-118">During installation, select hello version of Visual Studio toouse.</span></span>

2. <span data-ttu-id="9212a-119">Visual Studio 2015, selezionare __Analizza__ > __Portability Analyzer impostazioni__e assicurarsi che __4.5__ archiviazione hello __Mono__  sezione.</span><span class="sxs-lookup"><span data-stu-id="9212a-119">From Visual Studio 2015, select __Analyze__ > __Portability Analyzer Settings__, and make sure that __4.5__ is checked in hello __Mono__ section.</span></span>

    ![4.5 selezionati nella sezione Mono per le impostazioni di hello analyzer](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    <span data-ttu-id="9212a-121">Selezionare __OK__ configurazione hello toosave.</span><span class="sxs-lookup"><span data-stu-id="9212a-121">Select __OK__ toosave hello configuration.</span></span>

3. <span data-ttu-id="9212a-122">Selezionare __Analizza__ > __Analyze Assembly Portability__ (Analizza portabilità assembly).</span><span class="sxs-lookup"><span data-stu-id="9212a-122">Select __Analyze__ > __Analyze Assembly Portability__.</span></span> <span data-ttu-id="9212a-123">Selezionare l'assembly hello che contiene la soluzione, quindi __aprire__ toobegin analysis.</span><span class="sxs-lookup"><span data-stu-id="9212a-123">Select hello assembly that contains your solution, and then select __Open__ toobegin analysis.</span></span>

4. <span data-ttu-id="9212a-124">Una volta completata l'analisi, selezionare __Analizza__ > __View analysis reports__ (Visualizza rapporti di analisi).</span><span class="sxs-lookup"><span data-stu-id="9212a-124">Once analysis is complete, select __Analyze__ > __View analysis reports__.</span></span> <span data-ttu-id="9212a-125">In __risultati dell'analisi portabilità__selezionare __aprire report__ tooopen un report.</span><span class="sxs-lookup"><span data-stu-id="9212a-125">In __Portability Analysis Results__, select __Open report__ tooopen a report.</span></span>

    ![Finestra di dialogo dei risultati dell'analizzatore di portabilità](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> <span data-ttu-id="9212a-127">analizzatore Hello non può intercettare tutti i problemi con la soluzione.</span><span class="sxs-lookup"><span data-stu-id="9212a-127">hello analyzer cannot catch every problem with your solution.</span></span> <span data-ttu-id="9212a-128">Ad esempio, un percorso di file di `c:\temp\file.txt` viene considerata OK perché Mono viene eseguito in Windows e hello percorso sia valido in tale contesto.</span><span class="sxs-lookup"><span data-stu-id="9212a-128">For example, a file path of `c:\temp\file.txt` is considered OK because Mono runs on Windows and hello path is valid in that context.</span></span> <span data-ttu-id="9212a-129">Percorso hello, tuttavia, non è valido in una piattaforma Linux.</span><span class="sxs-lookup"><span data-stu-id="9212a-129">However, hello path is not valid on a Linux platform.</span></span>

## <a name="manual-portability-analysis"></a><span data-ttu-id="9212a-130">Analisi di portabilità manuale</span><span class="sxs-lookup"><span data-stu-id="9212a-130">Manual portability analysis</span></span>

<span data-ttu-id="9212a-131">Esecuzione di un controllo manuale del codice utilizzando le informazioni di hello in hello [la portabilità dell'applicazione (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) documento.</span><span class="sxs-lookup"><span data-stu-id="9212a-131">Perform a manual audit of your code using hello information in hello [Application Portability (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) document.</span></span>

## <a name="modify-and-build"></a><span data-ttu-id="9212a-132">Modificare e compilare</span><span class="sxs-lookup"><span data-stu-id="9212a-132">Modify and build</span></span>

<span data-ttu-id="9212a-133">È possibile continuare le soluzioni .NET toouse toobuild di Visual Studio per HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9212a-133">You can continue toouse Visual Studio toobuild your .NET solutions for HDInsight.</span></span> <span data-ttu-id="9212a-134">Tuttavia, è necessario assicurarsi di che tale progetto hello è configurato toouse .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="9212a-134">However, you must ensure that hello project is configured toouse .NET Framework 4.5.</span></span>

## <a name="deploy-and-test"></a><span data-ttu-id="9212a-135">Distribuire e testare</span><span class="sxs-lookup"><span data-stu-id="9212a-135">Deploy and test</span></span>

<span data-ttu-id="9212a-136">Dopo aver modificato la soluzione utilizzando hello indicazioni da hello .NET Portability Analyzer o da un'analisi manuale, è necessario eseguirne il test con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9212a-136">Once you have modified your solution using hello recommendations from hello .NET Portability Analyzer or from a manual analysis, you must test it with HDInsight.</span></span> <span data-ttu-id="9212a-137">Testare la soluzione hello in un cluster HDInsight basati su Linux può rivelare problemi complessi che necessitano di toobe corretti.</span><span class="sxs-lookup"><span data-stu-id="9212a-137">Testing hello solution on a Linux-based HDInsight cluster may reveal subtle problems that need toobe corrected.</span></span> <span data-ttu-id="9212a-138">Si consiglia di abilitare l'accesso aggiuntivo dell'applicazione durante l'esecuzione del test.</span><span class="sxs-lookup"><span data-stu-id="9212a-138">We recommend that you enable additional logging in your application while testing it.</span></span>

<span data-ttu-id="9212a-139">Per ulteriori informazioni sull'accesso ai registri, vedere hello seguenti documenti:</span><span class="sxs-lookup"><span data-stu-id="9212a-139">For more information on accessing logs, see hello following documents:</span></span>

* [<span data-ttu-id="9212a-140">Accedere ai log delle applicazioni YARN in HDInsight basato su Linux</span><span class="sxs-lookup"><span data-stu-id="9212a-140">Access YARN application logs on Linux-based HDInsight</span></span>](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a><span data-ttu-id="9212a-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9212a-141">Next steps</span></span>

* <span data-ttu-id="9212a-142">[Use C# with MapReduce on HDInsight](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md) (Usare C# con MapReduce in HDInsight)</span><span class="sxs-lookup"><span data-stu-id="9212a-142">[Use C# with MapReduce on HDInsight](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)</span></span>

* [<span data-ttu-id="9212a-143">Usare le funzioni definite dall'utente C# con lo streaming Hive e Pig in Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="9212a-143">Use C# user defined functions with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="9212a-144">Sviluppare topologie C# per Apache Storm in HDInsight tramite gli strumenti Hadoop per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9212a-144">Develop C# topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)