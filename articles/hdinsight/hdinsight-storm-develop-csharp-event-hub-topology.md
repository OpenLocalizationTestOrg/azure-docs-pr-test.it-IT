---
title: Elaborare eventi da Hub eventi con Storm - Azure HDInsight | Microsoft Docs
description: Informazioni su come elaborare i dati degli Hub eventi di Azure con una topologia Storm C# creata in Visual Studio tramite HDInsight Tools per Visual Studio.
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 67f9d08c-eea0-401b-952b-db765655dad0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 4b6fd87b057d93175d3ef284238d77be3bdde61d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-c"></a><span data-ttu-id="46f52-103">Elaborare eventi dell'hub eventi di Azure con Storm in HDInsight (C#)</span><span class="sxs-lookup"><span data-stu-id="46f52-103">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>

<span data-ttu-id="46f52-104">Informazioni su come usare Hub eventi di Azure da Apache Storm in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="46f52-104">Learn how to work with Azure Event Hubs from Apache Storm on HDInsight.</span></span> <span data-ttu-id="46f52-105">In questo documento viene usata una topologia Storm con C# per leggere e scrivere dati da Hub eventi</span><span class="sxs-lookup"><span data-stu-id="46f52-105">This document uses a C# Storm topology to read and write data from Evbent Hubs</span></span>

> [!NOTE]
> <span data-ttu-id="46f52-106">Per la versione Java di questo progetto, vedere [Elaborare eventi dell'hub eventi di Azure con Storm in HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="46f52-106">For a Java version of this project, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="scpnet"></a><span data-ttu-id="46f52-107">SCP.NET</span><span class="sxs-lookup"><span data-stu-id="46f52-107">SCP.NET</span></span>

<span data-ttu-id="46f52-108">Nella procedura in questo documento viene usato SCP.NET, un pacchetto NuGet che semplifica la creazione di topologie e componenti C# per l'uso con Storm in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="46f52-108">The steps in this document use SCP.NET, a NuGet package that makes it easy to create C# topologies and components for use with Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="46f52-109">Anche se i passaggi illustrati in questo documento si basano su un ambiente di sviluppo Windows con Visual Studio, il progetto compilato può essere inviato a Storm in un cluster HDInsight che usa Linux.</span><span class="sxs-lookup"><span data-stu-id="46f52-109">While the steps in this document rely on a Windows development environment with Visual Studio, the compiled project can be submitted to a Storm on HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="46f52-110">Solo i cluster basati su Linux creati dopo il 28 ottobre 2016 supportano le topologie SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="46f52-110">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="46f52-111">HDInsight versione 3.4 o successiva usano Mono per eseguire le topologie C#.</span><span class="sxs-lookup"><span data-stu-id="46f52-111">HDInsight 3.4 and greater use Mono to run C# topologies.</span></span> <span data-ttu-id="46f52-112">L'esempio in questo documento funziona con HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="46f52-112">The example used in this document works with HDInsight 3.6.</span></span> <span data-ttu-id="46f52-113">Se si prevede di creare soluzioni .NET personalizzate per HDInsight, leggere il documento [Mono Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) (Compatibilità di Mono) per individuare potenziali incompatibilità.</span><span class="sxs-lookup"><span data-stu-id="46f52-113">If you plan on creating your own .NET solutions for HDInsight, check the [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>

### <a name="cluster-versioning"></a><span data-ttu-id="46f52-114">Controllo delle versioni del cluster</span><span class="sxs-lookup"><span data-stu-id="46f52-114">Cluster versioning</span></span>

<span data-ttu-id="46f52-115">Il pacchetto NuGet Microsoft.SCP.Net.SDK usato per il progetto deve corrispondere alla versione principale di Storm installata in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="46f52-115">The Microsoft.SCP.Net.SDK NuGet package you use for your project must match the major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="46f52-116">HDInsight versioni 3.5 e 3.6 usa Storm versione 1.x, pertanto è necessario usare SCP.NET versione 1.0.x.x con questi cluster.</span><span class="sxs-lookup"><span data-stu-id="46f52-116">HDInsight versions 3.5 and 3.6 use Storm 1.x, so you must use SCP.NET version 1.0.x.x with these clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="46f52-117">L'esempio in questo documento presuppone un cluster HDInsight 3.5 o 3.6.</span><span class="sxs-lookup"><span data-stu-id="46f52-117">The example in this document expects an HDInsight 3.5 or 3.6 cluster.</span></span>
>
> <span data-ttu-id="46f52-118">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="46f52-118">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="46f52-119">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="46f52-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="46f52-120">Le topologie C# devono inoltre puntare a .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="46f52-120">C# topologies must also target .NET 4.5.</span></span>

## <a name="how-to-work-with-event-hubs"></a><span data-ttu-id="46f52-121">Come lavorare con gli Hub eventi</span><span class="sxs-lookup"><span data-stu-id="46f52-121">How to work with Event Hubs</span></span>

<span data-ttu-id="46f52-122">Microsoft fornisce un set di componenti Java da usare per comunicare con gli Hub eventi da una topologia Storm.</span><span class="sxs-lookup"><span data-stu-id="46f52-122">Microsoft provides a set of Java components that can be used to communicate with Event Hubs from a Storm topology.</span></span> <span data-ttu-id="46f52-123">Il file di archivio Java (JAR) che contiene una versione compatibile di HDInsight 3.6 di questi componenti è disponibile in [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span><span class="sxs-lookup"><span data-stu-id="46f52-123">You can find the Java archive (JAR) file that contains an HDInsight 3.6 compatible version of these components at [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="46f52-124">I componenti sono scritti in Java ma è comunque possibile usarli da una topologia C#.</span><span class="sxs-lookup"><span data-stu-id="46f52-124">While the components are written in Java, you can easily use them from a C# topology.</span></span>

<span data-ttu-id="46f52-125">Nell'esempio vengono usati i componenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="46f52-125">The following components are used in this example:</span></span>

* <span data-ttu-id="46f52-126">__EventHubSpout__: legge i dati dagli Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="46f52-126">__EventHubSpout__: Reads data from Event Hubs.</span></span>
* <span data-ttu-id="46f52-127">__EventHubBolt__: scrive i dati negli Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="46f52-127">__EventHubBolt__: Writes data to Event Hubs.</span></span>
* <span data-ttu-id="46f52-128">__EventHubSpoutConfig__: usato per configurare EventHubSpout.</span><span class="sxs-lookup"><span data-stu-id="46f52-128">__EventHubSpoutConfig__: Used to configure EventHubSpout.</span></span>
* <span data-ttu-id="46f52-129">__EventHubBoltConfig__: usato per configurare EventHubBolt.</span><span class="sxs-lookup"><span data-stu-id="46f52-129">__EventHubBoltConfig__: Used to configure EventHubBolt.</span></span>

### <a name="example-spout-usage"></a><span data-ttu-id="46f52-130">Esempio di uso di uno spout</span><span class="sxs-lookup"><span data-stu-id="46f52-130">Example spout usage</span></span>

<span data-ttu-id="46f52-131">SCP.NET offre metodi per l'aggiunta di EventHubSpout alla topologia.</span><span class="sxs-lookup"><span data-stu-id="46f52-131">SCP.NET provides methods for adding an EventHubSpout to your topology.</span></span> <span data-ttu-id="46f52-132">Questi metodi facilitano l'aggiunta di uno spout rispetto ai metodi generici di aggiunta di un componente Java.</span><span class="sxs-lookup"><span data-stu-id="46f52-132">These methods make it easier to add a spout than using the generic methods for adding a Java component.</span></span> <span data-ttu-id="46f52-133">L'esempio seguente illustra come creare uno spout usando i metodi __SetEventHubSpout__ ed **EventHubSpoutConfig** forniti da SCP.NET:</span><span class="sxs-lookup"><span data-stu-id="46f52-133">The following example demonstrates how to create a spout by using the __SetEventHubSpout__ and **EventHubSpoutConfig** methods provided by SCP.NET:</span></span>

```csharp
 topologyBuilder.SetEventHubSpout(
    "EventHubSpout",
    new EventHubSpoutConfig(
        ConfigurationManager.AppSettings["EventHubSharedAccessKeyName"],
        ConfigurationManager.AppSettings["EventHubSharedAccessKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        ConfigurationManager.AppSettings["EventHubEntityPath"],
        eventHubPartitions),
    eventHubPartitions);
```

<span data-ttu-id="46f52-134">Nell'esempio precedente viene creato un nuovo componente spout denominato __EventHubSpout__, che viene poi configurato per comunicare con un Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="46f52-134">The previous example creates a new spout component named __EventHubSpout__, and configures it to communicate with an event hub.</span></span> <span data-ttu-id="46f52-135">Per il componente viene impostato anche l'hint di parallelismo sul numero di partizioni nell'Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="46f52-135">The parallelism hint for the component is set to the number of partitions in the event hub.</span></span> <span data-ttu-id="46f52-136">Questa impostazione consente a Storm di creare un'istanza del componente per ogni partizione.</span><span class="sxs-lookup"><span data-stu-id="46f52-136">This setting allows Storm to create an instance of the component for each partition.</span></span>

### <a name="example-bolt-usage"></a><span data-ttu-id="46f52-137">Esempio di utilizzo di bolt</span><span class="sxs-lookup"><span data-stu-id="46f52-137">Example bolt usage</span></span>

<span data-ttu-id="46f52-138">Usare il metodo **JavaComponmentConstructor** per creare un'istanza del bolt.</span><span class="sxs-lookup"><span data-stu-id="46f52-138">Use the **JavaComponmentConstructor** method to create an instance of the bolt.</span></span> <span data-ttu-id="46f52-139">L'esempio seguente illustra come creare e configurare una nuova istanza di **EventHubBolt**:</span><span class="sxs-lookup"><span data-stu-id="46f52-139">The following example demonstrates how to create and configure a new instance of the **EventHubBolt**:</span></span>

```csharp
// Java construcvtor for the Event Hub Bolt
JavaComponentConstructor constructor = JavaComponentConstructor.CreateFromClojureExpr(
    String.Format(@"(org.apache.storm.eventhubs.bolt.EventHubBolt. (org.apache.storm.eventhubs.bolt.EventHubBoltConfig. " +
        @"""{0}"" ""{1}"" ""{2}"" ""{3}"" ""{4}"" {5}))",
        ConfigurationManager.AppSettings["EventHubPolicyName"],
        ConfigurationManager.AppSettings["EventHubPolicyKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        "servicebus.windows.net",
        ConfigurationManager.AppSettings["EventHubName"],
        "true"));

// Set the bolt to subscribe to data from the spout
topologyBuilder.SetJavaBolt(
    "eventhubbolt",
    constructor,
    partitionCount)
        .shuffleGrouping("Spout");
```

> [!NOTE]
> <span data-ttu-id="46f52-140">In questo esempio, per creare un **EventHubBoltConfig** viene usata un'espressione Clojure passata come stringa e non **JavaComponentConstructor**, come nell'esempio dello spout.</span><span class="sxs-lookup"><span data-stu-id="46f52-140">This example uses a Clojure expression passed as a string, instead of using **JavaComponentConstructor** to create an **EventHubBoltConfig**, as the spout example did.</span></span> <span data-ttu-id="46f52-141">Entrambi i metodi sono validi</span><span class="sxs-lookup"><span data-stu-id="46f52-141">Either method works.</span></span> <span data-ttu-id="46f52-142">ed è possibile scegliere quello ritenuto migliore.</span><span class="sxs-lookup"><span data-stu-id="46f52-142">Use the method that feels best to you.</span></span>

## <a name="download-the-completed-project"></a><span data-ttu-id="46f52-143">Scaricare il progetto completo</span><span class="sxs-lookup"><span data-stu-id="46f52-143">Download the completed project</span></span>

<span data-ttu-id="46f52-144">È possibile scaricare la versione completa del progetto creato in questa esercitazione da [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="46f52-144">You can download a complete version of the project created in this tutorial from [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span> <span data-ttu-id="46f52-145">Sarà tuttavia necessario fornire le impostazioni di configurazione seguendo la procedura riportata in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="46f52-145">However, you still need to provide configuration settings by following the steps in this tutorial.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="46f52-146">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="46f52-146">Prerequisites</span></span>

* <span data-ttu-id="46f52-147">Un [cluster Apache Storm in HDInsight versione 3.5 o 3.6](hdinsight-apache-storm-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="46f52-147">An [Apache Storm on HDInsight cluster version 3.5 or 3.6](hdinsight-apache-storm-tutorial-get-started.md).</span></span>

    > [!WARNING]
    > <span data-ttu-id="46f52-148">Per l'esempio usato in questo documento è necessario Storm in HDInsight versione 3.5 o 3.6.</span><span class="sxs-lookup"><span data-stu-id="46f52-148">The example used in this document requires Storm on HDInsight version 3.5 or 3.6.</span></span> <span data-ttu-id="46f52-149">Questo approccio non funzionerà con le versioni precedenti di HDInsight a causa di modifiche importanti apportate al nome della classe.</span><span class="sxs-lookup"><span data-stu-id="46f52-149">This does not work with older versions of HDInsight, due to breaking class name changes.</span></span> <span data-ttu-id="46f52-150">Per una versione di questo esempio funziona con i cluster precedenti, vedere [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span><span class="sxs-lookup"><span data-stu-id="46f52-150">For a version of this example that works with older clusters, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span></span>

* <span data-ttu-id="46f52-151">Un [Hub eventi di Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="46f52-151">An [Azure event hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="46f52-152">[Azure .NET SDK](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="46f52-152">The [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>

* <span data-ttu-id="46f52-153">[HDInsight Tools per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="46f52-153">The [HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="46f52-154">Java JDK 1.8 o versione successiva nell'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="46f52-154">Java JDK 1.8 or later on your development environment.</span></span> <span data-ttu-id="46f52-155">Sono disponibili download di JDK da [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="46f52-155">JDK downloads are available from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>

  * <span data-ttu-id="46f52-156">La variabile di ambiente **JAVA_HOME** deve puntare alla directory contenente Java.</span><span class="sxs-lookup"><span data-stu-id="46f52-156">The **JAVA_HOME** environment variable must point to the directory that contains Java.</span></span>
  * <span data-ttu-id="46f52-157">La directory **%JAVA_HOME%/bin** deve essere inclusa nel percorso.</span><span class="sxs-lookup"><span data-stu-id="46f52-157">The **%JAVA_HOME%/bin** directory must be in the path.</span></span>

## <a name="download-the-event-hubs-components"></a><span data-ttu-id="46f52-158">Scaricare i componenti di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="46f52-158">Download the Event Hubs components</span></span>

<span data-ttu-id="46f52-159">Scaricare il componente spout e bolt di Hub eventi da [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span><span class="sxs-lookup"><span data-stu-id="46f52-159">Download the Event Hubs spout and bolt component from [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

<span data-ttu-id="46f52-160">Creare una directory denominata `eventhubspout` e salvare il file in tale directory.</span><span class="sxs-lookup"><span data-stu-id="46f52-160">Create a directory named `eventhubspout`, and save the file into the directory.</span></span>

## <a name="configure-event-hubs"></a><span data-ttu-id="46f52-161">Configurare gli hub eventi</span><span class="sxs-lookup"><span data-stu-id="46f52-161">Configure Event Hubs</span></span>

<span data-ttu-id="46f52-162">L'hub eventi è l'origine dati per questo esempio.</span><span class="sxs-lookup"><span data-stu-id="46f52-162">Event Hubs is the data source for this example.</span></span> <span data-ttu-id="46f52-163">Usare le informazioni contenute nella sezione "Creare un hub eventi" di [Introduzione all'Hub eventi](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="46f52-163">Use the information in the "Create an event hub" section of [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

1. <span data-ttu-id="46f52-164">Dopo avere creato l'hub eventi, visualizzare il pannello **Hub eventi** nel portale di Azure e selezionare **Criteri di accesso condivisi**.</span><span class="sxs-lookup"><span data-stu-id="46f52-164">After the event hub has been created, view the **EventHub** blade in the Azure portal, and select **Shared access policies**.</span></span> <span data-ttu-id="46f52-165">Selezionare **+ Aggiungi** per aggiungere i criteri seguenti:</span><span class="sxs-lookup"><span data-stu-id="46f52-165">Select **+ Add** to add the following policies:</span></span>

   | <span data-ttu-id="46f52-166">Nome</span><span class="sxs-lookup"><span data-stu-id="46f52-166">Name</span></span> | <span data-ttu-id="46f52-167">Autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="46f52-167">Permissions</span></span> |
   | --- | --- |
   | <span data-ttu-id="46f52-168">writer</span><span class="sxs-lookup"><span data-stu-id="46f52-168">writer</span></span> |<span data-ttu-id="46f52-169">Invio</span><span class="sxs-lookup"><span data-stu-id="46f52-169">Send</span></span> |
   | <span data-ttu-id="46f52-170">reader</span><span class="sxs-lookup"><span data-stu-id="46f52-170">reader</span></span> |<span data-ttu-id="46f52-171">Attesa</span><span class="sxs-lookup"><span data-stu-id="46f52-171">Listen</span></span> |

    ![Schermata della finestra Criteri di accesso condivisi](./media/hdinsight-storm-develop-csharp-event-hub-topology/sas.png)

2. <span data-ttu-id="46f52-173">Selezionare i criteri **reader** and **writer**.</span><span class="sxs-lookup"><span data-stu-id="46f52-173">Select the **reader** and **writer** policies.</span></span> <span data-ttu-id="46f52-174">Copiare e salvare i valori di chiave primaria per entrambi i criteri, perché verranno usati in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="46f52-174">Copy and save the primary key value for both policies, as these values are used later.</span></span>

## <a name="configure-the-eventhubwriter"></a><span data-ttu-id="46f52-175">Configurare EventHubWriter</span><span class="sxs-lookup"><span data-stu-id="46f52-175">Configure the EventHubWriter</span></span>

1. <span data-ttu-id="46f52-176">Se la versione più recente di HDInsight Tools per Visual Studio non è ancora installata, vedere [Introduzione all'uso di HDInsight Tools per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="46f52-176">If you have not already installed the latest version of the HDInsight tools for Visual Studio, see [Get started using HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="46f52-177">Scaricare la soluzione da [eventhub-storm-hybrid](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="46f52-177">Download the solution from [eventhub-storm-hybrid](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

3. <span data-ttu-id="46f52-178">Nel progetto **EventHubWriter** aprire il file **App.config**.</span><span class="sxs-lookup"><span data-stu-id="46f52-178">In the **EventHubWriter** project, open the **App.config** file.</span></span> <span data-ttu-id="46f52-179">Usare le informazioni dell'hub eventi configurato prima per inserire il valore per le chiavi seguenti:</span><span class="sxs-lookup"><span data-stu-id="46f52-179">Use the information from the event hub that you configured earlier to fill in the value for the following keys:</span></span>

   | <span data-ttu-id="46f52-180">Chiave</span><span class="sxs-lookup"><span data-stu-id="46f52-180">Key</span></span> | <span data-ttu-id="46f52-181">Valore</span><span class="sxs-lookup"><span data-stu-id="46f52-181">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="46f52-182">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="46f52-182">EventHubPolicyName</span></span> |<span data-ttu-id="46f52-183">writer (se è stato usato un altro nome per il criterio con l'autorizzazione *Send*, usare l'altro nome)</span><span class="sxs-lookup"><span data-stu-id="46f52-183">writer (If you used a different name for the policy with *Send* permission, use it instead.)</span></span> |
   | <span data-ttu-id="46f52-184">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="46f52-184">EventHubPolicyKey</span></span> |<span data-ttu-id="46f52-185">Chiave per il criterio writer.</span><span class="sxs-lookup"><span data-stu-id="46f52-185">The key for the writer policy.</span></span> |
   | <span data-ttu-id="46f52-186">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="46f52-186">EventHubNamespace</span></span> |<span data-ttu-id="46f52-187">Spazio dei nomi contenente l'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="46f52-187">The namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="46f52-188">EventHubName</span><span class="sxs-lookup"><span data-stu-id="46f52-188">EventHubName</span></span> |<span data-ttu-id="46f52-189">Nome dell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="46f52-189">Your event hub name.</span></span> |
   | <span data-ttu-id="46f52-190">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="46f52-190">EventHubPartitionCount</span></span> |<span data-ttu-id="46f52-191">Numero di partizioni nell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="46f52-191">The number of partitions in your event hub.</span></span> |

4. <span data-ttu-id="46f52-192">Salvare e chiudere il file **App.config**.</span><span class="sxs-lookup"><span data-stu-id="46f52-192">Save and close the **App.config** file.</span></span>

## <a name="configure-the-eventhubreader"></a><span data-ttu-id="46f52-193">Configurare EventHubReader</span><span class="sxs-lookup"><span data-stu-id="46f52-193">Configure the EventHubReader</span></span>

1. <span data-ttu-id="46f52-194">Aprire il progetto **EventHubReader**.</span><span class="sxs-lookup"><span data-stu-id="46f52-194">Open the **EventHubReader** project.</span></span>

2. <span data-ttu-id="46f52-195">Aprire il file **App.config** per **EventHubReader**.</span><span class="sxs-lookup"><span data-stu-id="46f52-195">Open the **App.config** file for the **EventHubReader**.</span></span> <span data-ttu-id="46f52-196">Usare le informazioni dell'hub eventi configurato prima per inserire il valore per le chiavi seguenti:</span><span class="sxs-lookup"><span data-stu-id="46f52-196">Use the information from the event hub that you configured earlier to fill in the value for the following keys:</span></span>

   | <span data-ttu-id="46f52-197">Chiave</span><span class="sxs-lookup"><span data-stu-id="46f52-197">Key</span></span> | <span data-ttu-id="46f52-198">Valore</span><span class="sxs-lookup"><span data-stu-id="46f52-198">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="46f52-199">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="46f52-199">EventHubPolicyName</span></span> |<span data-ttu-id="46f52-200">reader (se è stato usato un altro nome per il criterio con l'autorizzazione *listen*, usare l'altro nome)</span><span class="sxs-lookup"><span data-stu-id="46f52-200">reader (If you used a different name for the policy with *listen* permission, use it instead.)</span></span> |
   | <span data-ttu-id="46f52-201">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="46f52-201">EventHubPolicyKey</span></span> |<span data-ttu-id="46f52-202">Chiave per il criterio reader.</span><span class="sxs-lookup"><span data-stu-id="46f52-202">The key for the reader policy.</span></span> |
   | <span data-ttu-id="46f52-203">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="46f52-203">EventHubNamespace</span></span> |<span data-ttu-id="46f52-204">Spazio dei nomi contenente l'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="46f52-204">The namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="46f52-205">EventHubName</span><span class="sxs-lookup"><span data-stu-id="46f52-205">EventHubName</span></span> |<span data-ttu-id="46f52-206">Nome dell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="46f52-206">Your event hub name.</span></span> |
   | <span data-ttu-id="46f52-207">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="46f52-207">EventHubPartitionCount</span></span> |<span data-ttu-id="46f52-208">Numero di partizioni nell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="46f52-208">The number of partitions in your event hub.</span></span> |

3. <span data-ttu-id="46f52-209">Salvare e chiudere il file **App.config**.</span><span class="sxs-lookup"><span data-stu-id="46f52-209">Save and close the **App.config** file.</span></span>

## <a name="deploy-the-topologies"></a><span data-ttu-id="46f52-210">Distribuire le topologie</span><span class="sxs-lookup"><span data-stu-id="46f52-210">Deploy the topologies</span></span>

1. <span data-ttu-id="46f52-211">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto **EventHubReader** e scegliere Submit to Storm on HDInsight **(Invia a Storm in HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="46f52-211">From **Solution Explorer**, right-click the **EventHubReader** project, and select **Submit to Storm on HDInsight**.</span></span>

    ![Schermata di Esplora soluzioni con Submit to Storm on HDInsight (Invia a Storm in HDInsight) evidenziato](./media/hdinsight-storm-develop-csharp-event-hub-topology/submittostorm.png)

2. <span data-ttu-id="46f52-213">Nella finestra di dialogo **Submit Topology** (Invia topologia) selezionare il **cluster Storm**.</span><span class="sxs-lookup"><span data-stu-id="46f52-213">On the **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="46f52-214">Espandere **Additional Configurations** (Configurazioni aggiuntive), selezionare **Java File Paths** (Percorsi file Java), selezionare **...** e quindi selezionare la directory contenente il file JAR scaricato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="46f52-214">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select the directory that contains the JAR file that you downloaded earlier.</span></span> <span data-ttu-id="46f52-215">Infine fare clic su **Submit**.</span><span class="sxs-lookup"><span data-stu-id="46f52-215">Finally, click **Submit**.</span></span>

    ![Schermata della finestra di dialogo Submit Topology (Invia topologia)](./media/hdinsight-storm-develop-csharp-event-hub-topology/submit.png)

3. <span data-ttu-id="46f52-217">Dopo l'invio della topologia, verrà visualizzato **Storm Topologies Viewer** (Visualizzatore topologie Storm).</span><span class="sxs-lookup"><span data-stu-id="46f52-217">When the topology has been submitted, the **Storm Topologies Viewer** appears.</span></span> <span data-ttu-id="46f52-218">Selezionare la topologia **EventHubReader** nel riquadro a sinistra per visualizzare le relative informazioni.</span><span class="sxs-lookup"><span data-stu-id="46f52-218">To view information about the topology, select the **EventHubReader** topology in the left pane.</span></span>

    ![Schermata Storm Topologies Viewer (Visualizzatore topologie Storm)](./media/hdinsight-storm-develop-csharp-event-hub-topology/topologyviewer.png)

4. <span data-ttu-id="46f52-220">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto **EventHubWriter** e scegliere **Submit to Storm on HDInsight** (Invia a Storm in HDInsight).</span><span class="sxs-lookup"><span data-stu-id="46f52-220">From **Solution Explorer**, right-click the **EventHubWriter** project, and select **Submit to Storm on HDInsight**.</span></span>

5. <span data-ttu-id="46f52-221">Nella finestra di dialogo **Submit Topology** (Invia topologia) selezionare il **cluster Storm**.</span><span class="sxs-lookup"><span data-stu-id="46f52-221">On the **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="46f52-222">Espandere **Additional Configurations** (Configurazioni aggiuntive), selezionare **Java File Paths** (Percorsi file Java), selezionare **...** e quindi selezionare la directory contenente il file JAR scaricato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="46f52-222">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select the directory that contains the JAR file you downloaded earlier.</span></span> <span data-ttu-id="46f52-223">Infine fare clic su **Submit**.</span><span class="sxs-lookup"><span data-stu-id="46f52-223">Finally, click **Submit**.</span></span>

6. <span data-ttu-id="46f52-224">Dopo l'invio della topologia, aggiornare l'elenco delle topologie in **Storm Topologies Viewer** per verificare che siano entrambe in esecuzione nel cluster.</span><span class="sxs-lookup"><span data-stu-id="46f52-224">When the topology has been submitted, refresh the topology list in the **Storm Topologies Viewer** to verify that both topologies are running on the cluster.</span></span>

7. <span data-ttu-id="46f52-225">In **Storm Topologies Viewer** (Visualizzatore topologie Storm) selezionare la topologia **EventHubReader**.</span><span class="sxs-lookup"><span data-stu-id="46f52-225">In **Storm Topologies Viewer**, select the **EventHubReader** topology.</span></span>

8. <span data-ttu-id="46f52-226">Per aprire il riepilogo componenti per il bolt, fare doppio clic sul componente **LogBolt** nel diagramma.</span><span class="sxs-lookup"><span data-stu-id="46f52-226">To open the component summary for the bolt, double-click the **LogBolt** component in the diagram.</span></span>

9. <span data-ttu-id="46f52-227">Nella sezione **Executors** (Esecutori) selezionare uno dei collegamenti nella colonna **Porta**.</span><span class="sxs-lookup"><span data-stu-id="46f52-227">In the **Executors** section, select one of the links in the **Port** column.</span></span> <span data-ttu-id="46f52-228">Verranno visualizzate le informazioni registrate dal componente.</span><span class="sxs-lookup"><span data-stu-id="46f52-228">This displays information logged by the component.</span></span> <span data-ttu-id="46f52-229">Le informazioni registrate sono simili al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="46f52-229">The logged information is similar to the following text:</span></span>

        2017-03-02 14:51:29.255 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,255 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1830978598,"deviceId":"8566ccbc-034d-45db-883d-d8a31f34068e"}
        2017-03-02 14:51:29.283 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,283 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1756413275,"deviceId":"647a5eff-823d-482f-a8b4-b95b35ae570b"}
        2017-03-02 14:51:29.313 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,312 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1108478910,"deviceId":"206a68fa-8264-4d61-9100-bfdb68ee8f0a"}

## <a name="stop-the-topologies"></a><span data-ttu-id="46f52-230">Arrestare le topologie</span><span class="sxs-lookup"><span data-stu-id="46f52-230">Stop the topologies</span></span>

<span data-ttu-id="46f52-231">Per arrestare le topologie, selezionarle singolarmente in **Storm Topology Viewer** (Visualizzatore topologie Storm) e quindi fare clic su **Termina**.</span><span class="sxs-lookup"><span data-stu-id="46f52-231">To stop the topologies, select each topology in the **Storm Topology Viewer**, then click **Kill**.</span></span>

![Schermata Storm Topology Viewer (Visualizzatore topologie Storm), con il pulsante Kill (Termina) evidenziato](./media/hdinsight-storm-develop-csharp-event-hub-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="46f52-233">Eliminare il cluster</span><span class="sxs-lookup"><span data-stu-id="46f52-233">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="46f52-234">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="46f52-234">Next steps</span></span>

<span data-ttu-id="46f52-235">In questo documento si è appreso come usare lo spout e il bolt degli Hub eventi Java da una topologia C# per utilizzare i dati nell'hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="46f52-235">In this document, you have learned how to use the Java Event Hubs spout and bolt from a C# topology to work with data in Azure Event Hubs.</span></span> <span data-ttu-id="46f52-236">Per altre informazioni sulla creazione di topologie C#, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="46f52-236">To learn more about creating C# topologies, see the following:</span></span>

* [<span data-ttu-id="46f52-237">Sviluppare topologie C# per Apache Storm in HDInsight tramite Visual Studio</span><span class="sxs-lookup"><span data-stu-id="46f52-237">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="46f52-238">Guida alla programmazione SCP</span><span class="sxs-lookup"><span data-stu-id="46f52-238">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)
* [<span data-ttu-id="46f52-239">Topologie di esempio per Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="46f52-239">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
