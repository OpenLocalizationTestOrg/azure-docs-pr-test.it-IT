---
title: topologie di Storm aaaApache con Visual Studio e Visual c# - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come le topologie di Storm toocreate in c#. Creare una topologia di conteggio parole semplice in Visual Studio utilizzando gli strumenti di hello Hadoop per Visual Studio.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 380d804f-a8c5-4b20-9762-593ec4da5a0d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/02/2017
ms.author: larryfr
ms.openlocfilehash: b3fb01a4dda144fd7fb4141e624e31e667f93753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="develop-c-topologies-for-apache-storm-by-using-hello-data-lake-tools-for-visual-studio"></a><span data-ttu-id="23f55-104">Sviluppare le topologie di c# per Apache Storm utilizzando gli strumenti di Data Lake hello per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="23f55-104">Develop C# topologies for Apache Storm by using hello Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="23f55-105">Informazioni su come toocreate una topologia c# Storm utilizzando hello Azure Data Lake (Hadoop) degli strumenti per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="23f55-105">Learn how toocreate a C# Storm topology by using hello Azure Data Lake (Hadoop) tools for Visual Studio.</span></span> <span data-ttu-id="23f55-106">Questo documento descrive fasi hello della creazione di un progetto di Storm in Visual Studio, eseguire il test in locale e distribuirlo tooan Apache Storm nel cluster HDInsight di Azure.</span><span class="sxs-lookup"><span data-stu-id="23f55-106">This document walks through hello process of creating a Storm project in Visual Studio, testing it locally, and deploying it tooan Apache Storm on Azure HDInsight cluster.</span></span>

<span data-ttu-id="23f55-107">Verrà inoltre descritto come le topologie di toocreate ibride che utilizzano componenti di c# e Java.</span><span class="sxs-lookup"><span data-stu-id="23f55-107">You also learn how toocreate hybrid topologies that use C# and Java components.</span></span>

> [!NOTE]
> <span data-ttu-id="23f55-108">Durante i passaggi di hello in questo documento si basano su un ambiente di sviluppo Windows con Visual Studio, progetto compilato hello può essere inviato tooeither un cluster HDInsight basati su Windows o di Linux.</span><span class="sxs-lookup"><span data-stu-id="23f55-108">While hello steps in this document rely on a Windows development environment with Visual Studio, hello compiled project can be submitted tooeither a Linux or Windows-based HDInsight cluster.</span></span> <span data-ttu-id="23f55-109">Solo i cluster basati su Linux creati dopo il 28 ottobre 2016 supportano le topologie SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="23f55-109">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="23f55-110">topologia toouse c# con un cluster basato su Linux, è necessario aggiornare hello pacchetto Microsoft.SCP.Net.SDK NuGet usato per il tooversion progetto 0.10.0.6 o versione successivo.</span><span class="sxs-lookup"><span data-stu-id="23f55-110">toouse a C# topology with a Linux-based cluster, you must update hello Microsoft.SCP.Net.SDK NuGet package used by your project tooversion 0.10.0.6 or later.</span></span> <span data-ttu-id="23f55-111">versione di Hello del pacchetto di hello deve corrispondere anche versione principale di hello di Storm installato in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="23f55-111">hello version of hello package must also match hello major version of Storm installed on HDInsight.</span></span>

| <span data-ttu-id="23f55-112">Versione HDInsight</span><span class="sxs-lookup"><span data-stu-id="23f55-112">HDInsight version</span></span> | <span data-ttu-id="23f55-113">Versione di Storm</span><span class="sxs-lookup"><span data-stu-id="23f55-113">Storm version</span></span> | <span data-ttu-id="23f55-114">Versione di SCP.NET</span><span class="sxs-lookup"><span data-stu-id="23f55-114">SCP.NET version</span></span> | <span data-ttu-id="23f55-115">Versione Mono predefinita</span><span class="sxs-lookup"><span data-stu-id="23f55-115">Default Mono version</span></span> |
|:-----------------:|:-------------:|:---------------:|:--------------------:|
| <span data-ttu-id="23f55-116">3.3</span><span class="sxs-lookup"><span data-stu-id="23f55-116">3.3</span></span> |<span data-ttu-id="23f55-117">0.10.x</span><span class="sxs-lookup"><span data-stu-id="23f55-117">0.10.x</span></span> |<span data-ttu-id="23f55-118">0.10.x.x</span><span class="sxs-lookup"><span data-stu-id="23f55-118">0.10.x.x</span></span></br><span data-ttu-id="23f55-119">(solo in HDInsight per Windows)</span><span class="sxs-lookup"><span data-stu-id="23f55-119">(only on Windows-based HDInsight)</span></span> | <span data-ttu-id="23f55-120">ND</span><span class="sxs-lookup"><span data-stu-id="23f55-120">NA</span></span> |
| <span data-ttu-id="23f55-121">3.4</span><span class="sxs-lookup"><span data-stu-id="23f55-121">3.4</span></span> | <span data-ttu-id="23f55-122">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="23f55-122">0.10.0.x</span></span> | <span data-ttu-id="23f55-123">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="23f55-123">0.10.0.x</span></span> | <span data-ttu-id="23f55-124">3.2.8</span><span class="sxs-lookup"><span data-stu-id="23f55-124">3.2.8</span></span> |
| <span data-ttu-id="23f55-125">3,5</span><span class="sxs-lookup"><span data-stu-id="23f55-125">3.5</span></span> | <span data-ttu-id="23f55-126">1.0.2.x</span><span class="sxs-lookup"><span data-stu-id="23f55-126">1.0.2.x</span></span> | <span data-ttu-id="23f55-127">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="23f55-127">1.0.0.x</span></span> | <span data-ttu-id="23f55-128">4.2.1</span><span class="sxs-lookup"><span data-stu-id="23f55-128">4.2.1</span></span> |
| <span data-ttu-id="23f55-129">3.6</span><span class="sxs-lookup"><span data-stu-id="23f55-129">3.6</span></span> | <span data-ttu-id="23f55-130">1.1.0.x</span><span class="sxs-lookup"><span data-stu-id="23f55-130">1.1.0.x</span></span> | <span data-ttu-id="23f55-131">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="23f55-131">1.0.0.x</span></span> | <span data-ttu-id="23f55-132">4.2.8</span><span class="sxs-lookup"><span data-stu-id="23f55-132">4.2.8</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="23f55-133">C# topologie nei cluster basati su Linux è necessario utilizzare .NET 4.5 e toorun Mono nel cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-133">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono toorun on hello HDInsight cluster.</span></span> <span data-ttu-id="23f55-134">Controllare la [compatibilità Mono](http://www.mono-project.com/docs/about-mono/compatibility/) per potenziali problemi di incompatibilità.</span><span class="sxs-lookup"><span data-stu-id="23f55-134">Check [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) for potential incompatibilities.</span></span>

## <a name="install-visual-studio"></a><span data-ttu-id="23f55-135">Installazione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="23f55-135">Install Visual Studio</span></span>

<span data-ttu-id="23f55-136">È possibile sviluppare le topologie di c# con SCP.NET utilizzando una delle seguenti versioni di Visual Studio hello:</span><span class="sxs-lookup"><span data-stu-id="23f55-136">You can develop C# topologies with SCP.NET by using one of hello following versions of Visual Studio:</span></span>

* <span data-ttu-id="23f55-137">Visual Studio 2012 con [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="23f55-137">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

* <span data-ttu-id="23f55-138">Visual Studio 2013 con [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) o [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="23f55-138">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>

* <span data-ttu-id="23f55-139">Visual Studio 2015 o [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span><span class="sxs-lookup"><span data-stu-id="23f55-139">Visual Studio 2015 or [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span></span>

* <span data-ttu-id="23f55-140">Visual Studio 2017, qualsiasi edizione</span><span class="sxs-lookup"><span data-stu-id="23f55-140">Visual Studio 2017 (any edition)</span></span>

## <a name="install-data-lake-tools-for-visual-studio"></a><span data-ttu-id="23f55-141">Installare gli strumenti Data Lake per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="23f55-141">Install Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="23f55-142">gli strumenti di Data Lake tooinstall per Visual Studio, seguire i passaggi di hello in [iniziare a usare gli strumenti di Data Lake per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="23f55-142">tooinstall Data Lake tools for Visual Studio, follow hello steps in [Get started using Data Lake tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

## <a name="install-java"></a><span data-ttu-id="23f55-143">Installare Java</span><span class="sxs-lookup"><span data-stu-id="23f55-143">Install Java</span></span>

<span data-ttu-id="23f55-144">Quando si invia una topologia di Storm da Visual Studio, SCP.NET genera un file zip che contiene le dipendenze e la topologia di hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-144">When you submit a Storm topology from Visual Studio, SCP.NET generates a zip file that contains hello topology and dependencies.</span></span> <span data-ttu-id="23f55-145">Java è toocreate utilizzati questi file, di zip perché utilizza un formato che è più compatibile con cluster basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="23f55-145">Java is used toocreate these zip files, because it uses a format that is more compatible with Linux-based clusters.</span></span>

1. <span data-ttu-id="23f55-146">Installare hello Java Developer Kit (JDK) 7 o versione successiva in ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="23f55-146">Install hello Java Developer Kit (JDK) 7 or later on your development environment.</span></span> <span data-ttu-id="23f55-147">È possibile ottenere hello Oracle JDK da [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="23f55-147">You can get hello Oracle JDK from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span> <span data-ttu-id="23f55-148">È inoltre possibile usare [altre distribuzioni Java](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="23f55-148">You can also use [other Java distributions](http://openjdk.java.net/).</span></span>

2. <span data-ttu-id="23f55-149">Hello `JAVA_HOME` directory di toohello punto deve variabile di ambiente contenente Java.</span><span class="sxs-lookup"><span data-stu-id="23f55-149">hello `JAVA_HOME` environment variable must point toohello directory that contains Java.</span></span>

3. <span data-ttu-id="23f55-150">Hello `PATH` variabile di ambiente deve includere hello `%JAVA_HOME%\bin` directory.</span><span class="sxs-lookup"><span data-stu-id="23f55-150">hello `PATH` environment variable must include hello `%JAVA_HOME%\bin` directory.</span></span>

<span data-ttu-id="23f55-151">È possibile utilizzare hello seguente c# console application tooverify Java e hello JDK siano installati correttamente:</span><span class="sxs-lookup"><span data-stu-id="23f55-151">You can use hello following C# console application tooverify that Java and hello JDK are correctly installed:</span></span>

```csharp
using System;
using System.IO;
namespace ConsoleApplication2
{
   class Program
   {
       static void Main(string[] args)
       {
           string javaHome = Environment.GetEnvironmentVariable(“JAVA_HOME”);
           if (!string.IsNullOrEmpty(javaHome))
           {
               string jarExe = Path.Combine(javaHome + @”\bin”, “jar.exe”);
               if (File.Exists(jarExe))
               {
                   Console.WriteLine(“JAVA Is Installed properly”);
                    return;
               }
               else
               {
                   Console.WriteLine(“A valid JAVA JDK is not found. Looks like JRE is installed instead of JDK.”);
               }
           }
           else
           {
             Console.WriteLine(“A valid JAVA JDK is not found. JAVA_HOME environment variable is not set.”);
           }
       }  
   }
}
```

## <a name="storm-templates"></a><span data-ttu-id="23f55-152">Modelli Storm</span><span class="sxs-lookup"><span data-stu-id="23f55-152">Storm templates</span></span>

<span data-ttu-id="23f55-153">gli strumenti di Data Lake Hello per Visual Studio forniscono hello seguenti modelli:</span><span class="sxs-lookup"><span data-stu-id="23f55-153">hello Data Lake tools for Visual Studio provide hello following templates:</span></span>

| <span data-ttu-id="23f55-154">Tipo di progetto</span><span class="sxs-lookup"><span data-stu-id="23f55-154">Project type</span></span> | <span data-ttu-id="23f55-155">Dimostra</span><span class="sxs-lookup"><span data-stu-id="23f55-155">Demonstrates</span></span> |
| --- | --- |
| <span data-ttu-id="23f55-156">Applicazione Storm</span><span class="sxs-lookup"><span data-stu-id="23f55-156">Storm Application</span></span> |<span data-ttu-id="23f55-157">Un progetto di topologia Storm vuoto</span><span class="sxs-lookup"><span data-stu-id="23f55-157">An empty Storm topology project.</span></span> |
| <span data-ttu-id="23f55-158">Esempio di writer SQL di Azure per Storm</span><span class="sxs-lookup"><span data-stu-id="23f55-158">Storm Azure SQL Writer Sample</span></span> |<span data-ttu-id="23f55-159">Come toowrite tooAzure Database SQL.</span><span class="sxs-lookup"><span data-stu-id="23f55-159">How toowrite tooAzure SQL Database.</span></span> |
| <span data-ttu-id="23f55-160">Esempio di reader Storm per Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="23f55-160">Storm Azure Cosmos DB Reader Sample</span></span> |<span data-ttu-id="23f55-161">Come tooread dal database di Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="23f55-161">How tooread from Azure Cosmos DB.</span></span> |
| <span data-ttu-id="23f55-162">Esempio di writer Storm per Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="23f55-162">Storm Azure Cosmos DB Writer Sample</span></span> |<span data-ttu-id="23f55-163">Come toowrite tooAzure DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="23f55-163">How toowrite tooAzure Cosmos DB.</span></span> |
| <span data-ttu-id="23f55-164">Esempio di lettore EventHub per Storm</span><span class="sxs-lookup"><span data-stu-id="23f55-164">Storm EventHub Reader Sample</span></span> |<span data-ttu-id="23f55-165">Come tooread dagli hub di eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="23f55-165">How tooread from Azure Event Hubs.</span></span> |
| <span data-ttu-id="23f55-166">Esempio di writer EventHub per Storm</span><span class="sxs-lookup"><span data-stu-id="23f55-166">Storm EventHub Writer Sample</span></span> |<span data-ttu-id="23f55-167">Come toowrite tooAzure hub eventi.</span><span class="sxs-lookup"><span data-stu-id="23f55-167">How toowrite tooAzure Event Hubs.</span></span> |
| <span data-ttu-id="23f55-168">Esempio di lettore HBase per Storm</span><span class="sxs-lookup"><span data-stu-id="23f55-168">Storm HBase Reader Sample</span></span> |<span data-ttu-id="23f55-169">Come cluster tooread da HBase in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="23f55-169">How tooread from HBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="23f55-170">Esempio di writer HBase per Storm</span><span class="sxs-lookup"><span data-stu-id="23f55-170">Storm HBase Writer Sample</span></span> |<span data-ttu-id="23f55-171">Come cluster tooHBase toowrite in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="23f55-171">How toowrite tooHBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="23f55-172">Esempio ibrido di Storm</span><span class="sxs-lookup"><span data-stu-id="23f55-172">Storm Hybrid Sample</span></span> |<span data-ttu-id="23f55-173">Come toouse un componente di Java.</span><span class="sxs-lookup"><span data-stu-id="23f55-173">How toouse a Java component.</span></span> |
| <span data-ttu-id="23f55-174">Esempio di Storm</span><span class="sxs-lookup"><span data-stu-id="23f55-174">Storm Sample</span></span> |<span data-ttu-id="23f55-175">Topologia di conteggio parole di base</span><span class="sxs-lookup"><span data-stu-id="23f55-175">A basic word count topology.</span></span> |

> [!WARNING]
> <span data-ttu-id="23f55-176">Non tutti i modelli funzionano con HDInsight basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="23f55-176">Not all templates will work with Linux-based HDInsight.</span></span> <span data-ttu-id="23f55-177">Pacchetti NuGet usati dai modelli hello potrebbero non essere compatibili con Mono.</span><span class="sxs-lookup"><span data-stu-id="23f55-177">Nuget packages used by hello templates may not be compatible with Mono.</span></span> <span data-ttu-id="23f55-178">Controllare hello [compatibilità Mono](http://www.mono-project.com/docs/about-mono/compatibility/) dei documenti e utilizzare hello [.NET Portability Analyzer](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) tooidentify potenziali problemi.</span><span class="sxs-lookup"><span data-stu-id="23f55-178">Check hello [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document and use hello [.NET Portability Analyzer](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) tooidentify potential problems.</span></span>

<span data-ttu-id="23f55-179">Nei passaggi hello in questo documento, utilizzare hello base tempesta applicazione progetto tipo toocreate una topologia.</span><span class="sxs-lookup"><span data-stu-id="23f55-179">In hello steps in this document, you use hello basic Storm Application project type toocreate a topology.</span></span>

### <a name="hbase-templates-notes"></a><span data-ttu-id="23f55-180">Note sui modelli HBase</span><span class="sxs-lookup"><span data-stu-id="23f55-180">HBase templates notes</span></span>

<span data-ttu-id="23f55-181">Hello HBase lettore e modelli di writer utilizzano hello l'API REST HBase non hello API Java HBase, toocommunicate con un HBase nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="23f55-181">hello HBase reader and writer templates use hello HBase REST API, not hello HBase Java API, toocommunicate with an HBase on HDInsight cluster.</span></span>

### <a name="eventhub-templates-notes"></a><span data-ttu-id="23f55-182">Note sui modelli EventHub</span><span class="sxs-lookup"><span data-stu-id="23f55-182">EventHub templates notes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="23f55-183">Hello basati su Java EventHub spout componente incluso con hello modello EventHub lettore potrebbe non funzionare con Storm in HDInsight 3.5 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="23f55-183">hello Java-based EventHub spout component included with hello EventHub Reader template may not work with Storm on HDInsight version 3.5 or later.</span></span> <span data-ttu-id="23f55-184">Una versione aggiornata di questo componente è disponibile in [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span><span class="sxs-lookup"><span data-stu-id="23f55-184">An updated version of this component is available at [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span></span>

<span data-ttu-id="23f55-185">Per una topologia di esempio che usa questo componente e funziona con Storm in HDInsight 3.5, vedere [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="23f55-185">For an example topology that uses this component and works with Storm on HDInsight 3.5, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

## <a name="create-a-c-topology"></a><span data-ttu-id="23f55-186">Creare una topologia C#</span><span class="sxs-lookup"><span data-stu-id="23f55-186">Create a C# topology</span></span>

1. <span data-ttu-id="23f55-187">Aprire Visual Studio, selezionare **File** > **Nuovo** e quindi **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="23f55-187">Open Visual Studio, select **File** > **New**, and then select **Project**.</span></span>

2. <span data-ttu-id="23f55-188">Da hello **nuovo progetto** finestra, espandere **installato** > **modelli**e selezionare **Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="23f55-188">From hello **New Project** window, expand **Installed** > **Templates**, and select **Azure Data Lake**.</span></span> <span data-ttu-id="23f55-189">Selezionare nell'elenco dei modelli di hello **Storm applicazione**.</span><span class="sxs-lookup"><span data-stu-id="23f55-189">From hello list of templates, select **Storm Application**.</span></span> <span data-ttu-id="23f55-190">In basso hello hello, immettere **WordCount** come nome di hello dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-190">At hello bottom of hello screen, enter **WordCount** as hello name of hello application.</span></span>

    ![Screenshot della finestra Nuovo progetto](./media/hdinsight-storm-develop-csharp-visual-studio-topology/new-project.png)

3. <span data-ttu-id="23f55-192">Dopo aver creato il progetto di hello, è necessario avere i seguenti file hello:</span><span class="sxs-lookup"><span data-stu-id="23f55-192">After you have created hello project, you should have hello following files:</span></span>

   * <span data-ttu-id="23f55-193">**Program.cs**: questo file definisce topologia hello per il progetto.</span><span class="sxs-lookup"><span data-stu-id="23f55-193">**Program.cs**: This file defines hello topology for your project.</span></span> <span data-ttu-id="23f55-194">Per impostazione predefinita viene creata una topologia predefinita costituita da uno spout e da un bolt.</span><span class="sxs-lookup"><span data-stu-id="23f55-194">A default topology that consists of one spout and one bolt is created by default.</span></span>

   * <span data-ttu-id="23f55-195">**Spout.cs**: spout di esempio che genera numeri casuali.</span><span class="sxs-lookup"><span data-stu-id="23f55-195">**Spout.cs**: An example spout that emits random numbers.</span></span>

   * <span data-ttu-id="23f55-196">**BOLT.cs**: un fulmine di esempio che mantiene un conteggio dei numeri generati da beccuccio hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-196">**Bolt.cs**: An example bolt that keeps a count of numbers emitted by hello spout.</span></span>

     <span data-ttu-id="23f55-197">Quando si crea il progetto di hello, download NuGet hello più recente [SCP.NET pacchetto](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span><span class="sxs-lookup"><span data-stu-id="23f55-197">When you create hello project, NuGet downloads hello latest [SCP.NET package](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span></span>

     [!INCLUDE [scp.net version important](../../includes/hdinsight-storm-scpdotnet-version.md)]

### <a name="implement-hello-spout"></a><span data-ttu-id="23f55-198">Beccuccio hello implementare</span><span class="sxs-lookup"><span data-stu-id="23f55-198">Implement hello spout</span></span>

1. <span data-ttu-id="23f55-199">Aprire **Spout.cs**.</span><span class="sxs-lookup"><span data-stu-id="23f55-199">Open **Spout.cs**.</span></span> <span data-ttu-id="23f55-200">Spouts sono dati tooread utilizzato in una topologia da un'origine esterna.</span><span class="sxs-lookup"><span data-stu-id="23f55-200">Spouts are used tooread data in a topology from an external source.</span></span> <span data-ttu-id="23f55-201">componenti principali di Hello per beccuccio sono:</span><span class="sxs-lookup"><span data-stu-id="23f55-201">hello main components for a spout are:</span></span>

   * <span data-ttu-id="23f55-202">**NextTuple**: chiamato da Storm beccuccio hello è consentito tooemit nuove Tuple.</span><span class="sxs-lookup"><span data-stu-id="23f55-202">**NextTuple**: Called by Storm when hello spout is allowed tooemit new tuples.</span></span>

   * <span data-ttu-id="23f55-203">**ACK** (solo per topologia transazionale): gestisce i riconoscimenti da altri componenti nella topologia hello per le tuple inviate da beccuccio hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-203">**Ack** (transactional topology only): Handles acknowledgements initiated by other components in hello topology for tuples sent from hello spout.</span></span> <span data-ttu-id="23f55-204">Una conferma di una tupla consente beccuccio hello di sapere che è stata elaborata correttamente dai componenti a valle.</span><span class="sxs-lookup"><span data-stu-id="23f55-204">Acknowledging a tuple lets hello spout know that it was processed successfully by downstream components.</span></span>

   * <span data-ttu-id="23f55-205">**Esito negativo** (solo per topologia transazionale): gestisce le tuple che sono non è riuscita l'elaborazione di altri componenti della topologia hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-205">**Fail** (transactional topology only): Handles tuples that are fail-processing other components in hello topology.</span></span> <span data-ttu-id="23f55-206">Implementazione di un metodo Fail consente toore-emit hello tupla in modo che possa essere elaborato nuovamente.</span><span class="sxs-lookup"><span data-stu-id="23f55-206">Implementing a Fail method allows you toore-emit hello tuple so that it can be processed again.</span></span>

2. <span data-ttu-id="23f55-207">Sostituire il contenuto di hello di hello **Spout** classe con hello dopo il testo.</span><span class="sxs-lookup"><span data-stu-id="23f55-207">Replace hello contents of hello **Spout** class with hello following text.</span></span> <span data-ttu-id="23f55-208">Questo beccuccio genera in modo casuale una frase nella topologia hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-208">This spout randomly emits a sentence into hello topology.</span></span>

    ```csharp
    private Context ctx;
    private Random r = new Random();
    string[] sentences = new string[] {
        "hello cow jumped over hello moon",
        "an apple a day keeps hello doctor away",
        "four score and seven years ago",
        "snow white and hello seven dwarfs",
        "i am at two with nature"
    };

    public Spout(Context ctx)
    {
        // Set hello instance context
        this.ctx = ctx;

        Context.Logger.Info("Generator constructor called");

        // Declare Output schema
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // hello schema for hello default output stream is
        // a tuple that contains a string field
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(null, outputSchema));
    }

    // Get an instance of hello spout
    public static Spout Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Spout(ctx);
    }

    public void NextTuple(Dictionary<string, Object> parms)
    {
        Context.Logger.Info("NextTuple enter");
        // hello sentence toobe emitted
        string sentence;

        // Get a random sentence
        sentence = sentences[r.Next(0, sentences.Length - 1)];
        Context.Logger.Info("Emit: {0}", sentence);
        // Emit it
        this.ctx.Emit(new Values(sentence));

        Context.Logger.Info("NextTuple exit");
    }

    public void Ack(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }
    ```

### <a name="implement-hello-bolts"></a><span data-ttu-id="23f55-209">Implementare bulloni hello</span><span class="sxs-lookup"><span data-stu-id="23f55-209">Implement hello bolts</span></span>

1. <span data-ttu-id="23f55-210">Eliminare hello esistente **Bolt.cs** file dal progetto hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-210">Delete hello existing **Bolt.cs** file from hello project.</span></span>

2. <span data-ttu-id="23f55-211">In **Esplora**, fare clic sul progetto hello e selezionare **Aggiungi** > **nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="23f55-211">In **Solution Explorer**, right-click hello project, and select **Add** > **New item**.</span></span> <span data-ttu-id="23f55-212">Selezionare nell'elenco hello **Storm fulmine**e immettere **Splitter.cs** come nome hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-212">From hello list, select **Storm Bolt**, and enter **Splitter.cs** as hello name.</span></span> <span data-ttu-id="23f55-213">Ripetere questo processo toocreate denominato di un fulmine secondo **Counter.cs**.</span><span class="sxs-lookup"><span data-stu-id="23f55-213">Repeat this process toocreate a second bolt named **Counter.cs**.</span></span>

   * <span data-ttu-id="23f55-214">**Splitter.cs**: implementa un bolt che divide le frasi in singole parole e crea un nuovo flusso di parole.</span><span class="sxs-lookup"><span data-stu-id="23f55-214">**Splitter.cs**: Implements a bolt that splits sentences into individual words, and emits a new stream of words.</span></span>

   * <span data-ttu-id="23f55-215">**Counter.cs**: implementa un fulmine che il conteggio di ogni parola e genera un nuovo flusso di parole e conteggio hello per ogni parola.</span><span class="sxs-lookup"><span data-stu-id="23f55-215">**Counter.cs**: Implements a bolt that counts each word, and emits a new stream of words and hello count for each word.</span></span>

     > [!NOTE]
     > <span data-ttu-id="23f55-216">Questi dadi leggere e scrivere toostreams, ma è inoltre possibile utilizzare un toocommunicate fulmine con origini, ad esempio un database o un servizio.</span><span class="sxs-lookup"><span data-stu-id="23f55-216">These bolts read and write toostreams, but you can also use a bolt toocommunicate with sources such as a database or service.</span></span>

3. <span data-ttu-id="23f55-217">Aprire **Splitter.cs**.</span><span class="sxs-lookup"><span data-stu-id="23f55-217">Open **Splitter.cs**.</span></span> <span data-ttu-id="23f55-218">Per impostazione predefinita, dispone soltanto del metodo **Execute**.</span><span class="sxs-lookup"><span data-stu-id="23f55-218">It has only one method by default: **Execute**.</span></span> <span data-ttu-id="23f55-219">metodo Execute Hello viene chiamato quando fulmine hello riceve una tupla per l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="23f55-219">hello Execute method is called when hello bolt receives a tuple for processing.</span></span> <span data-ttu-id="23f55-220">È possibile leggere ed elaborare tuple in ingresso e generare tuple in uscita.</span><span class="sxs-lookup"><span data-stu-id="23f55-220">Here, you can read and process incoming tuples, and emit outbound tuples.</span></span>

4. <span data-ttu-id="23f55-221">Sostituire il contenuto di hello di hello **divisione** classe con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="23f55-221">Replace hello contents of hello **Splitter** class with hello following code:</span></span>

    ```csharp
    private Context ctx;

    // Constructor
    public Splitter(Context ctx)
    {
        Context.Logger.Info("Splitter constructor called");
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // Input contains a tuple with a string field (hello sentence)
        inputSchema.Add("default", new List<Type>() { typeof(string) });
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // Outbound contains a tuple with a string field (hello word)
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance of hello bolt
    public static Splitter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Splitter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello sentence from hello tuple
        string sentence = tuple.GetString(0);
        // Split at space characters
        foreach (string word in sentence.Split(' '))
        {
            Context.Logger.Info("Emit: {0}", word);
            //Emit each word
            this.ctx.Emit(new Values(word));
        }

        Context.Logger.Info("Execute exit");
    }
    ```

5. <span data-ttu-id="23f55-222">Aprire **Counter.cs**e sostituire il contenuto di classe hello con hello seguente:</span><span class="sxs-lookup"><span data-stu-id="23f55-222">Open **Counter.cs**, and replace hello class contents with hello following:</span></span>

    ```csharp
    private Context ctx;

    // Dictionary for holding words and counts
    private Dictionary<string, int> counts = new Dictionary<string, int>();

    // Constructor
    public Counter(Context ctx)
    {
        Context.Logger.Info("Counter constructor called");
        // Set instance context
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string field - hello word
        inputSchema.Add("default", new List<Type>() { typeof(string) });

        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string and integer field - hello word and hello word count
        outputSchema.Add("default", new List<Type>() { typeof(string), typeof(int) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance
    public static Counter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Counter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello word from hello tuple
        string word = tuple.GetString(0);
        // Do we already have an entry for hello word in hello dictionary?
        // If no, create one with a count of 0
        int count = counts.ContainsKey(word) ? counts[word] : 0;
        // Increment hello count
        count++;
        // Update hello count in hello dictionary
        counts[word] = count;

        Context.Logger.Info("Emit: {0}, count: {1}", word, count);
        // Emit hello word and count information
        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new List<SCPTuple> { tuple }, new Values(word, count));
        Context.Logger.Info("Execute exit");
    }
    ```

### <a name="define-hello-topology"></a><span data-ttu-id="23f55-223">Definire la topologia hello</span><span class="sxs-lookup"><span data-stu-id="23f55-223">Define hello topology</span></span>

<span data-ttu-id="23f55-224">Spouts e le viti vengono disposte in un grafico, che definisce il flusso dei dati hello tra componenti.</span><span class="sxs-lookup"><span data-stu-id="23f55-224">Spouts and bolts are arranged in a graph, which defines how hello data flows between components.</span></span> <span data-ttu-id="23f55-225">Per questa topologia, hello è come segue:</span><span class="sxs-lookup"><span data-stu-id="23f55-225">For this topology, hello graph is as follows:</span></span>

![Diagramma della disposizione degli elementi](./media/hdinsight-storm-develop-csharp-visual-studio-topology/wordcount-topology.png)

<span data-ttu-id="23f55-227">Frasi vengono emessi da beccuccio hello e sono distribuite tooinstances di fulmine divisione hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-227">Sentences are emitted from hello spout, and are distributed tooinstances of hello Splitter bolt.</span></span> <span data-ttu-id="23f55-228">fulmine divisione Hello interrompe frasi hello in parole, che sono distribuite toohello fulmine di contatore.</span><span class="sxs-lookup"><span data-stu-id="23f55-228">hello Splitter bolt breaks hello sentences into words, which are distributed toohello Counter bolt.</span></span>

<span data-ttu-id="23f55-229">Poiché il conteggio di word viene mantenuto localmente nell'istanza di contatore hello, si desidera assicurarsi che le parole specifiche flusso toohello toomake stessa istanza di contatore fulmine.</span><span class="sxs-lookup"><span data-stu-id="23f55-229">Because word count is held locally in hello Counter instance, we want toomake sure that specific words flow toohello same Counter bolt instance.</span></span> <span data-ttu-id="23f55-230">Ogni istanza tiene traccia di una parola specifica.</span><span class="sxs-lookup"><span data-stu-id="23f55-230">Each instance keeps track of specific words.</span></span> <span data-ttu-id="23f55-231">Poiché fulmine divisione hello non mantiene lo stato, effettivamente non è importante che l'istanza della barra di divisione hello riceve quali frase.</span><span class="sxs-lookup"><span data-stu-id="23f55-231">Since hello Splitter bolt maintains no state, it really doesn't matter which instance of hello splitter receives which sentence.</span></span>

<span data-ttu-id="23f55-232">Aprire **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="23f55-232">Open **Program.cs**.</span></span> <span data-ttu-id="23f55-233">metodo importante Hello è **GetTopologyBuilder**, ovvero topologia hello toodefine utilizzati che viene inviato tooStorm.</span><span class="sxs-lookup"><span data-stu-id="23f55-233">hello important method is **GetTopologyBuilder**, which is used toodefine hello topology that is submitted tooStorm.</span></span> <span data-ttu-id="23f55-234">Sostituire il contenuto di hello di **GetTopologyBuilder** con hello seguente topologia di hello tooimplement codice descritta in precedenza:</span><span class="sxs-lookup"><span data-stu-id="23f55-234">Replace hello contents of **GetTopologyBuilder** with hello following code tooimplement hello topology described previously:</span></span>

```csharp
// Create a new topology named 'WordCount'
TopologyBuilder topologyBuilder = new TopologyBuilder("WordCount" + DateTime.Now.ToString("yyyyMMddHHmmss"));

// Add hello spout toohello topology.
// Name hello component 'sentences'
// Name hello field that is emitted as 'sentence'
topologyBuilder.SetSpout(
    "sentences",
    Spout.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"sentence"}}
    },
    1);
// Add hello splitter bolt toohello topology.
// Name hello component 'splitter'
// Name hello field that is emitted 'word'
// Use suffleGrouping toodistribute incoming tuples
//   from hello 'sentences' spout across instances
//   of hello splitter
topologyBuilder.SetBolt(
    "splitter",
    Splitter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word"}}
    },
    1).shuffleGrouping("sentences");

// Add hello counter bolt toohello topology.
// Name hello component 'counter'
// Name hello fields that are emitted 'word' and 'count'
// Use fieldsGrouping tooensure that tuples are routed
//   toocounter instances based on hello contents of field
//   position 0 (hello word). This could also have been
//   List<string>(){"word"}.
//   This ensures that hello word 'jumped', for example, will always
//   go toohello same instance
topologyBuilder.SetBolt(
    "counter",
    Counter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word", "count"}}
    },
    1).fieldsGrouping("splitter", new List<int>() { 0 });

// Add topology config
topologyBuilder.SetTopologyConfig(new Dictionary<string, string>()
{
    {"topology.kryo.register","[\"[B\"]"}
});

return topologyBuilder;
```

## <a name="submit-hello-topology"></a><span data-ttu-id="23f55-235">Inviare hello topologia</span><span class="sxs-lookup"><span data-stu-id="23f55-235">Submit hello topology</span></span>

1. <span data-ttu-id="23f55-236">In **Esplora**, fare clic sul progetto hello e selezionare **inviare tooStorm in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="23f55-236">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="23f55-237">Se richiesto, immettere le credenziali di hello per la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="23f55-237">If prompted, enter hello credentials for your Azure subscription.</span></span> <span data-ttu-id="23f55-238">Se si dispone di più di una sottoscrizione, accedere toohello uno che contiene l'elevato numero di cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="23f55-238">If you have more than one subscription, sign in toohello one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="23f55-239">Selezionare l'elevato numero di cluster HDInsight da hello **Cluster Storm** elenco a discesa e quindi selezionare **Invia**.</span><span class="sxs-lookup"><span data-stu-id="23f55-239">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="23f55-240">È possibile monitorare se invio hello ha esito positivo tramite hello **Output** finestra.</span><span class="sxs-lookup"><span data-stu-id="23f55-240">You can monitor if hello submission is successful by using hello **Output** window.</span></span>

3. <span data-ttu-id="23f55-241">Quando la topologia hello è stata inviata correttamente, hello **Storm topologie** per cluster hello devono essere visualizzati.</span><span class="sxs-lookup"><span data-stu-id="23f55-241">When hello topology has been successfully submitted, hello **Storm Topologies** for hello cluster should appear.</span></span> <span data-ttu-id="23f55-242">Seleziona hello **WordCount** topologia da hello elenco tooview informazioni hello in esecuzione sulla topologia.</span><span class="sxs-lookup"><span data-stu-id="23f55-242">Select hello **WordCount** topology from hello list tooview information about hello running topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="23f55-243">È inoltre possibile visualizzare le **topologie Storm**  da **Esplora Server**.</span><span class="sxs-lookup"><span data-stu-id="23f55-243">You can also view **Storm Topologies** from **Server Explorer**.</span></span> <span data-ttu-id="23f55-244">Espandere **Azure** > **HDInsight**, fare clic con il pulsante destro del mouse sul cluster Storm in HDInsight e quindi selezionare **Visualizza topologie Storm**.</span><span class="sxs-lookup"><span data-stu-id="23f55-244">Expand **Azure** > **HDInsight**, right-click a Storm on HDInsight cluster, and then select **View Storm Topologies**.</span></span>

    <span data-ttu-id="23f55-245">tooview informazioni sui componenti di hello nella topologia hello, fare doppio clic sul componente hello nel diagramma hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-245">tooview information about hello components in hello topology, double-click hello component in hello diagram.</span></span>

4. <span data-ttu-id="23f55-246">Da hello **topologia riepilogo** consente di visualizzare, fare clic su **Kill** topologia hello toostop.</span><span class="sxs-lookup"><span data-stu-id="23f55-246">From hello **Topology Summary** view, click **Kill** toostop hello topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="23f55-247">Topologie di Storm continuare toorun fino a quando non sono disattivate o hello cluster verrà eliminato.</span><span class="sxs-lookup"><span data-stu-id="23f55-247">Storm topologies continue toorun until they are deactivated, or hello cluster is deleted.</span></span>

## <a name="transactional-topology"></a><span data-ttu-id="23f55-248">Topologia transazionale</span><span class="sxs-lookup"><span data-stu-id="23f55-248">Transactional topology</span></span>

<span data-ttu-id="23f55-249">topologia di Hello precedente è non transazionale.</span><span class="sxs-lookup"><span data-stu-id="23f55-249">hello previous topology is non-transactional.</span></span> <span data-ttu-id="23f55-250">i componenti di Hello nella topologia hello non implementano messaggi tooreplaying funzionalità.</span><span class="sxs-lookup"><span data-stu-id="23f55-250">hello components in hello topology do not implement functionality tooreplaying messages.</span></span> <span data-ttu-id="23f55-251">Per un esempio di una topologia transazionale, creare un progetto e selezionare **esempio Storm** come tipo di progetto hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-251">For an example of a transactional topology, create a project and select **Storm Sample** as hello project type.</span></span>

<span data-ttu-id="23f55-252">Topologie transazionale implementano hello toosupport riproduzione di dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="23f55-252">Transactional topologies implement hello following toosupport replay of data:</span></span>

* <span data-ttu-id="23f55-253">**La memorizzazione nella cache di metadati**: beccuccio hello deve archiviare i metadati relativi a dati hello generati, in modo che i dati di hello possono essere recuperati e generati nuovamente se si verifica un errore.</span><span class="sxs-lookup"><span data-stu-id="23f55-253">**Metadata caching**: hello spout must store metadata about hello data emitted, so that hello data can be retrieved and emitted again if a failure occurs.</span></span> <span data-ttu-id="23f55-254">Poiché i dati di hello generati dall'esempio hello sono ridotta, dati non elaborati hello ogni tupla viene archiviati in un dizionario per la riproduzione.</span><span class="sxs-lookup"><span data-stu-id="23f55-254">Because hello data emitted by hello sample is small, hello raw data for each tuple is stored in a dictionary for replay.</span></span>

* <span data-ttu-id="23f55-255">**ACK**: ogni fulmine nella topologia hello può chiamare `this.ctx.Ack(tuple)` tooacknowledge che è stato elaborato correttamente una tupla.</span><span class="sxs-lookup"><span data-stu-id="23f55-255">**Ack**: Each bolt in hello topology can call `this.ctx.Ack(tuple)` tooacknowledge that it has successfully processed a tuple.</span></span> <span data-ttu-id="23f55-256">Quando tutti i bulloni tupla hello riconosciuto, hello `Ack` di beccuccio hello viene richiamato.</span><span class="sxs-lookup"><span data-stu-id="23f55-256">When all bolts have acked hello tuple, hello `Ack` method of hello spout is invoked.</span></span> <span data-ttu-id="23f55-257">Hello `Ack` metodo consente hello beccuccio tooremove i dati è stato memorizzato nella cache per la riproduzione.</span><span class="sxs-lookup"><span data-stu-id="23f55-257">hello `Ack` method allows hello spout tooremove data that was cached for replay.</span></span>

* <span data-ttu-id="23f55-258">**Esito negativo**: ogni fulmine può chiamare `this.ctx.Fail(tuple)` tooindicate che l'elaborazione non è riuscita per una tupla.</span><span class="sxs-lookup"><span data-stu-id="23f55-258">**Fail**: Each bolt can call `this.ctx.Fail(tuple)` tooindicate that processing has failed for a tuple.</span></span> <span data-ttu-id="23f55-259">Errore Hello propaga toohello `Fail` metodo beccuccio hello, in cui la tupla hello possa essere riprodotta utilizzando metadati memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="23f55-259">hello failure propagates toohello `Fail` method of hello spout, where hello tuple can be replayed by using cached metadata.</span></span>

* <span data-ttu-id="23f55-260">**ID sequenza**: quando si genera una tupla, è possibile specificare un ID sequenza univoco.</span><span class="sxs-lookup"><span data-stu-id="23f55-260">**Sequence ID**: When emitting a tuple, a unique sequence ID can be specified.</span></span> <span data-ttu-id="23f55-261">Questo valore identifica hello tupla per l'elaborazione di riproduzione (Ack e hanno esito negativo).</span><span class="sxs-lookup"><span data-stu-id="23f55-261">This value identifies hello tuple for replay (Ack and Fail) processing.</span></span> <span data-ttu-id="23f55-262">Ad esempio, hello beccuccio in hello **esempio Storm** seguente hello utilizzato in project per la creazione dei dati:</span><span class="sxs-lookup"><span data-stu-id="23f55-262">For example, hello spout in hello **Storm Sample** project uses hello following when emitting data:</span></span>

        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), lastSeqId);

    <span data-ttu-id="23f55-263">Questo codice genera una tupla che contiene un flusso predefinito toohello frase, con valore di ID sequenza hello contenuti in **lastSeqId**.</span><span class="sxs-lookup"><span data-stu-id="23f55-263">This code emits a tuple that contains a sentence toohello default stream, with hello sequence ID value contained in **lastSeqId**.</span></span> <span data-ttu-id="23f55-264">Ai fini di questo esempio, **lastSeqId** viene incrementato per ogni tupla generata.</span><span class="sxs-lookup"><span data-stu-id="23f55-264">For this example, **lastSeqId** is incremented for every tuple emitted.</span></span>

<span data-ttu-id="23f55-265">Come dimostrato nel hello **esempio Storm** del progetto, la transazione o meno un componente può essere impostata in fase di esecuzione, in base alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="23f55-265">As demonstrated in hello **Storm Sample** project, whether a component is transactional can be set at runtime, based on configuration.</span></span>

## <a name="hybrid-topology-with-c-and-java"></a><span data-ttu-id="23f55-266">Topologia ibrida con C# e Java</span><span class="sxs-lookup"><span data-stu-id="23f55-266">Hybrid topology with C# and Java</span></span>

<span data-ttu-id="23f55-267">È inoltre possibile utilizzare strumenti di Data Lake per Visual Studio toocreate ibrida le topologie, in cui alcuni componenti sono in c# e gli altri sono Java.</span><span class="sxs-lookup"><span data-stu-id="23f55-267">You can also use Data Lake tools for Visual Studio toocreate hybrid topologies, where some components are C# and others are Java.</span></span>

<span data-ttu-id="23f55-268">Per un esempio di topologia ibrida, creare un progetto e selezionare **Storm Hybrid Sample**.</span><span class="sxs-lookup"><span data-stu-id="23f55-268">For an example of a hybrid topology, create a project and select **Storm Hybrid Sample**.</span></span> <span data-ttu-id="23f55-269">Il tipo di questo esempio viene illustrato hello seguenti concetti:</span><span class="sxs-lookup"><span data-stu-id="23f55-269">This sample type demonstrates hello following concepts:</span></span>

* <span data-ttu-id="23f55-270">**Java spout** e **C# bolt**: definiti in **HybridTopology_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="23f55-270">**Java spout** and **C# bolt**: Defined in **HybridTopology_javaSpout_csharpBolt**.</span></span>

    * <span data-ttu-id="23f55-271">Una versione transazionale è definita in **HybridTopologyTx_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="23f55-271">A transactional version is defined in **HybridTopologyTx_javaSpout_csharpBolt**.</span></span>

* <span data-ttu-id="23f55-272">**C# spout** e **Java bolt**: definiti in **HybridTopology_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="23f55-272">**C# spout** and **Java bolt**: Defined in **HybridTopology_csharpSpout_javaBolt**.</span></span>

    * <span data-ttu-id="23f55-273">Una versione transazionale è definita in **HybridTopologyTx_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="23f55-273">A transactional version is defined in **HybridTopologyTx_csharpSpout_javaBolt**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="23f55-274">Questa versione viene inoltre illustrato come il codice da un file di testo come componente Java toouse Clojure.</span><span class="sxs-lookup"><span data-stu-id="23f55-274">This version also demonstrates how toouse Clojure code from a text file as a Java component.</span></span>


<span data-ttu-id="23f55-275">topologia di hello tooswitch utilizzata quando il progetto hello viene inviato, è sufficiente spostare hello `[Active(true)]` istruzione toohello topologia toouse, prima di inviarla toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="23f55-275">tooswitch hello topology that is used when hello project is submitted, simply move hello `[Active(true)]` statement toohello topology you want toouse, before submitting it toohello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="23f55-276">Tutti i file Java hello necessari vengono forniti come parte di questo progetto in hello **JavaDependency** cartella.</span><span class="sxs-lookup"><span data-stu-id="23f55-276">All hello Java files that are required are provided as part of this project in hello **JavaDependency** folder.</span></span>

<span data-ttu-id="23f55-277">Quando si desidera creare e inviare una topologia ibrida considerare hello segue:</span><span class="sxs-lookup"><span data-stu-id="23f55-277">Consider hello following when you are creating and submitting a hybrid topology:</span></span>

* <span data-ttu-id="23f55-278">È necessario utilizzare **JavaComponentConstructor** toocreate un'istanza della classe Java per un beccuccio o fulmine hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-278">You must use **JavaComponentConstructor** toocreate an instance of hello Java class for a spout or bolt.</span></span>

* <span data-ttu-id="23f55-279">È consigliabile utilizzare **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** tooJSON di oggetti dati tooserialize interno o all'esterno di componenti Java da Java.</span><span class="sxs-lookup"><span data-stu-id="23f55-279">You should use **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** tooserialize data into or out of Java components from Java objects tooJSON.</span></span>

* <span data-ttu-id="23f55-280">Quando si inviano server toohello di hello topologia, è necessario utilizzare hello **configurazioni aggiuntive** hello toospecify opzione **i percorsi di File Java**.</span><span class="sxs-lookup"><span data-stu-id="23f55-280">When submitting hello topology toohello server, you must use hello **Additional configurations** option toospecify hello **Java File paths**.</span></span> <span data-ttu-id="23f55-281">percorso Hello specificato deve essere una directory hello che contiene i file JAR hello che contengono le classi di Java.</span><span class="sxs-lookup"><span data-stu-id="23f55-281">hello path specified should be hello directory that contains hello JAR files that contain your Java classes.</span></span>

### <a name="azure-event-hubs"></a><span data-ttu-id="23f55-282">Hub eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="23f55-282">Azure Event Hubs</span></span>

<span data-ttu-id="23f55-283">Versione SCP.NET 0.9.4.203 introduce una nuova classe e metodo in modo specifico per l'utilizzo con beccuccio Hub eventi hello (Java beccuccio che legge da hub eventi).</span><span class="sxs-lookup"><span data-stu-id="23f55-283">SCP.NET version 0.9.4.203 introduces a new class and method specifically for working with hello Event Hub spout (a Java spout that reads from Event Hubs).</span></span> <span data-ttu-id="23f55-284">Quando si crea una topologia che utilizza un beccuccio Hub eventi, utilizzare hello dei seguenti metodi:</span><span class="sxs-lookup"><span data-stu-id="23f55-284">When you create a topology that uses an Event Hub spout, use hello following methods:</span></span>

* <span data-ttu-id="23f55-285">**EventHubSpoutConfig** classe: crea un oggetto che contiene la configurazione hello componente beccuccio hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-285">**EventHubSpoutConfig** class: Creates an object that contains hello configuration for hello spout component.</span></span>

* <span data-ttu-id="23f55-286">**TopologyBuilder.SetEventHubSpout** metodo: aggiunge la topologia toohello hello Hub eventi beccuccio componente.</span><span class="sxs-lookup"><span data-stu-id="23f55-286">**TopologyBuilder.SetEventHubSpout** method: Adds hello Event Hub spout component toohello topology.</span></span>

> [!NOTE]
> <span data-ttu-id="23f55-287">È necessario usare hello **CustomizedInteropJSONSerializer** tooserialize dati prodotti da beccuccio hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-287">You must still use hello **CustomizedInteropJSONSerializer** tooserialize data produced by hello spout.</span></span>

## <span data-ttu-id="23f55-288"><a id="configurationmanager"></a>Usare ConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="23f55-288"><a id="configurationmanager"></a>Use ConfigurationManager</span></span>

<span data-ttu-id="23f55-289">Non utilizzare **ConfigurationManager** tooretrieve configurazione valori bullone e spout componenti.</span><span class="sxs-lookup"><span data-stu-id="23f55-289">Don't use **ConfigurationManager** tooretrieve configuration values from bolt and spout components.</span></span> <span data-ttu-id="23f55-290">Questa operazione può generare un'eccezione del puntatore null.</span><span class="sxs-lookup"><span data-stu-id="23f55-290">Doing so can cause a null pointer exception.</span></span> <span data-ttu-id="23f55-291">Configurazione di hello per il progetto viene invece passata nella topologia Storm hello come una coppia chiave / valore nel contesto di topologia hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-291">Instead, hello configuration for your project is passed into hello Storm topology as a key and value pair in hello topology context.</span></span> <span data-ttu-id="23f55-292">Ogni componente che si basa su valori di configurazione necessario recuperarli dal contesto hello durante l'inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="23f55-292">Each component that relies on configuration values must retrieve them from hello context during initialization.</span></span>

<span data-ttu-id="23f55-293">Hello codice seguente viene illustrato come tooretrieve questi valori:</span><span class="sxs-lookup"><span data-stu-id="23f55-293">hello following code demonstrates how tooretrieve these values:</span></span>

```csharp
public class MyComponent : ISCPBolt
{
    // toohold configuration information loaded from context
    Configuration configuration;
    ...
    public MyComponent(Context ctx, Dictionary<string, Object> parms)
    {
        // Save a copy of hello context for this component instance
        this.ctx = ctx;
        // If it exists, load hello configuration for hello component
        if(parms.ContainsKey(Constants.USER_CONFIG))
        {
            this.configuration = parms[Constants.USER_CONFIG] as System.Configuration.Configuration;
        }
        // Retrieve hello value of "Foo" from configuration
        var foo = this.configuration.AppSettings.Settings["Foo"].Value;
    }
    ...
}
```

<span data-ttu-id="23f55-294">Se si utilizza un `Get` tooreturn metodo un'istanza del componente, è necessario assicurarsi che entrambi hello passa `Context` e `Dictionary<string, Object>` costruttore toohello parametri.</span><span class="sxs-lookup"><span data-stu-id="23f55-294">If you use a `Get` method tooreturn an instance of your component, you must ensure that it passes both hello `Context` and `Dictionary<string, Object>` parameters toohello constructor.</span></span> <span data-ttu-id="23f55-295">esempio Hello è un basic `Get` metodo correttamente passa questi valori:</span><span class="sxs-lookup"><span data-stu-id="23f55-295">hello following example is a basic `Get` method that properly passes these values:</span></span>

```csharp
public static MyComponent Get(Context ctx, Dictionary<string, Object> parms)
{
    return new MyComponent(ctx, parms);
}
```

## <a name="how-tooupdate-scpnet"></a><span data-ttu-id="23f55-296">Come tooupdate SCP.NET</span><span class="sxs-lookup"><span data-stu-id="23f55-296">How tooupdate SCP.NET</span></span>

<span data-ttu-id="23f55-297">Le versioni recenti di SCP.NET supportano l'aggiornamento del pacchetto tramite NuGet.</span><span class="sxs-lookup"><span data-stu-id="23f55-297">Recent releases of SCP.NET support package upgrade through NuGet.</span></span> <span data-ttu-id="23f55-298">Quando è disponibile un nuovo aggiornamento, si riceve una notifica.</span><span class="sxs-lookup"><span data-stu-id="23f55-298">When a new update is available, you receive an upgrade notification.</span></span> <span data-ttu-id="23f55-299">controllo toomanually per un aggiornamento, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="23f55-299">toomanually check for an upgrade, follow these steps:</span></span>

1. <span data-ttu-id="23f55-300">In **Esplora**, fare clic sul progetto hello e selezionare **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="23f55-300">In **Solution Explorer**, right-click hello project, and select **Manage NuGet Packages**.</span></span>

2. <span data-ttu-id="23f55-301">Gestione di pacchetti hello, selezionare **aggiornamenti**.</span><span class="sxs-lookup"><span data-stu-id="23f55-301">From hello package manager, select **Updates**.</span></span> <span data-ttu-id="23f55-302">Se un aggiornamento è disponibile, è presente nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="23f55-302">If an update is available, it is listed.</span></span> <span data-ttu-id="23f55-303">Fare clic su **aggiornamento** per tooinstall pacchetto hello è.</span><span class="sxs-lookup"><span data-stu-id="23f55-303">Click **Update** for hello package tooinstall it.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="23f55-304">Se il progetto è stato creato con una versione precedente di SCP.NET che non utilizza NuGet, è necessario eseguire hello versione più recente tooa tooupdate di passaggi seguente:</span><span class="sxs-lookup"><span data-stu-id="23f55-304">If your project was created with an earlier version of SCP.NET that did not use NuGet, you must perform hello following steps tooupdate tooa newer version:</span></span>
>
> 1. <span data-ttu-id="23f55-305">In **Esplora**, fare clic sul progetto hello e selezionare **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="23f55-305">In **Solution Explorer**, right-click hello project, and select **Manage NuGet Packages**.</span></span>
> 2. <span data-ttu-id="23f55-306">Utilizzo di hello **ricerca** campo, cercare e quindi aggiungere, **Microsoft.SCP.Net.SDK** toohello progetto.</span><span class="sxs-lookup"><span data-stu-id="23f55-306">Using hello **Search** field, search for, and then add, **Microsoft.SCP.Net.SDK** toohello project.</span></span>

## <a name="troubleshoot-common-issues-with-topologies"></a><span data-ttu-id="23f55-307">Risoluzione di problemi comuni con le topologie</span><span class="sxs-lookup"><span data-stu-id="23f55-307">Troubleshoot common issues with topologies</span></span>

### <a name="null-pointer-exceptions"></a><span data-ttu-id="23f55-308">Eccezioni del puntatore null</span><span class="sxs-lookup"><span data-stu-id="23f55-308">Null pointer exceptions</span></span>

<span data-ttu-id="23f55-309">Quando si utilizza una topologia c# con un cluster HDInsight basati su Linux, bullone e componenti che utilizzano spout **ConfigurationManager** tooread le impostazioni di configurazione in fase di esecuzione possono restituire le eccezioni di puntatore null.</span><span class="sxs-lookup"><span data-stu-id="23f55-309">When you are using a C# topology with a Linux-based HDInsight cluster, bolt and spout components that use **ConfigurationManager** tooread configuration settings at runtime may return null pointer exceptions.</span></span>

<span data-ttu-id="23f55-310">configurazione di Hello per il progetto viene passato come una coppia chiave / valore nel contesto di topologia hello topologia Storm hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-310">hello configuration for your project is passed into hello Storm topology as a key and value pair in hello topology context.</span></span> <span data-ttu-id="23f55-311">Può essere recuperato dall'oggetto dizionario hello passato tooyour componenti quando vengono inizializzati.</span><span class="sxs-lookup"><span data-stu-id="23f55-311">It can be retrieved from hello dictionary object that is passed tooyour components when they are initialized.</span></span>

<span data-ttu-id="23f55-312">Per ulteriori informazioni, vedere hello [ConfigurationManager](#configurationmanager) sezione di questo documento.</span><span class="sxs-lookup"><span data-stu-id="23f55-312">For more information, see hello [ConfigurationManager](#configurationmanager) section of this document.</span></span>

### <a name="systemtypeloadexception"></a><span data-ttu-id="23f55-313">System.TypeLoadException</span><span class="sxs-lookup"><span data-stu-id="23f55-313">System.TypeLoadException</span></span>

<span data-ttu-id="23f55-314">Quando si utilizza una topologia c# con un cluster HDInsight basati su Linux, è possibile riscontrare hello errore seguente:</span><span class="sxs-lookup"><span data-stu-id="23f55-314">When you are using a C# topology with a Linux-based HDInsight cluster, you may encounter hello following error:</span></span>

    System.TypeLoadException: Failure has occurred while loading a type.

<span data-ttu-id="23f55-315">Questo errore si verifica quando si utilizza un file binario che non è compatibile con la versione di hello di .NET che supporta Mono.</span><span class="sxs-lookup"><span data-stu-id="23f55-315">This error occurs when you use a binary that is not compatible with hello version of .NET that Mono supports.</span></span>

<span data-ttu-id="23f55-316">Per i cluster HDInsight basati su Linux, è necessario verificare che il progetto usi file binari compilati per .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="23f55-316">For Linux-based HDInsight clusters, make sure that your project uses binaries compiled for .NET 4.5.</span></span>

### <a name="test-a-topology-locally"></a><span data-ttu-id="23f55-317">Testare la topologia in locale</span><span class="sxs-lookup"><span data-stu-id="23f55-317">Test a topology locally</span></span>

<span data-ttu-id="23f55-318">Sebbene sia facile toodeploy un cluster di tooa topologia, in alcuni casi, potrebbe essere necessario tootest una topologia in locale.</span><span class="sxs-lookup"><span data-stu-id="23f55-318">Although it is easy toodeploy a topology tooa cluster, in some cases, you may need tootest a topology locally.</span></span> <span data-ttu-id="23f55-319">Utilizzare i seguenti passaggi toorun hello e testare la topologia di esempio hello in questa esercitazione in locale nell'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="23f55-319">Use hello following steps toorun and test hello example topology in this tutorial locally in your development environment.</span></span>

> [!WARNING]
> <span data-ttu-id="23f55-320">I test locali funzionano solo per topologie di base di tipo C#.</span><span class="sxs-lookup"><span data-stu-id="23f55-320">Local testing only works for basic, C#-only topologies.</span></span> <span data-ttu-id="23f55-321">Non è possibile usare il test locale per topologie ibride o topologie che impiegano più flussi.</span><span class="sxs-lookup"><span data-stu-id="23f55-321">You cannot use local testing for hybrid topologies or topologies that use multiple streams.</span></span>

1. <span data-ttu-id="23f55-322">In **Esplora**, fare clic sul progetto hello e selezionare **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="23f55-322">In **Solution Explorer**, right-click hello project, and select **Properties**.</span></span> <span data-ttu-id="23f55-323">Nelle proprietà del progetto hello, modificare hello **tipo di Output** troppo**applicazione Console**.</span><span class="sxs-lookup"><span data-stu-id="23f55-323">In hello project properties, change hello **Output type** too**Console Application**.</span></span>

    ![Screenshot delle proprietà di progetto, con il tipo di Output evidenziato](./media/hdinsight-storm-develop-csharp-visual-studio-topology/outputtype.png)

   > [!NOTE]
   > <span data-ttu-id="23f55-325">Ricordare hello toochange **tipo di Output** troppo indietro**libreria di classi** prima di distribuire cluster tooa di hello topologia.</span><span class="sxs-lookup"><span data-stu-id="23f55-325">Remember toochange hello **Output type** back too**Class Library** before you deploy hello topology tooa cluster.</span></span>

2. <span data-ttu-id="23f55-326">In **Esplora**, fare clic sul progetto hello e quindi selezionare **Aggiungi** > **nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="23f55-326">In **Solution Explorer**, right-click hello project, and then select **Add** > **New Item**.</span></span> <span data-ttu-id="23f55-327">Selezionare **classe**, quindi immettere **LocalTest.cs** come nome della classe hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-327">Select **Class**, and enter **LocalTest.cs** as hello class name.</span></span> <span data-ttu-id="23f55-328">Infine fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="23f55-328">Finally, click **Add**.</span></span>

3. <span data-ttu-id="23f55-329">Aprire **LocalTest.cs**e aggiungere il seguente hello **utilizzando** istruzione nella parte superiore di hello:</span><span class="sxs-lookup"><span data-stu-id="23f55-329">Open **LocalTest.cs**, and add hello following **using** statement at hello top:</span></span>

    ```csharp
    using Microsoft.SCP;
    ```

4. <span data-ttu-id="23f55-330">Esempio di codice seguente di hello utilizzare come contenuto di hello di hello **LocalTest** classe:</span><span class="sxs-lookup"><span data-stu-id="23f55-330">Use hello following code as hello contents of hello **LocalTest** class:</span></span>

    ```csharp
    // Drives hello topology components
    public void RunTestCase()
    {
        // An empty dictionary for use when creating components
        Dictionary<string, Object> emptyDictionary = new Dictionary<string, object>();

        #region Test hello spout
        {
            Console.WriteLine("Starting spout");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext spoutCtx = LocalContext.Get();
            // Get a new instance of hello spout, using hello local context
            Spout sentences = Spout.Get(spoutCtx, emptyDictionary);

            // Emit 10 tuples
            for (int i = 0; i < 10; i++)
            {
                sentences.NextTuple(emptyDictionary);
            }
            // Use LocalContext toopersist hello data stream toofile
            spoutCtx.WriteMsgQueueToFile("sentences.txt");
            Console.WriteLine("Spout finished");
        }
        #endregion

        #region Test hello splitter bolt
        {
            Console.WriteLine("Starting splitter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext splitterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Splitter splitter = Splitter.Get(splitterCtx, emptyDictionary);

            // Set hello data stream toohello data created by hello spout
            splitterCtx.ReadFromFileToMsgQueue("sentences.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = splitterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                splitter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            splitterCtx.WriteMsgQueueToFile("splitter.txt");
            Console.WriteLine("Splitter bolt finished");
        }
        #endregion

        #region Test hello counter bolt
        {
            Console.WriteLine("Starting counter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext counterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Counter counter = Counter.Get(counterCtx, emptyDictionary);

            // Set hello data stream toohello data created by splitter bolt
            counterCtx.ReadFromFileToMsgQueue("splitter.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = counterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                counter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            counterCtx.WriteMsgQueueToFile("counter.txt");
            Console.WriteLine("Counter bolt finished");
        }
        #endregion
    }
    ```

    <span data-ttu-id="23f55-331">Richiedere un tooread momento tramite i commenti di codice hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-331">Take a moment tooread through hello code comments.</span></span> <span data-ttu-id="23f55-332">Questo codice Usa **LocalContext** componenti hello toorun nell'ambiente di sviluppo hello e mantiene il flusso di dati hello tra file tootext componenti sul disco locale hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-332">This code uses **LocalContext** toorun hello components in hello development environment, and it persists hello data stream between components tootext files on hello local drive.</span></span>

1. <span data-ttu-id="23f55-333">Aprire **Program.cs**e aggiungere hello seguente toohello **Main** metodo:</span><span class="sxs-lookup"><span data-stu-id="23f55-333">Open **Program.cs**, and add hello following toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Starting tests");
    System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "WordCount-LocalTest");
    // Initialize hello runtime
    SCPRuntime.Initialize();

    //If we are not running under hello local context, throw an error
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)
    {
        throw new Exception(string.Format("unexpected pluginType: {0}", Context.pluginType));
    }
    // Create test instance
    LocalTest tests = new LocalTest();
    // Run tests
    tests.RunTestCase();
    Console.WriteLine("Tests finished");
    Console.ReadKey();
    ```

2. <span data-ttu-id="23f55-334">Salvare le modifiche di hello e quindi fare clic su **F5** o seleziona **Debug** > **Avvia debug** progetto hello toostart.</span><span class="sxs-lookup"><span data-stu-id="23f55-334">Save hello changes, and then click **F5** or select **Debug** > **Start Debugging** toostart hello project.</span></span> <span data-ttu-id="23f55-335">Una finestra della console dovrà essere visualizzato e stato del log come stato di avanzamento test hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-335">A console window should appear, and log status as hello tests progress.</span></span> <span data-ttu-id="23f55-336">Quando **test completato** viene visualizzato, premere qualsiasi finestra hello tooclose chiave.</span><span class="sxs-lookup"><span data-stu-id="23f55-336">When **Tests finished** appears, press any key tooclose hello window.</span></span>

3. <span data-ttu-id="23f55-337">Utilizzare **Esplora** directory hello toolocate contenente il progetto.</span><span class="sxs-lookup"><span data-stu-id="23f55-337">Use **Windows Explorer** toolocate hello directory that contains your project.</span></span> <span data-ttu-id="23f55-338">Ad esempio **C:\Users\<your_user_name>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span><span class="sxs-lookup"><span data-stu-id="23f55-338">For example: **C:\Users\<your_user_name>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span></span> <span data-ttu-id="23f55-339">In questa directory, aprire **Bin** e quindi fare clic su **Debug**.</span><span class="sxs-lookup"><span data-stu-id="23f55-339">In this directory, open **Bin**, and then click **Debug**.</span></span> <span data-ttu-id="23f55-340">Dovrebbe essere file di testo hello generati durante l'esecuzione di test hello: sentences.txt counter.txt e splitter.txt.</span><span class="sxs-lookup"><span data-stu-id="23f55-340">You should see hello text files that were produced when hello tests ran: sentences.txt, counter.txt, and splitter.txt.</span></span> <span data-ttu-id="23f55-341">Aprire ogni file di testo e verificare dati hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-341">Open each text file and inspect hello data.</span></span>

   > [!NOTE]
   > <span data-ttu-id="23f55-342">In questi file i dati stringa vengono resi permanenti come matrice di valori decimali.</span><span class="sxs-lookup"><span data-stu-id="23f55-342">String data persists as an array of decimal values in these files.</span></span> <span data-ttu-id="23f55-343">Ad esempio, \[[97,103,111]] in hello **splitter.txt** file è una parola hello *e*.</span><span class="sxs-lookup"><span data-stu-id="23f55-343">For example, \[[97,103,111]] in hello **splitter.txt** file is hello word *and*.</span></span>

> [!NOTE]
> <span data-ttu-id="23f55-344">Essere certi hello tooset **tipo di progetto** troppo indietro**libreria di classi** prima di distribuire tooa Storm nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="23f55-344">Be sure tooset hello **Project type** back too**Class Library** before deploying tooa Storm on HDInsight cluster.</span></span>

### <a name="log-information"></a><span data-ttu-id="23f55-345">Informazioni di log</span><span class="sxs-lookup"><span data-stu-id="23f55-345">Log information</span></span>

<span data-ttu-id="23f55-346">È possibile registrare facilmente le informazioni provenienti dai componenti della topologia usando `Context.Logger`.</span><span class="sxs-lookup"><span data-stu-id="23f55-346">You can easily log information from your topology components by using `Context.Logger`.</span></span> <span data-ttu-id="23f55-347">Ad esempio, l'esempio hello crea una voce di log informativo:</span><span class="sxs-lookup"><span data-stu-id="23f55-347">For example, hello following creates an informational log entry:</span></span>

```csharp
Context.Logger.Info("Component started");
```

<span data-ttu-id="23f55-348">Le informazioni registrate possono essere visualizzate dal hello **registro del servizio Hadoop**, che si trovano in **Esplora Server**.</span><span class="sxs-lookup"><span data-stu-id="23f55-348">Logged information can be viewed from hello **Hadoop Service Log**, which is found in **Server Explorer**.</span></span> <span data-ttu-id="23f55-349">Espandere la voce hello per le Storm nel cluster HDInsight e quindi **registro del servizio Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="23f55-349">Expand hello entry for your Storm on HDInsight cluster, and then expand **Hadoop Service Log**.</span></span> <span data-ttu-id="23f55-350">Infine, selezionare tooview file di log hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-350">Finally, select hello log file tooview.</span></span>

> [!NOTE]
> <span data-ttu-id="23f55-351">Hello log vengono archiviati in account di archiviazione di Azure che viene utilizzato il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-351">hello logs are stored in hello Azure storage account that is used by your cluster.</span></span> <span data-ttu-id="23f55-352">log di hello tooview in Visual Studio, è necessario accedere toohello sottoscrizione Azure a cui appartiene l'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-352">tooview hello logs in Visual Studio, you must sign in toohello Azure subscription that owns hello storage account.</span></span>

### <a name="view-error-information"></a><span data-ttu-id="23f55-353">Visualizzare le informazioni sugli errori</span><span class="sxs-lookup"><span data-stu-id="23f55-353">View error information</span></span>

<span data-ttu-id="23f55-354">tooview errori che si sono verificati in una topologia in esecuzione, utilizzare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="23f55-354">tooview errors that have occurred in a running topology, use hello following steps:</span></span>

1. <span data-ttu-id="23f55-355">Da **Esplora Server**, hello Storm nel cluster HDInsight e scegliere **topologie Storm vista**.</span><span class="sxs-lookup"><span data-stu-id="23f55-355">From **Server Explorer**, right-click hello Storm on HDInsight cluster, and select **View Storm topologies**.</span></span>

2. <span data-ttu-id="23f55-356">Per hello **Spout** e **bulloni**, hello **ultimo errore** colonna contiene informazioni sull'ultimo errore hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-356">For hello **Spout** and **Bolts**, hello **Last Error** column contains information on hello last error.</span></span>

3. <span data-ttu-id="23f55-357">Seleziona hello **Spout Id** o **Id fulmine** per il componente hello che contiene un errore elencato.</span><span class="sxs-lookup"><span data-stu-id="23f55-357">Select hello **Spout Id** or **Bolt Id** for hello component that has an error listed.</span></span> <span data-ttu-id="23f55-358">Nella pagina dettagli hello di errore visualizzato e altre informazioni sono elencate nella hello **errori** sezione hello parte inferiore della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-358">On hello details page that is displayed, additional error information is listed in hello **Errors** section at hello bottom of hello page.</span></span>

4. <span data-ttu-id="23f55-359">tooobtain ulteriori informazioni, selezionare un **porta** da hello **executor** sezione della pagina hello, toosee hello Storm lavoro registro hello ultimi minuti.</span><span class="sxs-lookup"><span data-stu-id="23f55-359">tooobtain more information, select a **Port** from hello **Executors** section of hello page, toosee hello Storm worker log for hello last few minutes.</span></span>

### <a name="errors-submitting-topologies"></a><span data-ttu-id="23f55-360">Errori durante l'invio delle topologie</span><span class="sxs-lookup"><span data-stu-id="23f55-360">Errors submitting topologies</span></span>

<span data-ttu-id="23f55-361">Se si verificano errori di invio di una topologia tooHDInsight, è possibile trovare log dei componenti lato server hello che gestiscono l'invio di topologia il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="23f55-361">If you encounter errors submitting a topology tooHDInsight, you can find logs for hello server-side components that handle topology submission on your HDInsight cluster.</span></span> <span data-ttu-id="23f55-362">tooretrieve questi log, utilizzare hello comando seguente dalla riga di comando:</span><span class="sxs-lookup"><span data-stu-id="23f55-362">tooretrieve these logs, use hello following command from a command line:</span></span>

    scp sshuser@clustername-ssh.azurehdinsight.net:/var/log/hdinsight-scpwebapi/hdinsight-scpwebapi.out .

<span data-ttu-id="23f55-363">Sostituire __sshuser__ con account utente SSH per il cluster hello hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-363">Replace __sshuser__ with hello SSH user account for hello cluster.</span></span> <span data-ttu-id="23f55-364">Sostituire __clustername__ con nome hello del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-364">Replace __clustername__ with hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="23f55-365">Per altre informazioni sull'uso di `scp` e `ssh` con HDInsight, vedere l'articolo [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="23f55-365">For more information on using `scp` and `ssh` with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="23f55-366">Gli invii possono non riuscire per diversi motivi:</span><span class="sxs-lookup"><span data-stu-id="23f55-366">Submissions can fail for multiple reasons:</span></span>

* <span data-ttu-id="23f55-367">JDK non è installato o non è presente nel percorso di hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-367">JDK is not installed or is not in hello path.</span></span>
* <span data-ttu-id="23f55-368">Dipendenze di Java richieste non sono inclusi in inoltro hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-368">Required Java dependencies are not included in hello submission.</span></span>
* <span data-ttu-id="23f55-369">Dipendenze incompatibili.</span><span class="sxs-lookup"><span data-stu-id="23f55-369">Incompatible dependencies.</span></span>
* <span data-ttu-id="23f55-370">Nomi di topologia duplicati.</span><span class="sxs-lookup"><span data-stu-id="23f55-370">Duplicate topology names.</span></span>

<span data-ttu-id="23f55-371">Se hello `hdinsight-scpwebapi.out` registro contiene un `FileNotFoundException`, ciò potrebbe dipendere da hello seguenti condizioni:</span><span class="sxs-lookup"><span data-stu-id="23f55-371">If hello `hdinsight-scpwebapi.out` log contains a `FileNotFoundException`, this might be caused by hello following conditions:</span></span>

* <span data-ttu-id="23f55-372">Hello JDK non è presente nel percorso di hello nell'ambiente di sviluppo hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-372">hello JDK is not in hello path on hello development environment.</span></span> <span data-ttu-id="23f55-373">Verificare che hello JDK è installato nell'ambiente di sviluppo hello e che `%JAVA_HOME%/bin` si trova nel percorso di hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-373">Verify that hello JDK is installed in hello development environment, and that `%JAVA_HOME%/bin` is in hello path.</span></span>
* <span data-ttu-id="23f55-374">Manca una dipendenza Java.</span><span class="sxs-lookup"><span data-stu-id="23f55-374">You are missing a Java dependency.</span></span> <span data-ttu-id="23f55-375">Verificare che si sono inclusi tutti i file JAR richiesto come parte dell'invio hello.</span><span class="sxs-lookup"><span data-stu-id="23f55-375">Make sure you are including any required .jar files as part of hello submission.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23f55-376">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="23f55-376">Next steps</span></span>

<span data-ttu-id="23f55-377">Per un esempio di elaborazione dei dati dall'hub eventi, vedere [Elaborare eventi dell'hub eventi di Azure con Storm in HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="23f55-377">For an example of processing data from Event Hubs, see [Process events from Azure Event Hubs with Storm on HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span>

<span data-ttu-id="23f55-378">Per un esempio di una topologia di C# che divide il flusso di dati in più flussi, vedere [csharp-storm-example](https://github.com/Blackmist/csharp-storm-example).</span><span class="sxs-lookup"><span data-stu-id="23f55-378">For an example of a C# topology that splits stream data into multiple streams, see [C# Storm example](https://github.com/Blackmist/csharp-storm-example).</span></span>

<span data-ttu-id="23f55-379">vedere altre informazioni sulla creazione di c# con le topologie, toodiscover [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span><span class="sxs-lookup"><span data-stu-id="23f55-379">toodiscover more information about creating C# topologies, see [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span></span>

<span data-ttu-id="23f55-380">Per altre modalità toowork con HDInsight e altre Storm su campioni di HDInsight, vedere hello seguenti documenti:</span><span class="sxs-lookup"><span data-stu-id="23f55-380">For more ways toowork with HDInsight and more Storm on HDInsight samples, see hello following documents:</span></span>

<span data-ttu-id="23f55-381">**Microsoft SCP.NET**</span><span class="sxs-lookup"><span data-stu-id="23f55-381">**Microsoft SCP.NET**</span></span>

* [<span data-ttu-id="23f55-382">Guida alla programmazione SCP</span><span class="sxs-lookup"><span data-stu-id="23f55-382">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)

<span data-ttu-id="23f55-383">**Apache Storm in HDInsight**</span><span class="sxs-lookup"><span data-stu-id="23f55-383">**Apache Storm on HDInsight**</span></span>

* [<span data-ttu-id="23f55-384">Distribuzione e monitoraggio di topologie con Apache Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="23f55-384">Deploy and monitor topologies with Apache Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)
* [<span data-ttu-id="23f55-385">Topologie di esempio per Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="23f55-385">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

<span data-ttu-id="23f55-386">**Apache Hadoop in HDInsight**</span><span class="sxs-lookup"><span data-stu-id="23f55-386">**Apache Hadoop on HDInsight**</span></span>

* [<span data-ttu-id="23f55-387">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="23f55-387">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="23f55-388">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="23f55-388">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="23f55-389">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="23f55-389">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="23f55-390">**Apache HBase in HDInsight**</span><span class="sxs-lookup"><span data-stu-id="23f55-390">**Apache HBase on HDInsight**</span></span>

* [<span data-ttu-id="23f55-391">Introduzione a HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="23f55-391">Getting started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
