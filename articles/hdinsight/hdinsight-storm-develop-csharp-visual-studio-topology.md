---
title: Topologie Apache Storm con Visual Studio e Visual C# - Azure HDInsight | Microsoft Docs
description: Informazioni su come creare topologie Storm in C#. Creare una semplice topologia di conteggio parole in Visual Studio usando gli strumenti Hadoop per Visual Studio.
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
ms.openlocfilehash: 3ee89b6644ba395e0a6c28ecc2c082c2f7393ac8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="develop-c-topologies-for-apache-storm-by-using-the-data-lake-tools-for-visual-studio"></a><span data-ttu-id="13e46-104">Sviluppare topologie C# per Apache Storm tramite gli strumenti Data Lake per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="13e46-104">Develop C# topologies for Apache Storm by using the Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="13e46-105">Informazioni su come creare una topologia Storm C# usando gli strumenti Azure Data Lake (Hadoop) per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="13e46-105">Learn how to create a C# Storm topology by using the Azure Data Lake (Hadoop) tools for Visual Studio.</span></span> <span data-ttu-id="13e46-106">Questo documento illustra il processo di creazione di un progetto Storm in Visual Studio, l'esecuzione dei test in locale e la distribuzione del progetto in un cluster Apache Storm in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="13e46-106">This document walks through the process of creating a Storm project in Visual Studio, testing it locally, and deploying it to an Apache Storm on Azure HDInsight cluster.</span></span>

<span data-ttu-id="13e46-107">Viene anche spiegato come creare topologie ibride che usano componenti C# e Java.</span><span class="sxs-lookup"><span data-stu-id="13e46-107">You also learn how to create hybrid topologies that use C# and Java components.</span></span>

> [!NOTE]
> <span data-ttu-id="13e46-108">Anche se i passaggi illustrati in questo documento si basano su un ambiente di sviluppo Windows con Visual Studio, il progetto compilato può essere inviato a un cluster HDInsight basato su Linux o su Windows.</span><span class="sxs-lookup"><span data-stu-id="13e46-108">While the steps in this document rely on a Windows development environment with Visual Studio, the compiled project can be submitted to either a Linux or Windows-based HDInsight cluster.</span></span> <span data-ttu-id="13e46-109">Solo i cluster basati su Linux creati dopo il 28 ottobre 2016 supportano le topologie SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="13e46-109">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="13e46-110">Per usare una topologia C# con un cluster basato su Linux, è necessario aggiornare il pacchetto NuGet Microsoft.SCP.Net.SDK usato dal progetto alla versione 0.10.0.6 o successiva.</span><span class="sxs-lookup"><span data-stu-id="13e46-110">To use a C# topology with a Linux-based cluster, you must update the Microsoft.SCP.Net.SDK NuGet package used by your project to version 0.10.0.6 or later.</span></span> <span data-ttu-id="13e46-111">La versione del pacchetto deve anche corrispondere alla versione principale di Storm installata in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="13e46-111">The version of the package must also match the major version of Storm installed on HDInsight.</span></span>

| <span data-ttu-id="13e46-112">Versione HDInsight</span><span class="sxs-lookup"><span data-stu-id="13e46-112">HDInsight version</span></span> | <span data-ttu-id="13e46-113">Versione di Storm</span><span class="sxs-lookup"><span data-stu-id="13e46-113">Storm version</span></span> | <span data-ttu-id="13e46-114">Versione di SCP.NET</span><span class="sxs-lookup"><span data-stu-id="13e46-114">SCP.NET version</span></span> | <span data-ttu-id="13e46-115">Versione Mono predefinita</span><span class="sxs-lookup"><span data-stu-id="13e46-115">Default Mono version</span></span> |
|:-----------------:|:-------------:|:---------------:|:--------------------:|
| <span data-ttu-id="13e46-116">3.3</span><span class="sxs-lookup"><span data-stu-id="13e46-116">3.3</span></span> |<span data-ttu-id="13e46-117">0.10.x</span><span class="sxs-lookup"><span data-stu-id="13e46-117">0.10.x</span></span> |<span data-ttu-id="13e46-118">0.10.x.x</span><span class="sxs-lookup"><span data-stu-id="13e46-118">0.10.x.x</span></span></br><span data-ttu-id="13e46-119">(solo in HDInsight per Windows)</span><span class="sxs-lookup"><span data-stu-id="13e46-119">(only on Windows-based HDInsight)</span></span> | <span data-ttu-id="13e46-120">ND</span><span class="sxs-lookup"><span data-stu-id="13e46-120">NA</span></span> |
| <span data-ttu-id="13e46-121">3.4</span><span class="sxs-lookup"><span data-stu-id="13e46-121">3.4</span></span> | <span data-ttu-id="13e46-122">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="13e46-122">0.10.0.x</span></span> | <span data-ttu-id="13e46-123">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="13e46-123">0.10.0.x</span></span> | <span data-ttu-id="13e46-124">3.2.8</span><span class="sxs-lookup"><span data-stu-id="13e46-124">3.2.8</span></span> |
| <span data-ttu-id="13e46-125">3,5</span><span class="sxs-lookup"><span data-stu-id="13e46-125">3.5</span></span> | <span data-ttu-id="13e46-126">1.0.2.x</span><span class="sxs-lookup"><span data-stu-id="13e46-126">1.0.2.x</span></span> | <span data-ttu-id="13e46-127">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="13e46-127">1.0.0.x</span></span> | <span data-ttu-id="13e46-128">4.2.1</span><span class="sxs-lookup"><span data-stu-id="13e46-128">4.2.1</span></span> |
| <span data-ttu-id="13e46-129">3.6</span><span class="sxs-lookup"><span data-stu-id="13e46-129">3.6</span></span> | <span data-ttu-id="13e46-130">1.1.0.x</span><span class="sxs-lookup"><span data-stu-id="13e46-130">1.1.0.x</span></span> | <span data-ttu-id="13e46-131">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="13e46-131">1.0.0.x</span></span> | <span data-ttu-id="13e46-132">4.2.8</span><span class="sxs-lookup"><span data-stu-id="13e46-132">4.2.8</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="13e46-133">Le topologie C# nei cluster basati su Linux devono usare .NET 4.5 e devono usare Mono per l'esecuzione nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="13e46-133">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono to run on the HDInsight cluster.</span></span> <span data-ttu-id="13e46-134">Controllare la [compatibilità Mono](http://www.mono-project.com/docs/about-mono/compatibility/) per potenziali problemi di incompatibilità.</span><span class="sxs-lookup"><span data-stu-id="13e46-134">Check [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) for potential incompatibilities.</span></span>

## <a name="install-visual-studio"></a><span data-ttu-id="13e46-135">Installazione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="13e46-135">Install Visual Studio</span></span>

<span data-ttu-id="13e46-136">È possibile sviluppare topologie C# con SCP.NET usando una delle versioni di Visual Studio seguenti:</span><span class="sxs-lookup"><span data-stu-id="13e46-136">You can develop C# topologies with SCP.NET by using one of the following versions of Visual Studio:</span></span>

* <span data-ttu-id="13e46-137">Visual Studio 2012 con [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="13e46-137">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

* <span data-ttu-id="13e46-138">Visual Studio 2013 con [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) o [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="13e46-138">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>

* <span data-ttu-id="13e46-139">Visual Studio 2015 o [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span><span class="sxs-lookup"><span data-stu-id="13e46-139">Visual Studio 2015 or [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span></span>

* <span data-ttu-id="13e46-140">Visual Studio 2017, qualsiasi edizione</span><span class="sxs-lookup"><span data-stu-id="13e46-140">Visual Studio 2017 (any edition)</span></span>

## <a name="install-data-lake-tools-for-visual-studio"></a><span data-ttu-id="13e46-141">Installare gli strumenti Data Lake per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="13e46-141">Install Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="13e46-142">Per installare gli strumenti Data Lake per Visual Studio, seguire la procedura in [Introduzione all'uso degli strumenti Data Lake per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="13e46-142">To install Data Lake tools for Visual Studio, follow the steps in [Get started using Data Lake tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

## <a name="install-java"></a><span data-ttu-id="13e46-143">Installare Java</span><span class="sxs-lookup"><span data-stu-id="13e46-143">Install Java</span></span>

<span data-ttu-id="13e46-144">Quando si invia una topologia Storm da Visual Studio, SCP.NET genera un file con estensione zip che contiene la topologia e le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="13e46-144">When you submit a Storm topology from Visual Studio, SCP.NET generates a zip file that contains the topology and dependencies.</span></span> <span data-ttu-id="13e46-145">Java viene usato per creare i file con estensione zip perché usa un formato più compatibile con i cluster basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="13e46-145">Java is used to create these zip files, because it uses a format that is more compatible with Linux-based clusters.</span></span>

1. <span data-ttu-id="13e46-146">Installare Java Developer Kit (JDK) 7 o versione successiva nell'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="13e46-146">Install the Java Developer Kit (JDK) 7 or later on your development environment.</span></span> <span data-ttu-id="13e46-147">È possibile ottenere Oracle JDK da [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="13e46-147">You can get the Oracle JDK from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span> <span data-ttu-id="13e46-148">È inoltre possibile usare [altre distribuzioni Java](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="13e46-148">You can also use [other Java distributions](http://openjdk.java.net/).</span></span>

2. <span data-ttu-id="13e46-149">La variabile di ambiente `JAVA_HOME` deve puntare la directory che contiene Java.</span><span class="sxs-lookup"><span data-stu-id="13e46-149">The `JAVA_HOME` environment variable must point to the directory that contains Java.</span></span>

3. <span data-ttu-id="13e46-150">La variabile di ambiente `PATH` deve includere la directory `%JAVA_HOME%\bin`.</span><span class="sxs-lookup"><span data-stu-id="13e46-150">The `PATH` environment variable must include the `%JAVA_HOME%\bin` directory.</span></span>

<span data-ttu-id="13e46-151">È possibile usare l'applicazione console C# seguente per verificare che Java e JDK siano installati correttamente:</span><span class="sxs-lookup"><span data-stu-id="13e46-151">You can use the following C# console application to verify that Java and the JDK are correctly installed:</span></span>

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

## <a name="storm-templates"></a><span data-ttu-id="13e46-152">Modelli Storm</span><span class="sxs-lookup"><span data-stu-id="13e46-152">Storm templates</span></span>

<span data-ttu-id="13e46-153">Gli strumenti Data Lake per Visual Studio includono i modelli seguenti:</span><span class="sxs-lookup"><span data-stu-id="13e46-153">The Data Lake tools for Visual Studio provide the following templates:</span></span>

| <span data-ttu-id="13e46-154">Tipo di progetto</span><span class="sxs-lookup"><span data-stu-id="13e46-154">Project type</span></span> | <span data-ttu-id="13e46-155">Dimostra</span><span class="sxs-lookup"><span data-stu-id="13e46-155">Demonstrates</span></span> |
| --- | --- |
| <span data-ttu-id="13e46-156">Applicazione Storm</span><span class="sxs-lookup"><span data-stu-id="13e46-156">Storm Application</span></span> |<span data-ttu-id="13e46-157">Un progetto di topologia Storm vuoto</span><span class="sxs-lookup"><span data-stu-id="13e46-157">An empty Storm topology project.</span></span> |
| <span data-ttu-id="13e46-158">Esempio di writer SQL di Azure per Storm</span><span class="sxs-lookup"><span data-stu-id="13e46-158">Storm Azure SQL Writer Sample</span></span> |<span data-ttu-id="13e46-159">Come scrivere nel database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="13e46-159">How to write to Azure SQL Database.</span></span> |
| <span data-ttu-id="13e46-160">Esempio di reader Storm per Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="13e46-160">Storm Azure Cosmos DB Reader Sample</span></span> |<span data-ttu-id="13e46-161">Come leggere da Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="13e46-161">How to read from Azure Cosmos DB.</span></span> |
| <span data-ttu-id="13e46-162">Esempio di writer Storm per Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="13e46-162">Storm Azure Cosmos DB Writer Sample</span></span> |<span data-ttu-id="13e46-163">Come scrivere in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="13e46-163">How to write to Azure Cosmos DB.</span></span> |
| <span data-ttu-id="13e46-164">Esempio di lettore EventHub per Storm</span><span class="sxs-lookup"><span data-stu-id="13e46-164">Storm EventHub Reader Sample</span></span> |<span data-ttu-id="13e46-165">Come leggere da Hub eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="13e46-165">How to read from Azure Event Hubs.</span></span> |
| <span data-ttu-id="13e46-166">Esempio di writer EventHub per Storm</span><span class="sxs-lookup"><span data-stu-id="13e46-166">Storm EventHub Writer Sample</span></span> |<span data-ttu-id="13e46-167">Come scrivere in Hub eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="13e46-167">How to write to Azure Event Hubs.</span></span> |
| <span data-ttu-id="13e46-168">Esempio di lettore HBase per Storm</span><span class="sxs-lookup"><span data-stu-id="13e46-168">Storm HBase Reader Sample</span></span> |<span data-ttu-id="13e46-169">Come leggere da cluster HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="13e46-169">How to read from HBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="13e46-170">Esempio di writer HBase per Storm</span><span class="sxs-lookup"><span data-stu-id="13e46-170">Storm HBase Writer Sample</span></span> |<span data-ttu-id="13e46-171">Come scrivere in cluster HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="13e46-171">How to write to HBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="13e46-172">Esempio ibrido di Storm</span><span class="sxs-lookup"><span data-stu-id="13e46-172">Storm Hybrid Sample</span></span> |<span data-ttu-id="13e46-173">Come usare un componente Java</span><span class="sxs-lookup"><span data-stu-id="13e46-173">How to use a Java component.</span></span> |
| <span data-ttu-id="13e46-174">Esempio di Storm</span><span class="sxs-lookup"><span data-stu-id="13e46-174">Storm Sample</span></span> |<span data-ttu-id="13e46-175">Topologia di conteggio parole di base</span><span class="sxs-lookup"><span data-stu-id="13e46-175">A basic word count topology.</span></span> |

> [!WARNING]
> <span data-ttu-id="13e46-176">Non tutti i modelli funzionano con HDInsight basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="13e46-176">Not all templates will work with Linux-based HDInsight.</span></span> <span data-ttu-id="13e46-177">È possibile che i pacchetti NuGet usati dai modelli non siano compatibili con Mono.</span><span class="sxs-lookup"><span data-stu-id="13e46-177">Nuget packages used by the templates may not be compatible with Mono.</span></span> <span data-ttu-id="13e46-178">Verificare il documento sulla [compatibilità di Mono](http://www.mono-project.com/docs/about-mono/compatibility/) e usare [.NET Portability Analyzer](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) per identificare potenziali problemi.</span><span class="sxs-lookup"><span data-stu-id="13e46-178">Check the [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document and use the [.NET Portability Analyzer](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) to identify potential problems.</span></span>

<span data-ttu-id="13e46-179">Nelle procedure di questo documento viene usato il tipo di progetto Applicazione Storm di base per creare una topologia.</span><span class="sxs-lookup"><span data-stu-id="13e46-179">In the steps in this document, you use the basic Storm Application project type to create a topology.</span></span>

### <a name="hbase-templates-notes"></a><span data-ttu-id="13e46-180">Note sui modelli HBase</span><span class="sxs-lookup"><span data-stu-id="13e46-180">HBase templates notes</span></span>

<span data-ttu-id="13e46-181">I modelli di lettore e writer HBase usano l'API REST HBase al posto dell'API Java HBase per comunicare con un cluster HBase in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="13e46-181">The HBase reader and writer templates use the HBase REST API, not the HBase Java API, to communicate with an HBase on HDInsight cluster.</span></span>

### <a name="eventhub-templates-notes"></a><span data-ttu-id="13e46-182">Note sui modelli EventHub</span><span class="sxs-lookup"><span data-stu-id="13e46-182">EventHub templates notes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="13e46-183">Il componente spout EventHub basato su Java incluso nel modello di lettore EventHub non funziona con Storm in HDInsight versione 3.5 o successiva.</span><span class="sxs-lookup"><span data-stu-id="13e46-183">The Java-based EventHub spout component included with the EventHub Reader template may not work with Storm on HDInsight version 3.5 or later.</span></span> <span data-ttu-id="13e46-184">Una versione aggiornata di questo componente è disponibile in [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span><span class="sxs-lookup"><span data-stu-id="13e46-184">An updated version of this component is available at [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span></span>

<span data-ttu-id="13e46-185">Per una topologia di esempio che usa questo componente e funziona con Storm in HDInsight 3.5, vedere [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="13e46-185">For an example topology that uses this component and works with Storm on HDInsight 3.5, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

## <a name="create-a-c-topology"></a><span data-ttu-id="13e46-186">Creare una topologia C#</span><span class="sxs-lookup"><span data-stu-id="13e46-186">Create a C# topology</span></span>

1. <span data-ttu-id="13e46-187">Aprire Visual Studio, selezionare **File** > **Nuovo** e quindi **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="13e46-187">Open Visual Studio, select **File** > **New**, and then select **Project**.</span></span>

2. <span data-ttu-id="13e46-188">Nella finestra **Nuovo progetto** espandere **Modelli** > **installati** e selezionare **Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="13e46-188">From the **New Project** window, expand **Installed** > **Templates**, and select **Azure Data Lake**.</span></span> <span data-ttu-id="13e46-189">Dall'elenco dei modelli selezionare **Applicazione Storm**.</span><span class="sxs-lookup"><span data-stu-id="13e46-189">From the list of templates, select **Storm Application**.</span></span> <span data-ttu-id="13e46-190">Nella parte inferiore della schermata immettere **WordCount** come nome dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="13e46-190">At the bottom of the screen, enter **WordCount** as the name of the application.</span></span>

    ![Screenshot della finestra Nuovo progetto](./media/hdinsight-storm-develop-csharp-visual-studio-topology/new-project.png)

3. <span data-ttu-id="13e46-192">Dopo avere creato il progetto, si dovrebbe disporre dei file seguenti:</span><span class="sxs-lookup"><span data-stu-id="13e46-192">After you have created the project, you should have the following files:</span></span>

   * <span data-ttu-id="13e46-193">**Program.cs**: questo file definisce la topologia per il progetto.</span><span class="sxs-lookup"><span data-stu-id="13e46-193">**Program.cs**: This file defines the topology for your project.</span></span> <span data-ttu-id="13e46-194">Per impostazione predefinita viene creata una topologia predefinita costituita da uno spout e da un bolt.</span><span class="sxs-lookup"><span data-stu-id="13e46-194">A default topology that consists of one spout and one bolt is created by default.</span></span>

   * <span data-ttu-id="13e46-195">**Spout.cs**: spout di esempio che genera numeri casuali.</span><span class="sxs-lookup"><span data-stu-id="13e46-195">**Spout.cs**: An example spout that emits random numbers.</span></span>

   * <span data-ttu-id="13e46-196">**Bolt.cs**: bolt di esempio che tiene conto dei numeri generati dallo spout.</span><span class="sxs-lookup"><span data-stu-id="13e46-196">**Bolt.cs**: An example bolt that keeps a count of numbers emitted by the spout.</span></span>

     <span data-ttu-id="13e46-197">Quando si crea il progetto, NuGet scarica la versione più recente del [pacchetto SCP.NET](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span><span class="sxs-lookup"><span data-stu-id="13e46-197">When you create the project, NuGet downloads the latest [SCP.NET package](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span></span>

     [!INCLUDE [scp.net version important](../../includes/hdinsight-storm-scpdotnet-version.md)]

### <a name="implement-the-spout"></a><span data-ttu-id="13e46-198">Implementare lo spout</span><span class="sxs-lookup"><span data-stu-id="13e46-198">Implement the spout</span></span>

1. <span data-ttu-id="13e46-199">Aprire **Spout.cs**.</span><span class="sxs-lookup"><span data-stu-id="13e46-199">Open **Spout.cs**.</span></span> <span data-ttu-id="13e46-200">Gli spout vengono usati per leggere i dati in una topologia da un'origine esterna.</span><span class="sxs-lookup"><span data-stu-id="13e46-200">Spouts are used to read data in a topology from an external source.</span></span> <span data-ttu-id="13e46-201">Di seguito sono indicati i componenti principali di uno spout:</span><span class="sxs-lookup"><span data-stu-id="13e46-201">The main components for a spout are:</span></span>

   * <span data-ttu-id="13e46-202">**NextTuple**: chiamato da Storm quando allo spout è consentita la generazione di nuove tuple.</span><span class="sxs-lookup"><span data-stu-id="13e46-202">**NextTuple**: Called by Storm when the spout is allowed to emit new tuples.</span></span>

   * <span data-ttu-id="13e46-203">**Ack** (solo topologia transazionale): gestisce i messaggi di riconoscimento avviati da altri componenti della topologia per tuple inviate dallo spout.</span><span class="sxs-lookup"><span data-stu-id="13e46-203">**Ack** (transactional topology only): Handles acknowledgements initiated by other components in the topology for tuples sent from the spout.</span></span> <span data-ttu-id="13e46-204">Il riconoscimento di una tupla consente allo spout di sapere che tale tupla è stata elaborata correttamente dai componenti downstream.</span><span class="sxs-lookup"><span data-stu-id="13e46-204">Acknowledging a tuple lets the spout know that it was processed successfully by downstream components.</span></span>

   * <span data-ttu-id="13e46-205">**Fail** (solo topologia transazionale): gestisce tuple la cui elaborazione da parte di altri componenti della topologia ha avuto esito negativo.</span><span class="sxs-lookup"><span data-stu-id="13e46-205">**Fail** (transactional topology only): Handles tuples that are fail-processing other components in the topology.</span></span> <span data-ttu-id="13e46-206">L'implementazione di un metodo Fail consente di generare nuovamente la tupla in modo che sia possibile elaborarla di nuovo.</span><span class="sxs-lookup"><span data-stu-id="13e46-206">Implementing a Fail method allows you to re-emit the tuple so that it can be processed again.</span></span>

2. <span data-ttu-id="13e46-207">Sostituire il contenuto della classe **Spout** con il testo riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="13e46-207">Replace the contents of the **Spout** class with the following text.</span></span> <span data-ttu-id="13e46-208">Lo spout genera in modo casuale una frase nella topologia.</span><span class="sxs-lookup"><span data-stu-id="13e46-208">This spout randomly emits a sentence into the topology.</span></span>

    ```csharp
    private Context ctx;
    private Random r = new Random();
    string[] sentences = new string[] {
        "the cow jumped over the moon",
        "an apple a day keeps the doctor away",
        "four score and seven years ago",
        "snow white and the seven dwarfs",
        "i am at two with nature"
    };

    public Spout(Context ctx)
    {
        // Set the instance context
        this.ctx = ctx;

        Context.Logger.Info("Generator constructor called");

        // Declare Output schema
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // The schema for the default output stream is
        // a tuple that contains a string field
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(null, outputSchema));
    }

    // Get an instance of the spout
    public static Spout Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Spout(ctx);
    }

    public void NextTuple(Dictionary<string, Object> parms)
    {
        Context.Logger.Info("NextTuple enter");
        // The sentence to be emitted
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

### <a name="implement-the-bolts"></a><span data-ttu-id="13e46-209">Implementare i bolt</span><span class="sxs-lookup"><span data-stu-id="13e46-209">Implement the bolts</span></span>

1. <span data-ttu-id="13e46-210">Eliminare dal progetto il file **Bolt.cs** esistente.</span><span class="sxs-lookup"><span data-stu-id="13e46-210">Delete the existing **Bolt.cs** file from the project.</span></span>

2. <span data-ttu-id="13e46-211">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto e selezionare **Aggiungi** > **Nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="13e46-211">In **Solution Explorer**, right-click the project, and select **Add** > **New item**.</span></span> <span data-ttu-id="13e46-212">Selezionare **Storm Bolt** dall'elenco e immettere **Splitter.cs** come nome.</span><span class="sxs-lookup"><span data-stu-id="13e46-212">From the list, select **Storm Bolt**, and enter **Splitter.cs** as the name.</span></span> <span data-ttu-id="13e46-213">Ripetere il processo per creare un secondo bolt denominato **Counter.cs**.</span><span class="sxs-lookup"><span data-stu-id="13e46-213">Repeat this process to create a second bolt named **Counter.cs**.</span></span>

   * <span data-ttu-id="13e46-214">**Splitter.cs**: implementa un bolt che divide le frasi in singole parole e crea un nuovo flusso di parole.</span><span class="sxs-lookup"><span data-stu-id="13e46-214">**Splitter.cs**: Implements a bolt that splits sentences into individual words, and emits a new stream of words.</span></span>

   * <span data-ttu-id="13e46-215">**Counter.cs**: implementa un bolt che conta ogni parola e genera un nuovo flusso di parole con il numero di occorrenze di ciascuna di esse.</span><span class="sxs-lookup"><span data-stu-id="13e46-215">**Counter.cs**: Implements a bolt that counts each word, and emits a new stream of words and the count for each word.</span></span>

     > [!NOTE]
     > <span data-ttu-id="13e46-216">I bolt sopra descritti eseguono operazioni di lettura e scrittura nei flussi. È tuttavia possibile usare un bolt per comunicare con origini quali un database o un servizio.</span><span class="sxs-lookup"><span data-stu-id="13e46-216">These bolts read and write to streams, but you can also use a bolt to communicate with sources such as a database or service.</span></span>

3. <span data-ttu-id="13e46-217">Aprire **Splitter.cs**.</span><span class="sxs-lookup"><span data-stu-id="13e46-217">Open **Splitter.cs**.</span></span> <span data-ttu-id="13e46-218">Per impostazione predefinita, dispone soltanto del metodo **Execute**.</span><span class="sxs-lookup"><span data-stu-id="13e46-218">It has only one method by default: **Execute**.</span></span> <span data-ttu-id="13e46-219">Il metodo Execute viene chiamato quando il bolt riceve una tupla da elaborare.</span><span class="sxs-lookup"><span data-stu-id="13e46-219">The Execute method is called when the bolt receives a tuple for processing.</span></span> <span data-ttu-id="13e46-220">È possibile leggere ed elaborare tuple in ingresso e generare tuple in uscita.</span><span class="sxs-lookup"><span data-stu-id="13e46-220">Here, you can read and process incoming tuples, and emit outbound tuples.</span></span>

4. <span data-ttu-id="13e46-221">Sostituire il contenuto della classe **Splitter** con il codice riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="13e46-221">Replace the contents of the **Splitter** class with the following code:</span></span>

    ```csharp
    private Context ctx;

    // Constructor
    public Splitter(Context ctx)
    {
        Context.Logger.Info("Splitter constructor called");
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // Input contains a tuple with a string field (the sentence)
        inputSchema.Add("default", new List<Type>() { typeof(string) });
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // Outbound contains a tuple with a string field (the word)
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance of the bolt
    public static Splitter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Splitter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get the sentence from the tuple
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

5. <span data-ttu-id="13e46-222">Aprire **Counter.cs** e sostituire il contenuto della classe con quanto riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="13e46-222">Open **Counter.cs**, and replace the class contents with the following:</span></span>

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
        // A tuple containing a string field - the word
        inputSchema.Add("default", new List<Type>() { typeof(string) });

        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string and integer field - the word and the word count
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

        // Get the word from the tuple
        string word = tuple.GetString(0);
        // Do we already have an entry for the word in the dictionary?
        // If no, create one with a count of 0
        int count = counts.ContainsKey(word) ? counts[word] : 0;
        // Increment the count
        count++;
        // Update the count in the dictionary
        counts[word] = count;

        Context.Logger.Info("Emit: {0}, count: {1}", word, count);
        // Emit the word and count information
        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new List<SCPTuple> { tuple }, new Values(word, count));
        Context.Logger.Info("Execute exit");
    }
    ```

### <a name="define-the-topology"></a><span data-ttu-id="13e46-223">Definire la topologia</span><span class="sxs-lookup"><span data-stu-id="13e46-223">Define the topology</span></span>

<span data-ttu-id="13e46-224">Gli spout e i bolt vengono disposti in un grafico che definisce i flussi di dati tra i componenti.</span><span class="sxs-lookup"><span data-stu-id="13e46-224">Spouts and bolts are arranged in a graph, which defines how the data flows between components.</span></span> <span data-ttu-id="13e46-225">Di seguito è riportato il grafico relativo alla topologia in oggetto:</span><span class="sxs-lookup"><span data-stu-id="13e46-225">For this topology, the graph is as follows:</span></span>

![Diagramma della disposizione degli elementi](./media/hdinsight-storm-develop-csharp-visual-studio-topology/wordcount-topology.png)

<span data-ttu-id="13e46-227">Lo spout genera frasi, che vengono quindi distribuite a istanze del bolt Splitter.</span><span class="sxs-lookup"><span data-stu-id="13e46-227">Sentences are emitted from the spout, and are distributed to instances of the Splitter bolt.</span></span> <span data-ttu-id="13e46-228">Il bolt Splitter suddivide le frasi in parole, che vengono quindi distribuite al bolt Counter.</span><span class="sxs-lookup"><span data-stu-id="13e46-228">The Splitter bolt breaks the sentences into words, which are distributed to the Counter bolt.</span></span>

<span data-ttu-id="13e46-229">Poiché il conteggio delle parole viene mantenuto in locale nell'istanza del bolt Counter, si vuole assicurare che parole specifiche vengano indirizzate alla stessa istanza del bolt Counter.</span><span class="sxs-lookup"><span data-stu-id="13e46-229">Because word count is held locally in the Counter instance, we want to make sure that specific words flow to the same Counter bolt instance.</span></span> <span data-ttu-id="13e46-230">Ogni istanza tiene traccia di una parola specifica.</span><span class="sxs-lookup"><span data-stu-id="13e46-230">Each instance keeps track of specific words.</span></span> <span data-ttu-id="13e46-231">Poiché il bolt Splitter non gestisce lo stato, non è importante stabilire quale istanza dello splitter riceve quale frase.</span><span class="sxs-lookup"><span data-stu-id="13e46-231">Since the Splitter bolt maintains no state, it really doesn't matter which instance of the splitter receives which sentence.</span></span>

<span data-ttu-id="13e46-232">Aprire **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="13e46-232">Open **Program.cs**.</span></span> <span data-ttu-id="13e46-233">In questo caso il metodo importante è **GetTopologyBuilder**, usato per definire la topologia inviata a Storm.</span><span class="sxs-lookup"><span data-stu-id="13e46-233">The important method is **GetTopologyBuilder**, which is used to define the topology that is submitted to Storm.</span></span> <span data-ttu-id="13e46-234">Sostituire il contenuto di **GetTopologyBuilder** con il seguente codice per implementare la topologia descritta in precedenza:</span><span class="sxs-lookup"><span data-stu-id="13e46-234">Replace the contents of **GetTopologyBuilder** with the following code to implement the topology described previously:</span></span>

```csharp
// Create a new topology named 'WordCount'
TopologyBuilder topologyBuilder = new TopologyBuilder("WordCount" + DateTime.Now.ToString("yyyyMMddHHmmss"));

// Add the spout to the topology.
// Name the component 'sentences'
// Name the field that is emitted as 'sentence'
topologyBuilder.SetSpout(
    "sentences",
    Spout.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"sentence"}}
    },
    1);
// Add the splitter bolt to the topology.
// Name the component 'splitter'
// Name the field that is emitted 'word'
// Use suffleGrouping to distribute incoming tuples
//   from the 'sentences' spout across instances
//   of the splitter
topologyBuilder.SetBolt(
    "splitter",
    Splitter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word"}}
    },
    1).shuffleGrouping("sentences");

// Add the counter bolt to the topology.
// Name the component 'counter'
// Name the fields that are emitted 'word' and 'count'
// Use fieldsGrouping to ensure that tuples are routed
//   to counter instances based on the contents of field
//   position 0 (the word). This could also have been
//   List<string>(){"word"}.
//   This ensures that the word 'jumped', for example, will always
//   go to the same instance
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

## <a name="submit-the-topology"></a><span data-ttu-id="13e46-235">Inviare la topologia</span><span class="sxs-lookup"><span data-stu-id="13e46-235">Submit the topology</span></span>

1. <span data-ttu-id="13e46-236">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto e selezionare **Submit to Storm on HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="13e46-236">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="13e46-237">Se richiesto, immettere le credenziali per la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="13e46-237">If prompted, enter the credentials for your Azure subscription.</span></span> <span data-ttu-id="13e46-238">Se si dispone di più di una sottoscrizione, accedere a quella che contiene il cluster Storm in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="13e46-238">If you have more than one subscription, sign in to the one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="13e46-239">Selezionare il cluster Storm in HDInsight dall'elenco a discesa **Storm Cluster** e quindi selezionare **Submit**.</span><span class="sxs-lookup"><span data-stu-id="13e46-239">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="13e46-240">È possibile verificare se l'invio è riuscito o meno usando la finestra **Output** .</span><span class="sxs-lookup"><span data-stu-id="13e46-240">You can monitor if the submission is successful by using the **Output** window.</span></span>

3. <span data-ttu-id="13e46-241">Dopo che la topologia è stata inviata correttamente, verrà visualizzato l'elenco **Storm Topologies** relativo al cluster.</span><span class="sxs-lookup"><span data-stu-id="13e46-241">When the topology has been successfully submitted, the **Storm Topologies** for the cluster should appear.</span></span> <span data-ttu-id="13e46-242">Selezionare dall'elenco la topologia **WordCount** per visualizzare le informazioni sulla topologia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="13e46-242">Select the **WordCount** topology from the list to view information about the running topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="13e46-243">È inoltre possibile visualizzare le **topologie Storm**  da **Esplora Server**.</span><span class="sxs-lookup"><span data-stu-id="13e46-243">You can also view **Storm Topologies** from **Server Explorer**.</span></span> <span data-ttu-id="13e46-244">Espandere **Azure** > **HDInsight**, fare clic con il pulsante destro del mouse sul cluster Storm in HDInsight e quindi selezionare **Visualizza topologie Storm**.</span><span class="sxs-lookup"><span data-stu-id="13e46-244">Expand **Azure** > **HDInsight**, right-click a Storm on HDInsight cluster, and then select **View Storm Topologies**.</span></span>

    <span data-ttu-id="13e46-245">Per visualizzare informazioni sui componenti della topologia, fare doppio clic sul componente nel diagramma.</span><span class="sxs-lookup"><span data-stu-id="13e46-245">To view information about the components in the topology, double-click the component in the diagram.</span></span>

4. <span data-ttu-id="13e46-246">Nella visualizzazione **Topology Summary** (Riepilogo topologie) selezionare **Kill** (Arresta) per arrestare la topologia.</span><span class="sxs-lookup"><span data-stu-id="13e46-246">From the **Topology Summary** view, click **Kill** to stop the topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="13e46-247">Le topologie Storm continuano l'esecuzione fino a quando non vengono disattivate o il cluster non viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="13e46-247">Storm topologies continue to run until they are deactivated, or the cluster is deleted.</span></span>

## <a name="transactional-topology"></a><span data-ttu-id="13e46-248">Topologia transazionale</span><span class="sxs-lookup"><span data-stu-id="13e46-248">Transactional topology</span></span>

<span data-ttu-id="13e46-249">La topologia descritta in precedenza è di tipo non transazionale.</span><span class="sxs-lookup"><span data-stu-id="13e46-249">The previous topology is non-transactional.</span></span> <span data-ttu-id="13e46-250">I componenti della topologia non implementano funzionalità di ripetizione dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="13e46-250">The components in the topology do not implement functionality to replaying messages.</span></span> <span data-ttu-id="13e46-251">Per un esempio di topologia transazionale, creare un progetto e selezionare **Storm Sample** come tipo di progetto.</span><span class="sxs-lookup"><span data-stu-id="13e46-251">For an example of a transactional topology, create a project and select **Storm Sample** as the project type.</span></span>

<span data-ttu-id="13e46-252">Le topologie transazionali implementano le operazioni seguenti per supportare la ripetizione dei dati:</span><span class="sxs-lookup"><span data-stu-id="13e46-252">Transactional topologies implement the following to support replay of data:</span></span>

* <span data-ttu-id="13e46-253">**Memorizzazione dei metadati nella cache**: lo spout deve memorizzare i metadati relativi ai dati generati, in modo che, in caso di errore, questi ultimi possano essere recuperati e generati nuovamente.</span><span class="sxs-lookup"><span data-stu-id="13e46-253">**Metadata caching**: The spout must store metadata about the data emitted, so that the data can be retrieved and emitted again if a failure occurs.</span></span> <span data-ttu-id="13e46-254">Poiché l'esempio genera una quantità limitata di dati, i dati non elaborati di ogni tupla vengono archiviati in un dizionario per la ripetizione.</span><span class="sxs-lookup"><span data-stu-id="13e46-254">Because the data emitted by the sample is small, the raw data for each tuple is stored in a dictionary for replay.</span></span>

* <span data-ttu-id="13e46-255">**Ack**: ogni bolt della topologia può chiamare `this.ctx.Ack(tuple)` per confermare che ha elaborato correttamente la tupla.</span><span class="sxs-lookup"><span data-stu-id="13e46-255">**Ack**: Each bolt in the topology can call `this.ctx.Ack(tuple)` to acknowledge that it has successfully processed a tuple.</span></span> <span data-ttu-id="13e46-256">Dopo che tutti i bolt hanno riconosciuto la tupla, viene richiamato il metodo `Ack` dello spout.</span><span class="sxs-lookup"><span data-stu-id="13e46-256">When all bolts have acked the tuple, the `Ack` method of the spout is invoked.</span></span> <span data-ttu-id="13e46-257">Il metodo `Ack` consente allo spout di rimuovere i dati memorizzati nella cache per la ripetizione.</span><span class="sxs-lookup"><span data-stu-id="13e46-257">The `Ack` method allows the spout to remove data that was cached for replay.</span></span>

* <span data-ttu-id="13e46-258">**Errore**: ciascun bolt può chiamare `this.ctx.Fail(tuple)` per indicare che l'elaborazione di una tupla non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="13e46-258">**Fail**: Each bolt can call `this.ctx.Fail(tuple)` to indicate that processing has failed for a tuple.</span></span> <span data-ttu-id="13e46-259">L'errore viene propagato al metodo `Fail` dello spout, dove la tupla può essere ripetuta usando i metadati memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="13e46-259">The failure propagates to the `Fail` method of the spout, where the tuple can be replayed by using cached metadata.</span></span>

* <span data-ttu-id="13e46-260">**ID sequenza**: quando si genera una tupla, è possibile specificare un ID sequenza univoco.</span><span class="sxs-lookup"><span data-stu-id="13e46-260">**Sequence ID**: When emitting a tuple, a unique sequence ID can be specified.</span></span> <span data-ttu-id="13e46-261">Questo valore identifica la tupla per la ripetizione dell'elaborazione (Riconoscimento ed Errore).</span><span class="sxs-lookup"><span data-stu-id="13e46-261">This value identifies the tuple for replay (Ack and Fail) processing.</span></span> <span data-ttu-id="13e46-262">Ad esempio, quando genera i dati, lo spout presente nel progetto **Storm Sample** usa il codice riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="13e46-262">For example, the spout in the **Storm Sample** project uses the following when emitting data:</span></span>

        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), lastSeqId);

    <span data-ttu-id="13e46-263">Questo codice genera una tupla contenente una frase indirizzata al flusso predefinito, con il valore di ID sequenza contenuto in **lastSeqId**.</span><span class="sxs-lookup"><span data-stu-id="13e46-263">This code emits a tuple that contains a sentence to the default stream, with the sequence ID value contained in **lastSeqId**.</span></span> <span data-ttu-id="13e46-264">Ai fini di questo esempio, **lastSeqId** viene incrementato per ogni tupla generata.</span><span class="sxs-lookup"><span data-stu-id="13e46-264">For this example, **lastSeqId** is incremented for every tuple emitted.</span></span>

<span data-ttu-id="13e46-265">Come dimostrato nel progetto **Storm Sample**, è possibile specificare in fase di esecuzione, in base alla configurazione, se un componente è transazionale o meno.</span><span class="sxs-lookup"><span data-stu-id="13e46-265">As demonstrated in the **Storm Sample** project, whether a component is transactional can be set at runtime, based on configuration.</span></span>

## <a name="hybrid-topology-with-c-and-java"></a><span data-ttu-id="13e46-266">Topologia ibrida con C# e Java</span><span class="sxs-lookup"><span data-stu-id="13e46-266">Hybrid topology with C# and Java</span></span>

<span data-ttu-id="13e46-267">Gli strumenti Data Lake per Visual Studio possono essere usati anche per creare topologie ibride, dove alcuni componenti sono in C# e altri in Java.</span><span class="sxs-lookup"><span data-stu-id="13e46-267">You can also use Data Lake tools for Visual Studio to create hybrid topologies, where some components are C# and others are Java.</span></span>

<span data-ttu-id="13e46-268">Per un esempio di topologia ibrida, creare un progetto e selezionare **Storm Hybrid Sample**.</span><span class="sxs-lookup"><span data-stu-id="13e46-268">For an example of a hybrid topology, create a project and select **Storm Hybrid Sample**.</span></span> <span data-ttu-id="13e46-269">Questo tipo di esempio illustra i concetti seguenti:</span><span class="sxs-lookup"><span data-stu-id="13e46-269">This sample type demonstrates the following concepts:</span></span>

* <span data-ttu-id="13e46-270">**Java spout** e **C# bolt**: definiti in **HybridTopology_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="13e46-270">**Java spout** and **C# bolt**: Defined in **HybridTopology_javaSpout_csharpBolt**.</span></span>

    * <span data-ttu-id="13e46-271">Una versione transazionale è definita in **HybridTopologyTx_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="13e46-271">A transactional version is defined in **HybridTopologyTx_javaSpout_csharpBolt**.</span></span>

* <span data-ttu-id="13e46-272">**C# spout** e **Java bolt**: definiti in **HybridTopology_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="13e46-272">**C# spout** and **Java bolt**: Defined in **HybridTopology_csharpSpout_javaBolt**.</span></span>

    * <span data-ttu-id="13e46-273">Una versione transazionale è definita in **HybridTopologyTx_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="13e46-273">A transactional version is defined in **HybridTopologyTx_csharpSpout_javaBolt**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="13e46-274">Questa versione illustra anche come usare codice Clojure da un file di testo come componente Java.</span><span class="sxs-lookup"><span data-stu-id="13e46-274">This version also demonstrates how to use Clojure code from a text file as a Java component.</span></span>


<span data-ttu-id="13e46-275">Quando si invia il progetto, per passare da una topologia all'altra spostare semplicemente l'istruzione `[Active(true)]` nella topologia che si desidera usare prima di effettuare l'invio al cluster.</span><span class="sxs-lookup"><span data-stu-id="13e46-275">To switch the topology that is used when the project is submitted, simply move the `[Active(true)]` statement to the topology you want to use, before submitting it to the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="13e46-276">Tutti i file Java necessari vengono forniti come parte di questo progetto nella cartella **JavaDependency** .</span><span class="sxs-lookup"><span data-stu-id="13e46-276">All the Java files that are required are provided as part of this project in the **JavaDependency** folder.</span></span>

<span data-ttu-id="13e46-277">Quando si crea e si invia una topologia ibrida, tenere presente quanto riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="13e46-277">Consider the following when you are creating and submitting a hybrid topology:</span></span>

* <span data-ttu-id="13e46-278">È necessario usare **JavaComponentConstructor** per creare un'istanza della classe Java per uno spout o un bolt.</span><span class="sxs-lookup"><span data-stu-id="13e46-278">You must use **JavaComponentConstructor** to create an instance of the Java class for a spout or bolt.</span></span>

* <span data-ttu-id="13e46-279">È consigliabile usare **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** per serializzare i dati dentro e fuori i componenti Java da oggetti Java a JSON.</span><span class="sxs-lookup"><span data-stu-id="13e46-279">You should use **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** to serialize data into or out of Java components from Java objects to JSON.</span></span>

* <span data-ttu-id="13e46-280">Durante l'invio della topologia al server, è necessario usare l'opzione **Configurazioni aggiuntive** per specificare i **percorsi dei file Java**.</span><span class="sxs-lookup"><span data-stu-id="13e46-280">When submitting the topology to the server, you must use the **Additional configurations** option to specify the **Java File paths**.</span></span> <span data-ttu-id="13e46-281">Il percorso specificato deve corrispondere alla directory contenente i file con estensione jar in cui sono presenti le classi Java.</span><span class="sxs-lookup"><span data-stu-id="13e46-281">The path specified should be the directory that contains the JAR files that contain your Java classes.</span></span>

### <a name="azure-event-hubs"></a><span data-ttu-id="13e46-282">Hub eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="13e46-282">Azure Event Hubs</span></span>

<span data-ttu-id="13e46-283">La versione 0.9.4.203 di SCP.Net introduce una nuova classe e un nuovo metodo appositamente da usare con lo spout dell'hub eventi (uno spout Java che legge dall'hub eventi).</span><span class="sxs-lookup"><span data-stu-id="13e46-283">SCP.NET version 0.9.4.203 introduces a new class and method specifically for working with the Event Hub spout (a Java spout that reads from Event Hubs).</span></span> <span data-ttu-id="13e46-284">Quando si crea una topologia che usa uno spout dell'hub eventi, usare i metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="13e46-284">When you create a topology that uses an Event Hub spout, use the following methods:</span></span>

* <span data-ttu-id="13e46-285">Classe **EventHubSpoutConfig**: crea un oggetto che contiene la configurazione per il componente spout.</span><span class="sxs-lookup"><span data-stu-id="13e46-285">**EventHubSpoutConfig** class: Creates an object that contains the configuration for the spout component.</span></span>

* <span data-ttu-id="13e46-286">Metodo **TopologyBuilder.SetEventHubSpout**: aggiunge il componente spout dell'hub eventi alla topologia.</span><span class="sxs-lookup"><span data-stu-id="13e46-286">**TopologyBuilder.SetEventHubSpout** method: Adds the Event Hub spout component to the topology.</span></span>

> [!NOTE]
> <span data-ttu-id="13e46-287">È comunque necessario usare **CustomizedInteropJSONSerializer** per serializzare i dati generati dallo spout.</span><span class="sxs-lookup"><span data-stu-id="13e46-287">You must still use the **CustomizedInteropJSONSerializer** to serialize data produced by the spout.</span></span>

## <span data-ttu-id="13e46-288"><a id="configurationmanager"></a>Usare ConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="13e46-288"><a id="configurationmanager"></a>Use ConfigurationManager</span></span>

<span data-ttu-id="13e46-289">Non usare **ConfigurationManager** per recuperare i valori di configurazione dai componenti bolt e spout.</span><span class="sxs-lookup"><span data-stu-id="13e46-289">Don't use **ConfigurationManager** to retrieve configuration values from bolt and spout components.</span></span> <span data-ttu-id="13e46-290">Questa operazione può generare un'eccezione del puntatore null.</span><span class="sxs-lookup"><span data-stu-id="13e46-290">Doing so can cause a null pointer exception.</span></span> <span data-ttu-id="13e46-291">La configurazione per il progetto viene invece passata nella topologia Storm come coppia chiave/valore nel contesto della topologia.</span><span class="sxs-lookup"><span data-stu-id="13e46-291">Instead, the configuration for your project is passed into the Storm topology as a key and value pair in the topology context.</span></span> <span data-ttu-id="13e46-292">Ogni componente basato sui valori di configurazione deve recuperarli dal contesto durante l'inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="13e46-292">Each component that relies on configuration values must retrieve them from the context during initialization.</span></span>

<span data-ttu-id="13e46-293">Il codice seguente illustra come recuperare questi valori:</span><span class="sxs-lookup"><span data-stu-id="13e46-293">The following code demonstrates how to retrieve these values:</span></span>

```csharp
public class MyComponent : ISCPBolt
{
    // To hold configuration information loaded from context
    Configuration configuration;
    ...
    public MyComponent(Context ctx, Dictionary<string, Object> parms)
    {
        // Save a copy of the context for this component instance
        this.ctx = ctx;
        // If it exists, load the configuration for the component
        if(parms.ContainsKey(Constants.USER_CONFIG))
        {
            this.configuration = parms[Constants.USER_CONFIG] as System.Configuration.Configuration;
        }
        // Retrieve the value of "Foo" from configuration
        var foo = this.configuration.AppSettings.Settings["Foo"].Value;
    }
    ...
}
```

<span data-ttu-id="13e46-294">Se si usa un metodo `Get` per restituire un'istanza del componente, è necessario assicurarsi che sia il parametro `Context` che il parametro `Dictionary<string, Object>` vengano passati al costruttore.</span><span class="sxs-lookup"><span data-stu-id="13e46-294">If you use a `Get` method to return an instance of your component, you must ensure that it passes both the `Context` and `Dictionary<string, Object>` parameters to the constructor.</span></span> <span data-ttu-id="13e46-295">L'esempio seguente illustra un metodo `Get` di base che passa in modo corretto questi valori:</span><span class="sxs-lookup"><span data-stu-id="13e46-295">The following example is a basic `Get` method that properly passes these values:</span></span>

```csharp
public static MyComponent Get(Context ctx, Dictionary<string, Object> parms)
{
    return new MyComponent(ctx, parms);
}
```

## <a name="how-to-update-scpnet"></a><span data-ttu-id="13e46-296">Come aggiornare SCP.NET</span><span class="sxs-lookup"><span data-stu-id="13e46-296">How to update SCP.NET</span></span>

<span data-ttu-id="13e46-297">Le versioni recenti di SCP.NET supportano l'aggiornamento del pacchetto tramite NuGet.</span><span class="sxs-lookup"><span data-stu-id="13e46-297">Recent releases of SCP.NET support package upgrade through NuGet.</span></span> <span data-ttu-id="13e46-298">Quando è disponibile un nuovo aggiornamento, si riceve una notifica.</span><span class="sxs-lookup"><span data-stu-id="13e46-298">When a new update is available, you receive an upgrade notification.</span></span> <span data-ttu-id="13e46-299">Per controllare manualmente la disponibilità di un aggiornamento, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="13e46-299">To manually check for an upgrade, follow these steps:</span></span>

1. <span data-ttu-id="13e46-300">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="13e46-300">In **Solution Explorer**, right-click the project, and select **Manage NuGet Packages**.</span></span>

2. <span data-ttu-id="13e46-301">In Gestione pacchetti selezionare **Aggiornamenti**.</span><span class="sxs-lookup"><span data-stu-id="13e46-301">From the package manager, select **Updates**.</span></span> <span data-ttu-id="13e46-302">Se un aggiornamento è disponibile, è presente nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="13e46-302">If an update is available, it is listed.</span></span> <span data-ttu-id="13e46-303">Fare clic sul pulsante **Aggiorna** relativo al pacchetto per installarlo.</span><span class="sxs-lookup"><span data-stu-id="13e46-303">Click **Update** for the package to install it.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="13e46-304">Se il progetto è stato creato con una versione precedente di SCP.NET che non usa NuGet, è necessario seguire questa procedura per effettuare l'aggiornamento a una nuova versione:</span><span class="sxs-lookup"><span data-stu-id="13e46-304">If your project was created with an earlier version of SCP.NET that did not use NuGet, you must perform the following steps to update to a newer version:</span></span>
>
> 1. <span data-ttu-id="13e46-305">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="13e46-305">In **Solution Explorer**, right-click the project, and select **Manage NuGet Packages**.</span></span>
> 2. <span data-ttu-id="13e46-306">Nel campo **Cerca** cercare **Microsoft.SCP.Net.SDK** e quindi aggiungerlo al progetto.</span><span class="sxs-lookup"><span data-stu-id="13e46-306">Using the **Search** field, search for, and then add, **Microsoft.SCP.Net.SDK** to the project.</span></span>

## <a name="troubleshoot-common-issues-with-topologies"></a><span data-ttu-id="13e46-307">Risoluzione di problemi comuni con le topologie</span><span class="sxs-lookup"><span data-stu-id="13e46-307">Troubleshoot common issues with topologies</span></span>

### <a name="null-pointer-exceptions"></a><span data-ttu-id="13e46-308">Eccezioni del puntatore null</span><span class="sxs-lookup"><span data-stu-id="13e46-308">Null pointer exceptions</span></span>

<span data-ttu-id="13e46-309">Quando si usa una topologia C# con un cluster HDInsight basato su Linux, i componenti bolt e spout che fanno uso di **ConfigurationManager** per leggere le impostazioni di configurazione in fase di esecuzione potrebbero restituire eccezioni del puntatore null.</span><span class="sxs-lookup"><span data-stu-id="13e46-309">When you are using a C# topology with a Linux-based HDInsight cluster, bolt and spout components that use **ConfigurationManager** to read configuration settings at runtime may return null pointer exceptions.</span></span>

<span data-ttu-id="13e46-310">La configurazione per il progetto viene passata nella topologia Storm come coppia chiave/valore nel contesto della topologia</span><span class="sxs-lookup"><span data-stu-id="13e46-310">The configuration for your project is passed into the Storm topology as a key and value pair in the topology context.</span></span> <span data-ttu-id="13e46-311">e può essere recuperata dall'oggetto dizionario passato ai componenti quando questi vengono inizializzati.</span><span class="sxs-lookup"><span data-stu-id="13e46-311">It can be retrieved from the dictionary object that is passed to your components when they are initialized.</span></span>

<span data-ttu-id="13e46-312">Per altre informazioni, vedere la sezione [Uso di ConfigurationManager](#configurationmanager) in questo documento.</span><span class="sxs-lookup"><span data-stu-id="13e46-312">For more information, see the [ConfigurationManager](#configurationmanager) section of this document.</span></span>

### <a name="systemtypeloadexception"></a><span data-ttu-id="13e46-313">System.TypeLoadException</span><span class="sxs-lookup"><span data-stu-id="13e46-313">System.TypeLoadException</span></span>

<span data-ttu-id="13e46-314">Quando si usa una topologia C# con un cluster HDInsight basato su Linux, è possibile riscontrare l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="13e46-314">When you are using a C# topology with a Linux-based HDInsight cluster, you may encounter the following error:</span></span>

    System.TypeLoadException: Failure has occurred while loading a type.

<span data-ttu-id="13e46-315">Questo errore si verifica quando si usa un file binario non compatibile con la versione di .NET supportata da Mono.</span><span class="sxs-lookup"><span data-stu-id="13e46-315">This error occurs when you use a binary that is not compatible with the version of .NET that Mono supports.</span></span>

<span data-ttu-id="13e46-316">Per i cluster HDInsight basati su Linux, è necessario verificare che il progetto usi file binari compilati per .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="13e46-316">For Linux-based HDInsight clusters, make sure that your project uses binaries compiled for .NET 4.5.</span></span>

### <a name="test-a-topology-locally"></a><span data-ttu-id="13e46-317">Testare la topologia in locale</span><span class="sxs-lookup"><span data-stu-id="13e46-317">Test a topology locally</span></span>

<span data-ttu-id="13e46-318">Anche se la distribuzione di una topologia a un cluster è un'operazione semplice, in alcuni casi può essere necessario eseguire un test in locale.</span><span class="sxs-lookup"><span data-stu-id="13e46-318">Although it is easy to deploy a topology to a cluster, in some cases, you may need to test a topology locally.</span></span> <span data-ttu-id="13e46-319">Per eseguire e testare la topologia di esempio descritta in questa esercitazione nell'ambiente di sviluppo locale, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="13e46-319">Use the following steps to run and test the example topology in this tutorial locally in your development environment.</span></span>

> [!WARNING]
> <span data-ttu-id="13e46-320">I test locali funzionano solo per topologie di base di tipo C#.</span><span class="sxs-lookup"><span data-stu-id="13e46-320">Local testing only works for basic, C#-only topologies.</span></span> <span data-ttu-id="13e46-321">Non è possibile usare il test locale per topologie ibride o topologie che impiegano più flussi.</span><span class="sxs-lookup"><span data-stu-id="13e46-321">You cannot use local testing for hybrid topologies or topologies that use multiple streams.</span></span>

1. <span data-ttu-id="13e46-322">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto, quindi scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="13e46-322">In **Solution Explorer**, right-click the project, and select **Properties**.</span></span> <span data-ttu-id="13e46-323">Nelle proprietà del progetto impostare **Tipo di output** su **Applicazione console**.</span><span class="sxs-lookup"><span data-stu-id="13e46-323">In the project properties, change the **Output type** to **Console Application**.</span></span>

    ![Screenshot delle proprietà di progetto, con il tipo di Output evidenziato](./media/hdinsight-storm-develop-csharp-visual-studio-topology/outputtype.png)

   > [!NOTE]
   > <span data-ttu-id="13e46-325">Ricordarsi di reimpostare **Tipo di output** su **Libreria di classi** prima di distribuire la topologia a un cluster.</span><span class="sxs-lookup"><span data-stu-id="13e46-325">Remember to change the **Output type** back to **Class Library** before you deploy the topology to a cluster.</span></span>

2. <span data-ttu-id="13e46-326">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto e quindi selezionare **Aggiungi** > **Nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="13e46-326">In **Solution Explorer**, right-click the project, and then select **Add** > **New Item**.</span></span> <span data-ttu-id="13e46-327">Selezionare **Classe** e immettere **LocalTest.cs** come nome della classe.</span><span class="sxs-lookup"><span data-stu-id="13e46-327">Select **Class**, and enter **LocalTest.cs** as the class name.</span></span> <span data-ttu-id="13e46-328">Infine fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="13e46-328">Finally, click **Add**.</span></span>

3. <span data-ttu-id="13e46-329">Aprire **LocalTest.cs** e aggiungere all'inizio l'istruzione **using** seguente:</span><span class="sxs-lookup"><span data-stu-id="13e46-329">Open **LocalTest.cs**, and add the following **using** statement at the top:</span></span>

    ```csharp
    using Microsoft.SCP;
    ```

4. <span data-ttu-id="13e46-330">Usare il codice seguente come contenuto della classe **LocalTest**:</span><span class="sxs-lookup"><span data-stu-id="13e46-330">Use the following code as the contents of the **LocalTest** class:</span></span>

    ```csharp
    // Drives the topology components
    public void RunTestCase()
    {
        // An empty dictionary for use when creating components
        Dictionary<string, Object> emptyDictionary = new Dictionary<string, object>();

        #region Test the spout
        {
            Console.WriteLine("Starting spout");
            // LocalContext is a local-mode context that can be used to initialize
            // components in the development environment.
            LocalContext spoutCtx = LocalContext.Get();
            // Get a new instance of the spout, using the local context
            Spout sentences = Spout.Get(spoutCtx, emptyDictionary);

            // Emit 10 tuples
            for (int i = 0; i < 10; i++)
            {
                sentences.NextTuple(emptyDictionary);
            }
            // Use LocalContext to persist the data stream to file
            spoutCtx.WriteMsgQueueToFile("sentences.txt");
            Console.WriteLine("Spout finished");
        }
        #endregion

        #region Test the splitter bolt
        {
            Console.WriteLine("Starting splitter bolt");
            // LocalContext is a local-mode context that can be used to initialize
            // components in the development environment.
            LocalContext splitterCtx = LocalContext.Get();
            // Get a new instance of the bolt
            Splitter splitter = Splitter.Get(splitterCtx, emptyDictionary);

            // Set the data stream to the data created by the spout
            splitterCtx.ReadFromFileToMsgQueue("sentences.txt");
            // Get a batch of tuples from the stream
            List<SCPTuple> batch = splitterCtx.RecvFromMsgQueue();
            // Process each tuple in the batch
            foreach (SCPTuple tuple in batch)
            {
                splitter.Execute(tuple);
            }
            // Use LocalContext to persist the data stream to file
            splitterCtx.WriteMsgQueueToFile("splitter.txt");
            Console.WriteLine("Splitter bolt finished");
        }
        #endregion

        #region Test the counter bolt
        {
            Console.WriteLine("Starting counter bolt");
            // LocalContext is a local-mode context that can be used to initialize
            // components in the development environment.
            LocalContext counterCtx = LocalContext.Get();
            // Get a new instance of the bolt
            Counter counter = Counter.Get(counterCtx, emptyDictionary);

            // Set the data stream to the data created by splitter bolt
            counterCtx.ReadFromFileToMsgQueue("splitter.txt");
            // Get a batch of tuples from the stream
            List<SCPTuple> batch = counterCtx.RecvFromMsgQueue();
            // Process each tuple in the batch
            foreach (SCPTuple tuple in batch)
            {
                counter.Execute(tuple);
            }
            // Use LocalContext to persist the data stream to file
            counterCtx.WriteMsgQueueToFile("counter.txt");
            Console.WriteLine("Counter bolt finished");
        }
        #endregion
    }
    ```

    <span data-ttu-id="13e46-331">Leggere con attenzione i commenti del codice.</span><span class="sxs-lookup"><span data-stu-id="13e46-331">Take a moment to read through the code comments.</span></span> <span data-ttu-id="13e46-332">Questo codice usa **LocalContext** per eseguire i componenti dell'ambiente di sviluppo e rende permanente il flusso di dati tra i componenti e i file di testo sull'unità locale.</span><span class="sxs-lookup"><span data-stu-id="13e46-332">This code uses **LocalContext** to run the components in the development environment, and it persists the data stream between components to text files on the local drive.</span></span>

1. <span data-ttu-id="13e46-333">Aprire **Program.cs** e aggiungere al metodo **Main** il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="13e46-333">Open **Program.cs**, and add the following to the **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Starting tests");
    System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "WordCount-LocalTest");
    // Initialize the runtime
    SCPRuntime.Initialize();

    //If we are not running under the local context, throw an error
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

2. <span data-ttu-id="13e46-334">Salvare le modifiche, quindi premere **F5** o selezionare **Debug** > **Avvia debug** per avviare il progetto.</span><span class="sxs-lookup"><span data-stu-id="13e46-334">Save the changes, and then click **F5** or select **Debug** > **Start Debugging** to start the project.</span></span> <span data-ttu-id="13e46-335">Viene visualizzata una finestra della console, con lo stato del log aggiornato in base all'avanzamento dei test.</span><span class="sxs-lookup"><span data-stu-id="13e46-335">A console window should appear, and log status as the tests progress.</span></span> <span data-ttu-id="13e46-336">Quando viene visualizzato il messaggio **Esecuzione test completata** , premere un tasto qualsiasi per chiudere la finestra.</span><span class="sxs-lookup"><span data-stu-id="13e46-336">When **Tests finished** appears, press any key to close the window.</span></span>

3. <span data-ttu-id="13e46-337">Usare **Esplora risorse** per individuare la directory contenente il progetto.</span><span class="sxs-lookup"><span data-stu-id="13e46-337">Use **Windows Explorer** to locate the directory that contains your project.</span></span> <span data-ttu-id="13e46-338">Ad esempio **C:\Users\<your_user_name>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span><span class="sxs-lookup"><span data-stu-id="13e46-338">For example: **C:\Users\<your_user_name>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span></span> <span data-ttu-id="13e46-339">In questa directory, aprire **Bin** e quindi fare clic su **Debug**.</span><span class="sxs-lookup"><span data-stu-id="13e46-339">In this directory, open **Bin**, and then click **Debug**.</span></span> <span data-ttu-id="13e46-340">Verranno visualizzati i file di testo generati durante l'esecuzione dei test: sentences.txt, counter.txt e splitter.txt.</span><span class="sxs-lookup"><span data-stu-id="13e46-340">You should see the text files that were produced when the tests ran: sentences.txt, counter.txt, and splitter.txt.</span></span> <span data-ttu-id="13e46-341">Aprire ogni file di testo e verificare i dati.</span><span class="sxs-lookup"><span data-stu-id="13e46-341">Open each text file and inspect the data.</span></span>

   > [!NOTE]
   > <span data-ttu-id="13e46-342">In questi file i dati stringa vengono resi permanenti come matrice di valori decimali.</span><span class="sxs-lookup"><span data-stu-id="13e46-342">String data persists as an array of decimal values in these files.</span></span> <span data-ttu-id="13e46-343">Ad esempio \[[97,103,111]] nel file **splitter.txt** corrisponde alla parola *and*.</span><span class="sxs-lookup"><span data-stu-id="13e46-343">For example, \[[97,103,111]] in the **splitter.txt** file is the word *and*.</span></span>

> [!NOTE]
> <span data-ttu-id="13e46-344">Assicurarsi di reimpostare **Tipo di progetto** su **Libreria di classi** prima di eseguire la distribuzione a un cluster Storm in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="13e46-344">Be sure to set the **Project type** back to **Class Library** before deploying to a Storm on HDInsight cluster.</span></span>

### <a name="log-information"></a><span data-ttu-id="13e46-345">Informazioni di log</span><span class="sxs-lookup"><span data-stu-id="13e46-345">Log information</span></span>

<span data-ttu-id="13e46-346">È possibile registrare facilmente le informazioni provenienti dai componenti della topologia usando `Context.Logger`.</span><span class="sxs-lookup"><span data-stu-id="13e46-346">You can easily log information from your topology components by using `Context.Logger`.</span></span> <span data-ttu-id="13e46-347">Il codice seguente, ad esempio, crea una voce di log informativa:</span><span class="sxs-lookup"><span data-stu-id="13e46-347">For example, the following creates an informational log entry:</span></span>

```csharp
Context.Logger.Info("Component started");
```

<span data-ttu-id="13e46-348">È possibile visualizzare le informazioni registrate da **Hadoop Service Log**, disponibile in **Esplora Server**.</span><span class="sxs-lookup"><span data-stu-id="13e46-348">Logged information can be viewed from the **Hadoop Service Log**, which is found in **Server Explorer**.</span></span> <span data-ttu-id="13e46-349">Espandere la voce relativa al cluster Storm in HDInsight, quindi espandere **Hadoop Service Log**.</span><span class="sxs-lookup"><span data-stu-id="13e46-349">Expand the entry for your Storm on HDInsight cluster, and then expand **Hadoop Service Log**.</span></span> <span data-ttu-id="13e46-350">Al termine, selezionare il file di log da visualizzare.</span><span class="sxs-lookup"><span data-stu-id="13e46-350">Finally, select the log file to view.</span></span>

> [!NOTE]
> <span data-ttu-id="13e46-351">I log vengono memorizzati nell'account del servizio Archiviazione di Azure usato dal cluster.</span><span class="sxs-lookup"><span data-stu-id="13e46-351">The logs are stored in the Azure storage account that is used by your cluster.</span></span> <span data-ttu-id="13e46-352">Per visualizzare i log in Visual Studio, è necessario accedere alla sottoscrizione di Azure proprietaria dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="13e46-352">To view the logs in Visual Studio, you must sign in to the Azure subscription that owns the storage account.</span></span>

### <a name="view-error-information"></a><span data-ttu-id="13e46-353">Visualizzare le informazioni sugli errori</span><span class="sxs-lookup"><span data-stu-id="13e46-353">View error information</span></span>

<span data-ttu-id="13e46-354">Per visualizzare gli errori che si sono verificati in una topologia in esecuzione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="13e46-354">To view errors that have occurred in a running topology, use the following steps:</span></span>

1. <span data-ttu-id="13e46-355">Da **Esplora server** fare clic con il pulsante destro del mouse sul cluster Storm in HDInsight e selezionare **Visualizza topologie Storm**.</span><span class="sxs-lookup"><span data-stu-id="13e46-355">From **Server Explorer**, right-click the Storm on HDInsight cluster, and select **View Storm topologies**.</span></span>

2. <span data-ttu-id="13e46-356">Per quanto riguarda **Spout** e **Bolt**, nella colonna **Ultimo errore** vengono visualizzate informazioni sull'ultimo errore verificatosi.</span><span class="sxs-lookup"><span data-stu-id="13e46-356">For the **Spout** and **Bolts**, the **Last Error** column contains information on the last error.</span></span>

3. <span data-ttu-id="13e46-357">Selezionare **Spout Id** (ID spout) o **Bolt Id** (ID bolt) per il componente in cui si è verificato un errore.</span><span class="sxs-lookup"><span data-stu-id="13e46-357">Select the **Spout Id** or **Bolt Id** for the component that has an error listed.</span></span> <span data-ttu-id="13e46-358">Viene visualizzata una pagina dei dettagli. Nella parte inferiore di tale pagina, nella sezione **Errori**, vengono visualizzate informazioni aggiuntive sugli errori.</span><span class="sxs-lookup"><span data-stu-id="13e46-358">On the details page that is displayed, additional error information is listed in the **Errors** section at the bottom of the page.</span></span>

4. <span data-ttu-id="13e46-359">Per ottenere altre informazioni, selezionare una **porta** nella sezione **Executors** (Esecutori) della pagina. Verrà visualizzato il log di lavoro di Storm relativo agli ultimi minuti.</span><span class="sxs-lookup"><span data-stu-id="13e46-359">To obtain more information, select a **Port** from the **Executors** section of the page, to see the Storm worker log for the last few minutes.</span></span>

### <a name="errors-submitting-topologies"></a><span data-ttu-id="13e46-360">Errori durante l'invio delle topologie</span><span class="sxs-lookup"><span data-stu-id="13e46-360">Errors submitting topologies</span></span>

<span data-ttu-id="13e46-361">Se si verificano errori durante l'invio di una topologia a HDInsight, è possibile cercare i log per i componenti lato server che gestiscono l'invio delle topologie nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="13e46-361">If you encounter errors submitting a topology to HDInsight, you can find logs for the server-side components that handle topology submission on your HDInsight cluster.</span></span> <span data-ttu-id="13e46-362">Per recuperare questi log, usare il comando seguente da una riga di comando:</span><span class="sxs-lookup"><span data-stu-id="13e46-362">To retrieve these logs, use the following command from a command line:</span></span>

    scp sshuser@clustername-ssh.azurehdinsight.net:/var/log/hdinsight-scpwebapi/hdinsight-scpwebapi.out .

<span data-ttu-id="13e46-363">Sostituire __sshuser__ con l'account utente SSH per il cluster.</span><span class="sxs-lookup"><span data-stu-id="13e46-363">Replace __sshuser__ with the SSH user account for the cluster.</span></span> <span data-ttu-id="13e46-364">Sostituire __clustername__ con il nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="13e46-364">Replace __clustername__ with the name of the HDInsight cluster.</span></span> <span data-ttu-id="13e46-365">Per altre informazioni sull'uso di `scp` e `ssh` con HDInsight, vedere l'articolo [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="13e46-365">For more information on using `scp` and `ssh` with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="13e46-366">Gli invii possono non riuscire per diversi motivi:</span><span class="sxs-lookup"><span data-stu-id="13e46-366">Submissions can fail for multiple reasons:</span></span>

* <span data-ttu-id="13e46-367">JDK non è installato o non è presente nel percorso.</span><span class="sxs-lookup"><span data-stu-id="13e46-367">JDK is not installed or is not in the path.</span></span>
* <span data-ttu-id="13e46-368">Le dipendenze Java richieste non sono incluse nell'invio.</span><span class="sxs-lookup"><span data-stu-id="13e46-368">Required Java dependencies are not included in the submission.</span></span>
* <span data-ttu-id="13e46-369">Dipendenze incompatibili.</span><span class="sxs-lookup"><span data-stu-id="13e46-369">Incompatible dependencies.</span></span>
* <span data-ttu-id="13e46-370">Nomi di topologia duplicati.</span><span class="sxs-lookup"><span data-stu-id="13e46-370">Duplicate topology names.</span></span>

<span data-ttu-id="13e46-371">Se il log `hdinsight-scpwebapi.out` contiene un `FileNotFoundException`, le condizioni seguenti potrebbero esserne la causa:</span><span class="sxs-lookup"><span data-stu-id="13e46-371">If the `hdinsight-scpwebapi.out` log contains a `FileNotFoundException`, this might be caused by the following conditions:</span></span>

* <span data-ttu-id="13e46-372">Il pacchetto JDK non è presente nel percorso nell'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="13e46-372">The JDK is not in the path on the development environment.</span></span> <span data-ttu-id="13e46-373">Verificare che il pacchetto JDK sia installato nell'ambiente di sviluppo e che `%JAVA_HOME%/bin` sia presente nel percorso.</span><span class="sxs-lookup"><span data-stu-id="13e46-373">Verify that the JDK is installed in the development environment, and that `%JAVA_HOME%/bin` is in the path.</span></span>
* <span data-ttu-id="13e46-374">Manca una dipendenza Java.</span><span class="sxs-lookup"><span data-stu-id="13e46-374">You are missing a Java dependency.</span></span> <span data-ttu-id="13e46-375">Assicurarsi di includere nell'invio tutti i file con estensione jar necessari.</span><span class="sxs-lookup"><span data-stu-id="13e46-375">Make sure you are including any required .jar files as part of the submission.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13e46-376">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="13e46-376">Next steps</span></span>

<span data-ttu-id="13e46-377">Per un esempio di elaborazione dei dati dall'hub eventi, vedere [Elaborare eventi dell'hub eventi di Azure con Storm in HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="13e46-377">For an example of processing data from Event Hubs, see [Process events from Azure Event Hubs with Storm on HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span>

<span data-ttu-id="13e46-378">Per un esempio di una topologia di C# che divide il flusso di dati in più flussi, vedere [csharp-storm-example](https://github.com/Blackmist/csharp-storm-example).</span><span class="sxs-lookup"><span data-stu-id="13e46-378">For an example of a C# topology that splits stream data into multiple streams, see [C# Storm example](https://github.com/Blackmist/csharp-storm-example).</span></span>

<span data-ttu-id="13e46-379">Per altre informazioni sulla creazione delle topologie C#, visitare [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span><span class="sxs-lookup"><span data-stu-id="13e46-379">To discover more information about creating C# topologies, see [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span></span>

<span data-ttu-id="13e46-380">Per altre informazioni su come usare HDInsight o altri esempi su Storm in HDinsight, vedere i documenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="13e46-380">For more ways to work with HDInsight and more Storm on HDInsight samples, see the following documents:</span></span>

<span data-ttu-id="13e46-381">**Microsoft SCP.NET**</span><span class="sxs-lookup"><span data-stu-id="13e46-381">**Microsoft SCP.NET**</span></span>

* [<span data-ttu-id="13e46-382">Guida alla programmazione SCP</span><span class="sxs-lookup"><span data-stu-id="13e46-382">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)

<span data-ttu-id="13e46-383">**Apache Storm in HDInsight**</span><span class="sxs-lookup"><span data-stu-id="13e46-383">**Apache Storm on HDInsight**</span></span>

* [<span data-ttu-id="13e46-384">Distribuzione e monitoraggio di topologie con Apache Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="13e46-384">Deploy and monitor topologies with Apache Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)
* [<span data-ttu-id="13e46-385">Topologie di esempio per Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="13e46-385">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

<span data-ttu-id="13e46-386">**Apache Hadoop in HDInsight**</span><span class="sxs-lookup"><span data-stu-id="13e46-386">**Apache Hadoop on HDInsight**</span></span>

* [<span data-ttu-id="13e46-387">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="13e46-387">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="13e46-388">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="13e46-388">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="13e46-389">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="13e46-389">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="13e46-390">**Apache HBase in HDInsight**</span><span class="sxs-lookup"><span data-stu-id="13e46-390">**Apache HBase on HDInsight**</span></span>

* [<span data-ttu-id="13e46-391">Introduzione a HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="13e46-391">Getting started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
