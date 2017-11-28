---
title: eventi aaaProcess dagli hub eventi con Storm - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come dati tooprocess dagli hub di eventi di Azure con una topologia c# Storm create in Visual Studio, utilizzando hello strumenti HDInsight per Visual Studio.
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
ms.openlocfilehash: 30cd910d80eba066f283197bcbbaf11145bc5524
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-c"></a><span data-ttu-id="409a8-103">Elaborare eventi dell'hub eventi di Azure con Storm in HDInsight (C#)</span><span class="sxs-lookup"><span data-stu-id="409a8-103">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>

<span data-ttu-id="409a8-104">Informazioni su come toowork con hub di eventi di Azure da Apache Storm in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="409a8-104">Learn how toowork with Azure Event Hubs from Apache Storm on HDInsight.</span></span> <span data-ttu-id="409a8-105">Questo documento viene utilizzato un elevato numero di c# topologia tooread e scrittura dati dagli hub Evbent</span><span class="sxs-lookup"><span data-stu-id="409a8-105">This document uses a C# Storm topology tooread and write data from Evbent Hubs</span></span>

> [!NOTE]
> <span data-ttu-id="409a8-106">Per la versione Java di questo progetto, vedere [Elaborare eventi dell'hub eventi di Azure con Storm in HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="409a8-106">For a Java version of this project, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="scpnet"></a><span data-ttu-id="409a8-107">SCP.NET</span><span class="sxs-lookup"><span data-stu-id="409a8-107">SCP.NET</span></span>

<span data-ttu-id="409a8-108">passaggi di Hello in questo documento usano SCP.NET, un pacchetto NuGet che rende facile toocreate c# topologie e componenti per l'utilizzo con Storm in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="409a8-108">hello steps in this document use SCP.NET, a NuGet package that makes it easy toocreate C# topologies and components for use with Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="409a8-109">Anche se hello i passaggi in questo documento si basano su un ambiente di sviluppo Windows con Visual Studio, progetto compilato hello può essere inviato tooa Storm nel cluster HDInsight che utilizza Linux.</span><span class="sxs-lookup"><span data-stu-id="409a8-109">While hello steps in this document rely on a Windows development environment with Visual Studio, hello compiled project can be submitted tooa Storm on HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="409a8-110">Solo i cluster basati su Linux creati dopo il 28 ottobre 2016 supportano le topologie SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="409a8-110">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="409a8-111">HDInsight 3.4 e maggiore utilizzo Mono toorun c# topologie.</span><span class="sxs-lookup"><span data-stu-id="409a8-111">HDInsight 3.4 and greater use Mono toorun C# topologies.</span></span> <span data-ttu-id="409a8-112">esempio Hello utilizzato in questo documento illustra 3.6 di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="409a8-112">hello example used in this document works with HDInsight 3.6.</span></span> <span data-ttu-id="409a8-113">Se si prevede la creazione di soluzioni di .NET per HDInsight, controllare hello [compatibilità Mono](http://www.mono-project.com/docs/about-mono/compatibility/) documento per potenziali problemi di incompatibilità.</span><span class="sxs-lookup"><span data-stu-id="409a8-113">If you plan on creating your own .NET solutions for HDInsight, check hello [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>

### <a name="cluster-versioning"></a><span data-ttu-id="409a8-114">Controllo delle versioni del cluster</span><span class="sxs-lookup"><span data-stu-id="409a8-114">Cluster versioning</span></span>

<span data-ttu-id="409a8-115">Hello pacchetto Microsoft.SCP.Net.SDK NuGet usato per il progetto deve corrispondere versione principale di hello di Storm installato in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="409a8-115">hello Microsoft.SCP.Net.SDK NuGet package you use for your project must match hello major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="409a8-116">HDInsight versioni 3.5 e 3.6 usa Storm versione 1.x, pertanto è necessario usare SCP.NET versione 1.0.x.x con questi cluster.</span><span class="sxs-lookup"><span data-stu-id="409a8-116">HDInsight versions 3.5 and 3.6 use Storm 1.x, so you must use SCP.NET version 1.0.x.x with these clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="409a8-117">esempio Hello in questo documento è previsto un 3.5 HDInsight o 3,6 cluster.</span><span class="sxs-lookup"><span data-stu-id="409a8-117">hello example in this document expects an HDInsight 3.5 or 3.6 cluster.</span></span>
>
> <span data-ttu-id="409a8-118">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="409a8-118">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="409a8-119">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="409a8-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="409a8-120">Le topologie C# devono inoltre puntare a .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="409a8-120">C# topologies must also target .NET 4.5.</span></span>

## <a name="how-toowork-with-event-hubs"></a><span data-ttu-id="409a8-121">Come toowork con hub eventi</span><span class="sxs-lookup"><span data-stu-id="409a8-121">How toowork with Event Hubs</span></span>

<span data-ttu-id="409a8-122">Microsoft fornisce un set di componenti Java che possono essere utilizzati toocommunicate con hub di eventi da una topologia di Storm.</span><span class="sxs-lookup"><span data-stu-id="409a8-122">Microsoft provides a set of Java components that can be used toocommunicate with Event Hubs from a Storm topology.</span></span> <span data-ttu-id="409a8-123">È possibile trovare i file di archivio (JAR) di Java hello che contiene una versione compatibile di HDInsight 3.6 di questi componenti in [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span><span class="sxs-lookup"><span data-stu-id="409a8-123">You can find hello Java archive (JAR) file that contains an HDInsight 3.6 compatible version of these components at [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="409a8-124">Mentre i componenti di hello sono scritti in Java, è possibile utilizzarli da una topologia c#.</span><span class="sxs-lookup"><span data-stu-id="409a8-124">While hello components are written in Java, you can easily use them from a C# topology.</span></span>

<span data-ttu-id="409a8-125">in questo esempio viene utilizzato i Hello seguenti componenti:</span><span class="sxs-lookup"><span data-stu-id="409a8-125">hello following components are used in this example:</span></span>

* <span data-ttu-id="409a8-126">__EventHubSpout__: legge i dati dagli Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="409a8-126">__EventHubSpout__: Reads data from Event Hubs.</span></span>
* <span data-ttu-id="409a8-127">__EventHubBolt__: scrive dati tooEvent hub.</span><span class="sxs-lookup"><span data-stu-id="409a8-127">__EventHubBolt__: Writes data tooEvent Hubs.</span></span>
* <span data-ttu-id="409a8-128">__EventHubSpoutConfig__: tooconfigure EventHubSpout utilizzato.</span><span class="sxs-lookup"><span data-stu-id="409a8-128">__EventHubSpoutConfig__: Used tooconfigure EventHubSpout.</span></span>
* <span data-ttu-id="409a8-129">__EventHubBoltConfig__: tooconfigure EventHubBolt utilizzato.</span><span class="sxs-lookup"><span data-stu-id="409a8-129">__EventHubBoltConfig__: Used tooconfigure EventHubBolt.</span></span>

### <a name="example-spout-usage"></a><span data-ttu-id="409a8-130">Esempio di uso di uno spout</span><span class="sxs-lookup"><span data-stu-id="409a8-130">Example spout usage</span></span>

<span data-ttu-id="409a8-131">SCP.NET fornisce metodi per l'aggiunta di una topologia di tooyour EventHubSpout.</span><span class="sxs-lookup"><span data-stu-id="409a8-131">SCP.NET provides methods for adding an EventHubSpout tooyour topology.</span></span> <span data-ttu-id="409a8-132">Questi metodi rendono più semplice tooadd beccuccio rispetto all'utilizzo di metodi generici hello per l'aggiunta di un componente di Java.</span><span class="sxs-lookup"><span data-stu-id="409a8-132">These methods make it easier tooadd a spout than using hello generic methods for adding a Java component.</span></span> <span data-ttu-id="409a8-133">Hello esempio seguente viene illustrato come toocreate beccuccio utilizzando hello __SetEventHubSpout__ e **EventHubSpoutConfig** metodi forniti da SCP.NET:</span><span class="sxs-lookup"><span data-stu-id="409a8-133">hello following example demonstrates how toocreate a spout by using hello __SetEventHubSpout__ and **EventHubSpoutConfig** methods provided by SCP.NET:</span></span>

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

<span data-ttu-id="409a8-134">esempio di Hello precedente crea un nuovo componente di beccuccio denominato __EventHubSpout__e lo configura toocommunicate con un hub eventi.</span><span class="sxs-lookup"><span data-stu-id="409a8-134">hello previous example creates a new spout component named __EventHubSpout__, and configures it toocommunicate with an event hub.</span></span> <span data-ttu-id="409a8-135">Hello parallelismo per il componente hello è impostato toohello numero di partizioni nell'hub eventi hello.</span><span class="sxs-lookup"><span data-stu-id="409a8-135">hello parallelism hint for hello component is set toohello number of partitions in hello event hub.</span></span> <span data-ttu-id="409a8-136">Questa impostazione consente di Storm toocreate un'istanza del componente hello per ogni partizione.</span><span class="sxs-lookup"><span data-stu-id="409a8-136">This setting allows Storm toocreate an instance of hello component for each partition.</span></span>

### <a name="example-bolt-usage"></a><span data-ttu-id="409a8-137">Esempio di utilizzo di bolt</span><span class="sxs-lookup"><span data-stu-id="409a8-137">Example bolt usage</span></span>

<span data-ttu-id="409a8-138">Hello utilizzare **JavaComponmentConstructor** toocreate metodo un'istanza di fulmine hello.</span><span class="sxs-lookup"><span data-stu-id="409a8-138">Use hello **JavaComponmentConstructor** method toocreate an instance of hello bolt.</span></span> <span data-ttu-id="409a8-139">Hello esempio seguente viene illustrato come toocreate e configurare una nuova istanza di hello **EventHubBolt**:</span><span class="sxs-lookup"><span data-stu-id="409a8-139">hello following example demonstrates how toocreate and configure a new instance of hello **EventHubBolt**:</span></span>

```csharp
// Java construcvtor for hello Event Hub Bolt
JavaComponentConstructor constructor = JavaComponentConstructor.CreateFromClojureExpr(
    String.Format(@"(org.apache.storm.eventhubs.bolt.EventHubBolt. (org.apache.storm.eventhubs.bolt.EventHubBoltConfig. " +
        @"""{0}"" ""{1}"" ""{2}"" ""{3}"" ""{4}"" {5}))",
        ConfigurationManager.AppSettings["EventHubPolicyName"],
        ConfigurationManager.AppSettings["EventHubPolicyKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        "servicebus.windows.net",
        ConfigurationManager.AppSettings["EventHubName"],
        "true"));

// Set hello bolt toosubscribe toodata from hello spout
topologyBuilder.SetJavaBolt(
    "eventhubbolt",
    constructor,
    partitionCount)
        .shuffleGrouping("Spout");
```

> [!NOTE]
> <span data-ttu-id="409a8-140">In questo esempio viene utilizzata un'espressione di Clojure passata come stringa, anziché utilizzare **JavaComponentConstructor** toocreate un **EventHubBoltConfig**, come esempio beccuccio hello.</span><span class="sxs-lookup"><span data-stu-id="409a8-140">This example uses a Clojure expression passed as a string, instead of using **JavaComponentConstructor** toocreate an **EventHubBoltConfig**, as hello spout example did.</span></span> <span data-ttu-id="409a8-141">Entrambi i metodi sono validi</span><span class="sxs-lookup"><span data-stu-id="409a8-141">Either method works.</span></span> <span data-ttu-id="409a8-142">Utilizzare il metodo hello che ritiene tooyou migliore.</span><span class="sxs-lookup"><span data-stu-id="409a8-142">Use hello method that feels best tooyou.</span></span>

## <a name="download-hello-completed-project"></a><span data-ttu-id="409a8-143">Scaricare il progetto hello completata</span><span class="sxs-lookup"><span data-stu-id="409a8-143">Download hello completed project</span></span>

<span data-ttu-id="409a8-144">È possibile scaricare una versione completa di hello progetto creato in questa esercitazione da [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="409a8-144">You can download a complete version of hello project created in this tutorial from [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span> <span data-ttu-id="409a8-145">Tuttavia, è comunque necessario tooprovide le impostazioni di configurazione seguendo i passaggi di hello in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="409a8-145">However, you still need tooprovide configuration settings by following hello steps in this tutorial.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="409a8-146">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="409a8-146">Prerequisites</span></span>

* <span data-ttu-id="409a8-147">Un [cluster Apache Storm in HDInsight versione 3.5 o 3.6](hdinsight-apache-storm-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="409a8-147">An [Apache Storm on HDInsight cluster version 3.5 or 3.6](hdinsight-apache-storm-tutorial-get-started.md).</span></span>

    > [!WARNING]
    > <span data-ttu-id="409a8-148">esempio Hello utilizzato in questo documento richiede Storm in HDInsight versione 3.5 o 3.6.</span><span class="sxs-lookup"><span data-stu-id="409a8-148">hello example used in this document requires Storm on HDInsight version 3.5 or 3.6.</span></span> <span data-ttu-id="409a8-149">Questo non funziona con le versioni precedenti di HDInsight, a causa di modifiche al nome di classe toobreaking.</span><span class="sxs-lookup"><span data-stu-id="409a8-149">This does not work with older versions of HDInsight, due toobreaking class name changes.</span></span> <span data-ttu-id="409a8-150">Per una versione di questo esempio funziona con i cluster precedenti, vedere [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span><span class="sxs-lookup"><span data-stu-id="409a8-150">For a version of this example that works with older clusters, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span></span>

* <span data-ttu-id="409a8-151">Un [Hub eventi di Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="409a8-151">An [Azure event hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="409a8-152">Hello [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="409a8-152">hello [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>

* <span data-ttu-id="409a8-153">Hello [strumenti HDInsight per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="409a8-153">hello [HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="409a8-154">Java JDK 1.8 o versione successiva nell'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="409a8-154">Java JDK 1.8 or later on your development environment.</span></span> <span data-ttu-id="409a8-155">Sono disponibili download di JDK da [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="409a8-155">JDK downloads are available from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>

  * <span data-ttu-id="409a8-156">Hello **JAVA_HOME** directory di toohello punto deve variabile di ambiente contenente Java.</span><span class="sxs-lookup"><span data-stu-id="409a8-156">hello **JAVA_HOME** environment variable must point toohello directory that contains Java.</span></span>
  * <span data-ttu-id="409a8-157">Hello **%JAVA_HOME%/bin** directory deve trovarsi nel percorso di hello.</span><span class="sxs-lookup"><span data-stu-id="409a8-157">hello **%JAVA_HOME%/bin** directory must be in hello path.</span></span>

## <a name="download-hello-event-hubs-components"></a><span data-ttu-id="409a8-158">Scaricare i componenti di hello hub eventi</span><span class="sxs-lookup"><span data-stu-id="409a8-158">Download hello Event Hubs components</span></span>

<span data-ttu-id="409a8-159">Download hello hub eventi spout e bullone componente da [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span><span class="sxs-lookup"><span data-stu-id="409a8-159">Download hello Event Hubs spout and bolt component from [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

<span data-ttu-id="409a8-160">Creare una directory denominata `eventhubspout`e salvarlo nella directory hello hello.</span><span class="sxs-lookup"><span data-stu-id="409a8-160">Create a directory named `eventhubspout`, and save hello file into hello directory.</span></span>

## <a name="configure-event-hubs"></a><span data-ttu-id="409a8-161">Configurare gli hub eventi</span><span class="sxs-lookup"><span data-stu-id="409a8-161">Configure Event Hubs</span></span>

<span data-ttu-id="409a8-162">Hub eventi è l'origine dati hello per questo esempio.</span><span class="sxs-lookup"><span data-stu-id="409a8-162">Event Hubs is hello data source for this example.</span></span> <span data-ttu-id="409a8-163">Utilizzare le informazioni di hello nella sezione "Creare un hub eventi" hello di [Introduzione agli hub di eventi](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="409a8-163">Use hello information in hello "Create an event hub" section of [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

1. <span data-ttu-id="409a8-164">Dopo aver creato l'hub di eventi hello, visualizzare hello **EventHub** pannello in hello Azure portale e selezionare **criteri di accesso condiviso**.</span><span class="sxs-lookup"><span data-stu-id="409a8-164">After hello event hub has been created, view hello **EventHub** blade in hello Azure portal, and select **Shared access policies**.</span></span> <span data-ttu-id="409a8-165">Selezionare **+ Aggiungi** hello tooadd seguenti criteri:</span><span class="sxs-lookup"><span data-stu-id="409a8-165">Select **+ Add** tooadd hello following policies:</span></span>

   | <span data-ttu-id="409a8-166">Nome</span><span class="sxs-lookup"><span data-stu-id="409a8-166">Name</span></span> | <span data-ttu-id="409a8-167">Autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="409a8-167">Permissions</span></span> |
   | --- | --- |
   | <span data-ttu-id="409a8-168">writer</span><span class="sxs-lookup"><span data-stu-id="409a8-168">writer</span></span> |<span data-ttu-id="409a8-169">Invio</span><span class="sxs-lookup"><span data-stu-id="409a8-169">Send</span></span> |
   | <span data-ttu-id="409a8-170">reader</span><span class="sxs-lookup"><span data-stu-id="409a8-170">reader</span></span> |<span data-ttu-id="409a8-171">Attesa</span><span class="sxs-lookup"><span data-stu-id="409a8-171">Listen</span></span> |

    ![Schermata della finestra Criteri di accesso condivisi](./media/hdinsight-storm-develop-csharp-event-hub-topology/sas.png)

2. <span data-ttu-id="409a8-173">Seleziona hello **lettore** e **writer** criteri.</span><span class="sxs-lookup"><span data-stu-id="409a8-173">Select hello **reader** and **writer** policies.</span></span> <span data-ttu-id="409a8-174">Copiare e salvare hello chiave primaria per entrambi i criteri, questi valori vengono utilizzati in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="409a8-174">Copy and save hello primary key value for both policies, as these values are used later.</span></span>

## <a name="configure-hello-eventhubwriter"></a><span data-ttu-id="409a8-175">Configurare hello EventHubWriter</span><span class="sxs-lookup"><span data-stu-id="409a8-175">Configure hello EventHubWriter</span></span>

1. <span data-ttu-id="409a8-176">Se non è già installato più recente degli strumenti di HDInsight hello hello per Visual Studio, vedere [iniziare a usare gli strumenti HDInsight per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="409a8-176">If you have not already installed hello latest version of hello HDInsight tools for Visual Studio, see [Get started using HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="409a8-177">Download soluzione di hello da [eventhub-storm-ibrida](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="409a8-177">Download hello solution from [eventhub-storm-hybrid](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

3. <span data-ttu-id="409a8-178">In hello **EventHubWriter** progetto, aprire hello **app** file.</span><span class="sxs-lookup"><span data-stu-id="409a8-178">In hello **EventHubWriter** project, open hello **App.config** file.</span></span> <span data-ttu-id="409a8-179">Utilizzare le informazioni di hello da hub di eventi hello di configurato toofill precedenti valore hello hello seguenti chiavi:</span><span class="sxs-lookup"><span data-stu-id="409a8-179">Use hello information from hello event hub that you configured earlier toofill in hello value for hello following keys:</span></span>

   | <span data-ttu-id="409a8-180">Chiave</span><span class="sxs-lookup"><span data-stu-id="409a8-180">Key</span></span> | <span data-ttu-id="409a8-181">Valore</span><span class="sxs-lookup"><span data-stu-id="409a8-181">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="409a8-182">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="409a8-182">EventHubPolicyName</span></span> |<span data-ttu-id="409a8-183">Writer (se è utilizzato un nome diverso per i criteri di hello con *inviare* autorizzazione, utilizzare tale.)</span><span class="sxs-lookup"><span data-stu-id="409a8-183">writer (If you used a different name for hello policy with *Send* permission, use it instead.)</span></span> |
   | <span data-ttu-id="409a8-184">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="409a8-184">EventHubPolicyKey</span></span> |<span data-ttu-id="409a8-185">chiave di Hello per criteri di writer hello.</span><span class="sxs-lookup"><span data-stu-id="409a8-185">hello key for hello writer policy.</span></span> |
   | <span data-ttu-id="409a8-186">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="409a8-186">EventHubNamespace</span></span> |<span data-ttu-id="409a8-187">spazio dei nomi Hello contenente dell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="409a8-187">hello namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="409a8-188">EventHubName</span><span class="sxs-lookup"><span data-stu-id="409a8-188">EventHubName</span></span> |<span data-ttu-id="409a8-189">Nome dell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="409a8-189">Your event hub name.</span></span> |
   | <span data-ttu-id="409a8-190">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="409a8-190">EventHubPartitionCount</span></span> |<span data-ttu-id="409a8-191">numero di Hello di partizioni nell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="409a8-191">hello number of partitions in your event hub.</span></span> |

4. <span data-ttu-id="409a8-192">Salvare e chiudere hello **app** file.</span><span class="sxs-lookup"><span data-stu-id="409a8-192">Save and close hello **App.config** file.</span></span>

## <a name="configure-hello-eventhubreader"></a><span data-ttu-id="409a8-193">Configurare hello EventHubReader</span><span class="sxs-lookup"><span data-stu-id="409a8-193">Configure hello EventHubReader</span></span>

1. <span data-ttu-id="409a8-194">Aprire hello **EventHubReader** progetto.</span><span class="sxs-lookup"><span data-stu-id="409a8-194">Open hello **EventHubReader** project.</span></span>

2. <span data-ttu-id="409a8-195">Aprire hello **app** file per hello **EventHubReader**.</span><span class="sxs-lookup"><span data-stu-id="409a8-195">Open hello **App.config** file for hello **EventHubReader**.</span></span> <span data-ttu-id="409a8-196">Utilizzare le informazioni di hello da hub di eventi hello di configurato toofill precedenti valore hello hello seguenti chiavi:</span><span class="sxs-lookup"><span data-stu-id="409a8-196">Use hello information from hello event hub that you configured earlier toofill in hello value for hello following keys:</span></span>

   | <span data-ttu-id="409a8-197">Chiave</span><span class="sxs-lookup"><span data-stu-id="409a8-197">Key</span></span> | <span data-ttu-id="409a8-198">Valore</span><span class="sxs-lookup"><span data-stu-id="409a8-198">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="409a8-199">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="409a8-199">EventHubPolicyName</span></span> |<span data-ttu-id="409a8-200">lettura (se è utilizzato un nome diverso per i criteri di hello con *ascolto* autorizzazione, utilizzare tale.)</span><span class="sxs-lookup"><span data-stu-id="409a8-200">reader (If you used a different name for hello policy with *listen* permission, use it instead.)</span></span> |
   | <span data-ttu-id="409a8-201">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="409a8-201">EventHubPolicyKey</span></span> |<span data-ttu-id="409a8-202">chiave di Hello per criteri di lettore hello.</span><span class="sxs-lookup"><span data-stu-id="409a8-202">hello key for hello reader policy.</span></span> |
   | <span data-ttu-id="409a8-203">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="409a8-203">EventHubNamespace</span></span> |<span data-ttu-id="409a8-204">spazio dei nomi Hello contenente dell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="409a8-204">hello namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="409a8-205">EventHubName</span><span class="sxs-lookup"><span data-stu-id="409a8-205">EventHubName</span></span> |<span data-ttu-id="409a8-206">Nome dell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="409a8-206">Your event hub name.</span></span> |
   | <span data-ttu-id="409a8-207">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="409a8-207">EventHubPartitionCount</span></span> |<span data-ttu-id="409a8-208">numero di Hello di partizioni nell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="409a8-208">hello number of partitions in your event hub.</span></span> |

3. <span data-ttu-id="409a8-209">Salvare e chiudere hello **app** file.</span><span class="sxs-lookup"><span data-stu-id="409a8-209">Save and close hello **App.config** file.</span></span>

## <a name="deploy-hello-topologies"></a><span data-ttu-id="409a8-210">Distribuire le topologie di hello</span><span class="sxs-lookup"><span data-stu-id="409a8-210">Deploy hello topologies</span></span>

1. <span data-ttu-id="409a8-211">Da **Esplora**, hello rapida **EventHubReader** del progetto e selezionare **inviare tooStorm in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="409a8-211">From **Solution Explorer**, right-click hello **EventHubReader** project, and select **Submit tooStorm on HDInsight**.</span></span>

    ![Schermata di Esplora soluzioni con tooStorm invia in HDInsight evidenziato](./media/hdinsight-storm-develop-csharp-event-hub-topology/submittostorm.png)

2. <span data-ttu-id="409a8-213">In hello **inviare topologia** la finestra di dialogo, seleziona il **Cluster Storm**.</span><span class="sxs-lookup"><span data-stu-id="409a8-213">On hello **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="409a8-214">Espandere **configurazioni aggiuntive**selezionare **i percorsi di File Java**selezionare **...** e selezionare hello directory che contiene i file JAR hello che è stato scaricato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="409a8-214">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select hello directory that contains hello JAR file that you downloaded earlier.</span></span> <span data-ttu-id="409a8-215">Infine fare clic su **Submit**.</span><span class="sxs-lookup"><span data-stu-id="409a8-215">Finally, click **Submit**.</span></span>

    ![Schermata della finestra di dialogo Submit Topology (Invia topologia)](./media/hdinsight-storm-develop-csharp-event-hub-topology/submit.png)

3. <span data-ttu-id="409a8-217">Quando è stata inviata la topologia hello, hello **Storm topologie Visualizzatore** viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="409a8-217">When hello topology has been submitted, hello **Storm Topologies Viewer** appears.</span></span> <span data-ttu-id="409a8-218">tooview informazioni sulla topologia di hello, seleziona hello **EventHubReader** topologia nel riquadro di sinistra hello.</span><span class="sxs-lookup"><span data-stu-id="409a8-218">tooview information about hello topology, select hello **EventHubReader** topology in hello left pane.</span></span>

    ![Schermata Storm Topologies Viewer (Visualizzatore topologie Storm)](./media/hdinsight-storm-develop-csharp-event-hub-topology/topologyviewer.png)

4. <span data-ttu-id="409a8-220">Da **Esplora**, hello rapida **EventHubWriter** del progetto e selezionare **inviare tooStorm in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="409a8-220">From **Solution Explorer**, right-click hello **EventHubWriter** project, and select **Submit tooStorm on HDInsight**.</span></span>

5. <span data-ttu-id="409a8-221">In hello **inviare topologia** la finestra di dialogo, seleziona il **Cluster Storm**.</span><span class="sxs-lookup"><span data-stu-id="409a8-221">On hello **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="409a8-222">Espandere **configurazioni aggiuntive**selezionare **i percorsi di File Java**selezionare **...** , e le directory hello select che contiene i file JAR hello scaricato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="409a8-222">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select hello directory that contains hello JAR file you downloaded earlier.</span></span> <span data-ttu-id="409a8-223">Infine fare clic su **Submit**.</span><span class="sxs-lookup"><span data-stu-id="409a8-223">Finally, click **Submit**.</span></span>

6. <span data-ttu-id="409a8-224">Quando è stata inviata la topologia hello, aggiornare l'elenco di topologia di hello in hello **Storm topologie Visualizzatore** tooverify che entrambe le topologie sono in esecuzione nel cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="409a8-224">When hello topology has been submitted, refresh hello topology list in hello **Storm Topologies Viewer** tooverify that both topologies are running on hello cluster.</span></span>

7. <span data-ttu-id="409a8-225">In **Storm topologie Visualizzatore**selezionare hello **EventHubReader** topologia.</span><span class="sxs-lookup"><span data-stu-id="409a8-225">In **Storm Topologies Viewer**, select hello **EventHubReader** topology.</span></span>

8. <span data-ttu-id="409a8-226">componente hello tooopen riepilogo fulmine hello, fare doppio clic su hello **LogBolt** componente nel diagramma hello.</span><span class="sxs-lookup"><span data-stu-id="409a8-226">tooopen hello component summary for hello bolt, double-click hello **LogBolt** component in hello diagram.</span></span>

9. <span data-ttu-id="409a8-227">In hello **executor** , selezionare uno dei collegamenti hello in hello **porta** colonna.</span><span class="sxs-lookup"><span data-stu-id="409a8-227">In hello **Executors** section, select one of hello links in hello **Port** column.</span></span> <span data-ttu-id="409a8-228">Consente di visualizzare informazioni registrate dal componente hello.</span><span class="sxs-lookup"><span data-stu-id="409a8-228">This displays information logged by hello component.</span></span> <span data-ttu-id="409a8-229">informazioni di Hello registrato sono simile toohello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="409a8-229">hello logged information is similar toohello following text:</span></span>

        2017-03-02 14:51:29.255 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,255 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1830978598,"deviceId":"8566ccbc-034d-45db-883d-d8a31f34068e"}
        2017-03-02 14:51:29.283 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,283 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1756413275,"deviceId":"647a5eff-823d-482f-a8b4-b95b35ae570b"}
        2017-03-02 14:51:29.313 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,312 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1108478910,"deviceId":"206a68fa-8264-4d61-9100-bfdb68ee8f0a"}

## <a name="stop-hello-topologies"></a><span data-ttu-id="409a8-230">Arrestare le topologie di hello</span><span class="sxs-lookup"><span data-stu-id="409a8-230">Stop hello topologies</span></span>

<span data-ttu-id="409a8-231">le topologie hello toostop, selezionare ogni topologia hello **Visualizzatore della topologia Storm**, quindi fare clic su **Kill**.</span><span class="sxs-lookup"><span data-stu-id="409a8-231">toostop hello topologies, select each topology in hello **Storm Topology Viewer**, then click **Kill**.</span></span>

![Schermata Storm Topology Viewer (Visualizzatore topologie Storm), con il pulsante Kill (Termina) evidenziato](./media/hdinsight-storm-develop-csharp-event-hub-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="409a8-233">Eliminare il cluster</span><span class="sxs-lookup"><span data-stu-id="409a8-233">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="409a8-234">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="409a8-234">Next steps</span></span>

<span data-ttu-id="409a8-235">In questo documento, si è appreso come toouse hello Java hub eventi spout e bullone da toowork una topologia c# con i dati in hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="409a8-235">In this document, you have learned how toouse hello Java Event Hubs spout and bolt from a C# topology toowork with data in Azure Event Hubs.</span></span> <span data-ttu-id="409a8-236">toolearn informazioni sulla creazione di topologie di c#, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="409a8-236">toolearn more about creating C# topologies, see hello following:</span></span>

* [<span data-ttu-id="409a8-237">Sviluppare topologie C# per Apache Storm in HDInsight tramite Visual Studio</span><span class="sxs-lookup"><span data-stu-id="409a8-237">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="409a8-238">Guida alla programmazione SCP</span><span class="sxs-lookup"><span data-stu-id="409a8-238">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)
* [<span data-ttu-id="409a8-239">Topologie di esempio per Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="409a8-239">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
