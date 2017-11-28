---
title: Usare lo streaming di Apache Spark con 	Hub eventi in Azure HDInsight | Microsoft Docs
description: Creare un esempio di streaming di Apache Spark su come inviare un flusso di dati a Hub eventi di Azure e quindi ricevere tali eventi nel cluster HDInsight Spark usando un'applicazione Scala.
keywords: streaming apache spark, streaming spark, esempio spark, esempio streaming spark apache, esempio azure hub eventi, esempio spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 68894e75-3ffa-47bd-8982-96cdad38b7d0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 175a2ad70b1f554d05846eb62fb685d4f259af7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="apache-spark-streaming-process-data-from-azure-event-hubs-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="2730b-104">Streaming Apache Spark: elaborare i dati dall'Hub eventi di Azure con il cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="2730b-104">Apache Spark streaming: Process data from Azure Event Hubs with Spark cluster on HDInsight</span></span>

<span data-ttu-id="2730b-105">In questo articolo si crea un esempio di streaming di Apache Spark che implica i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2730b-105">In this article, you create an Apache Spark streaming sample that involves the following steps:</span></span>

1. <span data-ttu-id="2730b-106">Usare un'applicazione autonoma per inserire messaggi in un Hub di eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="2730b-106">You use a standalone application to ingest messages into an Azure Event Hub.</span></span>

2. <span data-ttu-id="2730b-107">Esistono due approcci diversi per recuperare i messaggi dall'Hub eventi in tempo reale usando un'applicazione eseguita nel cluster Spark in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2730b-107">With two different approaches, you retrieve the messages from Event Hub in real-time using an application running in Spark cluster on Azure HDInsight.</span></span>

3. <span data-ttu-id="2730b-108">Compilare le pipeline analitiche sullo streaming per rendere persistenti i dati su sistemi di archiviazione diversi o ottenere informazioni dettagliate dai dati in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="2730b-108">You build streaming analytic pipelines to persist data to different storage systems, or get insights from data on the fly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2730b-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2730b-109">Prerequisites</span></span>

* <span data-ttu-id="2730b-110">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2730b-110">An Azure subscription.</span></span> <span data-ttu-id="2730b-111">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="2730b-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="2730b-112">Un cluster Apache Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2730b-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="2730b-113">Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="2730b-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="spark-streaming-concepts"></a><span data-ttu-id="2730b-114">Concetti relativi allo streaming Spark</span><span class="sxs-lookup"><span data-stu-id="2730b-114">Spark Streaming concepts</span></span>

<span data-ttu-id="2730b-115">Per una spiegazione dettagliata dello streaming Spark, vedere [Apache Spark streaming overview](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview) (Panoramica dello streaming in Apache Spark).</span><span class="sxs-lookup"><span data-stu-id="2730b-115">For a detailed explanation of Spark streaming, see [Apache Spark streaming overview](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span></span> <span data-ttu-id="2730b-116">HDInsight offre le stesse funzioni di streaming a un cluster Spark in Azure.</span><span class="sxs-lookup"><span data-stu-id="2730b-116">HDInsight brings the same streaming features to a Spark cluster on Azure.</span></span>  

## <a name="what-does-this-solution-do"></a><span data-ttu-id="2730b-117">Scopo di questa soluzione</span><span class="sxs-lookup"><span data-stu-id="2730b-117">What does this solution do?</span></span>

<span data-ttu-id="2730b-118">In questo articolo per creare un esempio di streaming Spark è necessario procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="2730b-118">In this article, to create a Spark streaming example, perform the following steps:</span></span>

1. <span data-ttu-id="2730b-119">Creare un Hub eventi di Azure che riceve un flusso di eventi.</span><span class="sxs-lookup"><span data-stu-id="2730b-119">Create an Azure Event Hub that will receive a stream of events.</span></span>

2. <span data-ttu-id="2730b-120">Eseguire un'applicazione autonoma locale che generi eventi e ne effettui il push all'Hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="2730b-120">Run a local standalone application that generates events and pushes it to the Azure Event Hub.</span></span> <span data-ttu-id="2730b-121">L'applicazione di esempio che esegue questa operazione è pubblicata all'indirizzo [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span><span class="sxs-lookup"><span data-stu-id="2730b-121">The sample application that does this is published at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span>

3. <span data-ttu-id="2730b-122">Eseguire un'applicazione di streaming in modalità remota in un cluster Spark che legge eventi di streaming provenienti dall'Hub di eventi di Azure ed eseguire varie analisi/elaborazioni di dati.</span><span class="sxs-lookup"><span data-stu-id="2730b-122">Run a streaming application remotely on a Spark cluster that reads streaming events from Azure Event Hub and perform various data processing/analysis.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="2730b-123">Creare un Hub di eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="2730b-123">Create an Azure Event Hub</span></span>

1. <span data-ttu-id="2730b-124">Accedere al [portale di Azure](https://ms.portal.azure.com) e fare clic su **Nuovo** nella parte superiore sinistra della schermata.</span><span class="sxs-lookup"><span data-stu-id="2730b-124">Log on to the [Azure Portal](https://ms.portal.azure.com), and click **New** at the top left of the screen.</span></span>

2. <span data-ttu-id="2730b-125">Fare clic su **Internet delle cose** e quindi su **Hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="2730b-125">Click **Internet of Things**, then click **Event Hubs**.</span></span>

    <span data-ttu-id="2730b-126">![Creare un hub eventi per l'esempio di streaming Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Creare un hub eventi per l'esempio di streaming Spark")</span><span class="sxs-lookup"><span data-stu-id="2730b-126">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Create event hub for Spark streaming example")</span></span>

3. <span data-ttu-id="2730b-127">Nel pannello **Crea spazio dei nomi** immettere un nome per lo spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="2730b-127">In the **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="2730b-128">scegliere il piano tariffario (Base o Standard).</span><span class="sxs-lookup"><span data-stu-id="2730b-128">choose the pricing tier (Basic or Standard).</span></span> <span data-ttu-id="2730b-129">Scegliere anche una sottoscrizione, un gruppo di risorse e una località di Azure in cui creare la risorsa.</span><span class="sxs-lookup"><span data-stu-id="2730b-129">Also, choose an Azure subscription, resource group, and location in which to create the resource.</span></span> <span data-ttu-id="2730b-130">Fare clic su **Crea** per creare lo spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="2730b-130">Click **Create** to create the namespace.</span></span>

      <span data-ttu-id="2730b-131">![Fornire un nome di hub eventi per l'esempio di streaming Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Fornire un nome di hub eventi per l'esempio di streaming Spark")</span><span class="sxs-lookup"><span data-stu-id="2730b-131">![Provide an event hub name for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Provide an event hub name for Spark streaming example")</span></span>

    > [!NOTE]
    > <span data-ttu-id="2730b-132">È necessario selezionare lo stesso **Percorso** del cluster Apache Spark in HDInsight per ridurre i costi e la latenza.</span><span class="sxs-lookup"><span data-stu-id="2730b-132">You should select the same **Location** as your Apache Spark cluster in HDInsight to reduce latency and costs.</span></span>
    >
    >

4. <span data-ttu-id="2730b-133">Nell'elenco degli spazi dei nomi di Hub eventi fare clic sullo spazio dei nomi appena creato.</span><span class="sxs-lookup"><span data-stu-id="2730b-133">In the Event Hubs namespace list, click the newly-created namespace.</span></span>      


5. <span data-ttu-id="2730b-134">Nel pannello dello spazio dei nomi, fare clic su **Hub eventi**, quindi fare clic su **+ Event Hub** (+ Hub eventi) per creare un nuovo Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="2730b-134">In the namespace blade, click **Event Hubs**, and then click **+ Event Hub** to create a new Event Hub.</span></span>
   
    <span data-ttu-id="2730b-135">![Creare un hub eventi per l'esempio di streaming Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Creare un hub eventi per l'esempio di streaming Spark")</span><span class="sxs-lookup"><span data-stu-id="2730b-135">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Create event hub for Spark streaming example")</span></span>

6. <span data-ttu-id="2730b-136">Digitare un nome per l'Hub eventi, impostare il numero di partizioni su 10 e la conservazione dei messaggi su 1.</span><span class="sxs-lookup"><span data-stu-id="2730b-136">Type a name for your Event Hub, set the partition count to 10, and message retention to 1.</span></span> <span data-ttu-id="2730b-137">In questa soluzione non vengono archiviati i messaggi, pertanto è consigliabile non modificare le impostazioni predefinite e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="2730b-137">We are not archiving the messages in this solution so you can leave the rest as default, and then click **Create**.</span></span>
   
    <span data-ttu-id="2730b-138">![Fornire i dettagli dell'hub eventi per l'esempio di streaming Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Fornire i dettagli dell'hub eventi per l'esempio di streaming Spark")</span><span class="sxs-lookup"><span data-stu-id="2730b-138">![Provide event hub details for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Provide event hub details for Spark streaming example")</span></span>

7. <span data-ttu-id="2730b-139">L'Hub eventi appena creato viene elencato nel pannello dell'Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="2730b-139">The newly created Event Hub is listed in the Event Hub blade.</span></span>
    
     <span data-ttu-id="2730b-140">![Visualizzare un hub eventi per l'esempio di streaming Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "Visualizzare un hub eventi per l'esempio di streaming Spark")</span><span class="sxs-lookup"><span data-stu-id="2730b-140">![View Event Hub for the Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "View Event Hub for the Spark streaming example")</span></span>

8. <span data-ttu-id="2730b-141">Nel pannello dello spazio dei nomi (non in quello dello specifico hub eventi) fare clic su **Criteri di accesso condivisi** e quindi su **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="2730b-141">Back in the namespace blade (not the specific Event Hub blade), click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
     <span data-ttu-id="2730b-142">![Impostare i criteri dell'hub eventi per l'esempio di streaming Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "Impostare i criteri dell'hub eventi per l'esempio di streaming Spark")</span><span class="sxs-lookup"><span data-stu-id="2730b-142">![Set Event Hub policies for the Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "Set Event Hub policies for the Spark streaming example")</span></span>

9. <span data-ttu-id="2730b-143">Fare clic sul pulsante di copia per copiare la chiave primaria **RootManageSharedAccessKey** e la stringa di connessione negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="2730b-143">Click the copy button to copy the **RootManageSharedAccessKey** primary key and connection string to the clipboard.</span></span> <span data-ttu-id="2730b-144">Salvarle per usarle più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2730b-144">Save these to use later in the tutorial.</span></span>
    
     <span data-ttu-id="2730b-145">![Visualizzare le chiavi dei criteri dell'hub eventi per l'esempio di streaming Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "Visualizzare le chiavi dei criteri dell'hub eventi per l'esempio di streaming Spark")</span><span class="sxs-lookup"><span data-stu-id="2730b-145">![View Event Hub policy keys for the Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "View Event Hub policy keys for the Spark streaming example")</span></span>

## <a name="send-messages-to-azure-event-hub-using-a-sample-scala-application"></a><span data-ttu-id="2730b-146">Usare un'applicazione Scala di esempio per inviare messaggi all'Hub eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="2730b-146">Send messages to Azure Event Hub using a sample Scala application</span></span>

<span data-ttu-id="2730b-147">In questa sezione si userà un'applicazione Scala locale autonoma che genera un flusso di eventi e lo invia all'Hub eventi di Azure creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2730b-147">In this section you use a standalone local Scala application that generates a stream of events and sends it to Azure Event Hub that you created earlier.</span></span> <span data-ttu-id="2730b-148">Questa applicazione è disponibile in GitHub all'indirizzo [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span><span class="sxs-lookup"><span data-stu-id="2730b-148">This application is available on GitHub at [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span></span> <span data-ttu-id="2730b-149">Questi passaggi presuppongono che sia già stato eseguito il fork di questo repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="2730b-149">The steps here assume that you have already forked this GitHub repository.</span></span>

1. <span data-ttu-id="2730b-150">Assicurarsi che nel computer in cui viene eseguita l'applicazione siano installati i prodotti seguenti.</span><span class="sxs-lookup"><span data-stu-id="2730b-150">Make sure you have the following installed on the computer where you run this application.</span></span>

    * <span data-ttu-id="2730b-151">Oracle Java Development Kit.</span><span class="sxs-lookup"><span data-stu-id="2730b-151">Oracle Java Development kit.</span></span> <span data-ttu-id="2730b-152">Per installarlo, fare clic [qui](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="2730b-152">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
    * <span data-ttu-id="2730b-153">Apache Maven.</span><span class="sxs-lookup"><span data-stu-id="2730b-153">Apache Maven.</span></span> <span data-ttu-id="2730b-154">È possibile scaricarlo [qui](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="2730b-154">You can download it from [here](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="2730b-155">Le istruzioni per scaricare Maven sono disponibili [qui](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="2730b-155">Instructions to install Maven are available [here](https://maven.apache.org/install.html).</span></span>

2. <span data-ttu-id="2730b-156">Aprire un prompt dei comandi e accedere alla posizione in cui è stato clonato il repository GitHub per l'applicazione di esempio Scala, quindi eseguire il comando seguente per compilare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2730b-156">Open a command prompt and navigate to the location you cloned the GitHub repo for the sample Scala application and run the following command to build the application.</span></span>

        mvn package

3. <span data-ttu-id="2730b-157">Il file di output con estensione jar per l'applicazione, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, viene creato in **/target** directory.</span><span class="sxs-lookup"><span data-stu-id="2730b-157">The output jar for the application, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, is created under **/target** directory.</span></span> <span data-ttu-id="2730b-158">Il file con estensione jar viene usato più avanti in questo articolo per testare la soluzione completa.</span><span class="sxs-lookup"><span data-stu-id="2730b-158">You use this JAR later in this article to test the complete solution.</span></span>

## <a name="create-application-to-receive-messages-from-event-hub-into-a-spark-cluster"></a><span data-ttu-id="2730b-159">Creare l'applicazione per ricevere messaggi dall'Hub eventi in un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="2730b-159">Create application to receive messages from Event Hub into a Spark cluster</span></span> 

<span data-ttu-id="2730b-160">Esistono due approcci per connettere lo streaming Spark e gli Hub eventi di Azure: la connessione basata su ricevitore e la connessione basata su DStream diretto.</span><span class="sxs-lookup"><span data-stu-id="2730b-160">We have two approaches to connect Spark Streaming and Azure Event Hubs, Receiver-based connection and Direct-DStream-based connection.</span></span> <span data-ttu-id="2730b-161">Quest'ultima è stata introdotta a gennaio 2017 con la versione 2.0.3.</span><span class="sxs-lookup"><span data-stu-id="2730b-161">Direct-DStream-based is introduced on Jan of 2017, in the 2.0.3 release.</span></span> <span data-ttu-id="2730b-162">Dal momento che è più efficiente e usa le risorse in modo più efficace, è destinata a sostituire la connessione originale basata su ricevitore.</span><span class="sxs-lookup"><span data-stu-id="2730b-162">It is supposed to replace the original receiver-based connection as it is more performant and resource-efficient.</span></span> <span data-ttu-id="2730b-163">Altre informazioni sono disponibili su [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span><span class="sxs-lookup"><span data-stu-id="2730b-163">More details found in [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span></span> <span data-ttu-id="2730b-164">DStream diretto supporta solo Spark 2.0 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="2730b-164">Direct DStream only supports Spark 2.0+.</span></span>

### <a name="build-applications-with-the-dependency-to-spark-eventhubs-connector"></a><span data-ttu-id="2730b-165">Compilazione di applicazioni con la dipendenza al connettore Spark-EventHubs</span><span class="sxs-lookup"><span data-stu-id="2730b-165">Build applications with the dependency to spark-eventhubs connector</span></span>

<span data-ttu-id="2730b-166">Verrà pubblicata anche la versione di gestione temporanea di Spark-EventHubs in GitHub.</span><span class="sxs-lookup"><span data-stu-id="2730b-166">We will also publish the staging version of Spark-EventHubs in GitHub.</span></span> <span data-ttu-id="2730b-167">Il primo passaggio per usare la versione di gestione temporanea di Spark-EventHubs consiste nell'indicare GitHub come repository di origine aggiungendo la voce seguente a pom.xml:</span><span class="sxs-lookup"><span data-stu-id="2730b-167">To use the staging version of Spark-EventHubs, the first step is to indicate GitHub as the source repo by adding the following entry to pom.xml:</span></span>

```xml
<repository>
      <id>spark-eventhubs</id>
      <url>https://raw.github.com/hdinsight/spark-eventhubs/maven-repo/</url>
      <snapshots>
        <enabled>true</enabled>
        <updatePolicy>always</updatePolicy>
      </snapshots>
</repository>
```

<span data-ttu-id="2730b-168">È quindi possibile aggiungere la dipendenza seguente al progetto per selezionare la versione pre-rilascio.</span><span class="sxs-lookup"><span data-stu-id="2730b-168">You can then add the following dependency to your project to take the pre-released version.</span></span>

<span data-ttu-id="2730b-169">Dipendenza Maven</span><span class="sxs-lookup"><span data-stu-id="2730b-169">Maven Dependency</span></span>

```xml
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11 -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>spark-streaming-eventhubs_2.11</artifactId>
    <version>2.0.4</version>
</dependency>
```

<span data-ttu-id="2730b-170">Dipendenza SBT</span><span class="sxs-lookup"><span data-stu-id="2730b-170">SBT Dependency</span></span>

```
// https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11
libraryDependencies += "com.microsoft.azure" % "spark-streaming-eventhubs_2.11" % "2.0.4"
```

### <a name="direct-dstream-connection"></a><span data-ttu-id="2730b-171">Connessione DStream diretto</span><span class="sxs-lookup"><span data-stu-id="2730b-171">Direct DStream Connection</span></span>

<span data-ttu-id="2730b-172">È possibile scaricare da [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar) un file con estensione jar preesistente contenente esempi di uso di DStream diretto.</span><span class="sxs-lookup"><span data-stu-id="2730b-172">A pre-built jar file containing examples using Direct DStream can be downloaded in [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).</span></span>

<span data-ttu-id="2730b-173">Il file con estensione jar contiene tre esempi i cui codici sorgente sono disponibili su [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span><span class="sxs-lookup"><span data-stu-id="2730b-173">The jar file contains three examples whose source code are available at [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span></span>

<span data-ttu-id="2730b-174">Prendere come esempio [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala):</span><span class="sxs-lookup"><span data-stu-id="2730b-174">Taking [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) as an example:</span></span>

```scala
private def createStreamingContext(
  sparkCheckpointDir: String,
  batchDuration: Int,
  namespace: String,
  eventHunName: String,
  eventhubParams: Map[String, String],
  progressDir: String) = {
val ssc = new StreamingContext(new SparkContext(), Seconds(batchDuration))
ssc.checkpoint(sparkCheckpointDir)
val inputDirectStream = EventHubsUtils.createDirectStreams(
  ssc,
  namespace,
  progressDir,
  Map(eventHunName -> eventhubParams))

inputDirectStream.map(receivedRecord => (new String(receivedRecord.getBody), 1)).
  reduceByKeyAndWindow((v1, v2) => v1 + v2, (v1, v2) => v1 - v2, Seconds(batchDuration * 3),
    Seconds(batchDuration)).print()

ssc
}

def main(args: Array[String]): Unit = {

if (args.length != 8) {
  println("Usage: program progressDir PolicyName PolicyKey EventHubNamespace EventHubName" +
    " BatchDuration(seconds) Spark_Checkpoint_Directory maxRate")
  sys.exit(1)
}

val progressDir = args(0)
val policyName = args(1)
val policykey = args(2)
val namespace = args(3)
val name = args(4)
val batchDuration = args(5).toInt
val sparkCheckpointDir = args(6)
val maxRate = args(7)

val eventhubParameters = Map[String, String] (
  "eventhubs.policyname" -> policyName,
  "eventhubs.policykey" -> policykey,
  "eventhubs.namespace" -> namespace,
  "eventhubs.name" -> name,
  "eventhubs.partition.count" -> "32",
  "eventhubs.consumergroup" -> "$Default",
  "eventhubs.maxRate" -> s"$maxRate"
)

val ssc = StreamingContext.getOrCreate(sparkCheckpointDir,
  () => createStreamingContext(sparkCheckpointDir, batchDuration, namespace, name,
    eventhubParameters, progressDir))

ssc.start()
ssc.awaitTermination()
}
```

<span data-ttu-id="2730b-175">Nell'esempio precedente, `eventhubParameters` si riferisce ai parametri specifici di una singola istanza EventHubs e deve essere trasferito all'API `createDirectStreams` che costruisce un mapping degli oggetti DStream diretto a uno spazio dei nomi dell'Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="2730b-175">In the above example, `eventhubParameters` are the parameters specific to a single EventHubs instance and you have to pass it to the `createDirectStreams` API which constructs a Direct DStream object mapping to a Event Hubs namespace.</span></span> <span data-ttu-id="2730b-176">Nell'oggetto DStream diretto, è possibile chiamare qualsiasi API DStream fornita dal framework dell'API di streaming Spark.</span><span class="sxs-lookup"><span data-stu-id="2730b-176">Over the Direct DStream object, you can call any DStream API provided by Spark Streaming API framework.</span></span> <span data-ttu-id="2730b-177">In questo esempio viene calcolata la frequenza di ogni parola negli ultimi 3 intervalli di micro batch.</span><span class="sxs-lookup"><span data-stu-id="2730b-177">In this example, we calculate the frequency of each word within the last 3 micro batch intervals.</span></span>

### <a name="receiver-based-connection"></a><span data-ttu-id="2730b-178">Connessioni basate su ricevitore</span><span class="sxs-lookup"><span data-stu-id="2730b-178">Receiver-based Connection</span></span>

<span data-ttu-id="2730b-179">Un'applicazione scritta in Scala di esempio di streaming Spark, che riceve gli eventi e li instrada a destinazioni diverse, è disponibile all'indirizzo [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span><span class="sxs-lookup"><span data-stu-id="2730b-179">A Spark streaming example application written in Scala, which receives events and route the to different destinations, is available at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span> <span data-ttu-id="2730b-180">Seguire questa procedura per aggiornare l'applicazione per la configurazione dell'Hub eventi e creare il file con estensione jar di output.</span><span class="sxs-lookup"><span data-stu-id="2730b-180">Follow the steps below to update the application for your Event Hub configuration and create the output jar.</span></span>

1. <span data-ttu-id="2730b-181">Avviare IntelliJ IDEA e dalla schermata di avvio selezionare **Check out from Version Control** (Estrai da controllo della versione) e quindi fare clic su **Git**.</span><span class="sxs-lookup"><span data-stu-id="2730b-181">Launch IntelliJ IDEA and from the launch screen select **Check out from Version Control** and then click **Git**.</span></span>
   
    <span data-ttu-id="2730b-182">![Esempio di streaming Apache Spark - Ottenere origini da Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Esempio di streaming Apache Spark - Ottenere origini da Git")</span><span class="sxs-lookup"><span data-stu-id="2730b-182">![Apache Spark streaming example - get sources from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark streaming example - get sources from Git")</span></span>

2. <span data-ttu-id="2730b-183">Nella finestra di dialogo **Clone Repository** (Clona repository) immettere l'URL del repository Git da cui eseguire la clonazione, specificare la directory da clonare e quindi fare clic su **Clone** (Clona).</span><span class="sxs-lookup"><span data-stu-id="2730b-183">In the **Clone Repository** dialog box, provide the URL to the Git repository to clone from, specify the directory to clone to, and then click **Clone**.</span></span>
   
    <span data-ttu-id="2730b-184">![Esempio di streaming Apache Spark - Clonare da Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Esempio di streaming Apache Spark - Clonare da Git")</span><span class="sxs-lookup"><span data-stu-id="2730b-184">![Apache Spark streaming example - clone from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark streaming example - clone from Git")</span></span>
3. <span data-ttu-id="2730b-185">Seguire le istruzioni finché la clonazione del progetto non sarà completa.</span><span class="sxs-lookup"><span data-stu-id="2730b-185">Follow the prompts till the project is completely cloned.</span></span> <span data-ttu-id="2730b-186">Premere **ALT+1** per aprire la **visualizzazione progetto**,</span><span class="sxs-lookup"><span data-stu-id="2730b-186">Press **Alt + 1** to open the **Project View**.</span></span> <span data-ttu-id="2730b-187">che dovrebbe essere simile alla seguente.</span><span class="sxs-lookup"><span data-stu-id="2730b-187">It should resemble the following.</span></span>
   
    <span data-ttu-id="2730b-188">![Esempio di streaming Apache Spark - Project View](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Esempio di streaming Apache Spark - Project View")</span><span class="sxs-lookup"><span data-stu-id="2730b-188">![Apache Spark streaming example - Project View](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark streaming example - Project View")</span></span>
4. <span data-ttu-id="2730b-189">Verificare che il codice dell'applicazione venga compilato con Java8.</span><span class="sxs-lookup"><span data-stu-id="2730b-189">Make sure the application code is compiled with Java8.</span></span> <span data-ttu-id="2730b-190">Per esserne certi, fare clic su **File** (File), quindi su **Project Structure** (Struttura progetto) e nella scheda **Project** (Progetto) verificare che Project language level (Livello del linguaggio di progetto) sia impostato su **8 - Lambdas, type annotations, etc.** (8 - Lambda, annotazioni tipo e così via).</span><span class="sxs-lookup"><span data-stu-id="2730b-190">To ensure this, click **File**, click **Project Structure**, and on the **Project** tab, make sure Project language level is set to **8 - Lambdas, type annotations, etc.**.</span></span>
   
    <span data-ttu-id="2730b-191">![Esempio di streaming Apache Spark - Impostare il compilatore](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Esempio di streaming Apache Spark - Impostare il compilatore")</span><span class="sxs-lookup"><span data-stu-id="2730b-191">![Apache Spark streaming example - Set compiler](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark streaming example - Set compiler")</span></span>
5. <span data-ttu-id="2730b-192">Aprire il file **pom.xml** e verificare che la versione di Spark sia corretta.</span><span class="sxs-lookup"><span data-stu-id="2730b-192">Open the **pom.xml** and make sure the Spark version is correct.</span></span> <span data-ttu-id="2730b-193">Nel nodo `<properties>` cercare il frammento seguente e verificare la versione di Spark.</span><span class="sxs-lookup"><span data-stu-id="2730b-193">Under `<properties>` node, look for the following snippet and verify the Spark version.</span></span>

        <scala.version>2.11.8</scala.version>
        <scala.compat.version>2.11.8</scala.compat.version>
        <scala.binary.version>2.11</scala.binary.version>
        <spark.version>2.0.0</spark.version>

6. <span data-ttu-id="2730b-194">L'applicazione richiede un file con estensione JAR di dipendenza denominato **JDBC driver jar** (Driver JDBC jar).</span><span class="sxs-lookup"><span data-stu-id="2730b-194">The application requires a dependency jar called **JDBC driver jar**.</span></span> <span data-ttu-id="2730b-195">È necessario per scrivere i messaggi ricevuti dall'Hub eventi in un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="2730b-195">This is required to write the messages received from Event Hub into an Azure SQL database.</span></span> <span data-ttu-id="2730b-196">È possibile scaricare la versione 4.1 o successiva di questo file con estensione jar [qui](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span><span class="sxs-lookup"><span data-stu-id="2730b-196">You can download this jar (v4.1 or later) from [here](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span></span> <span data-ttu-id="2730b-197">Aggiungere riferimenti a questo file con estensione jar nella libreria del progetto.</span><span class="sxs-lookup"><span data-stu-id="2730b-197">Add reference to this jar in the project library.</span></span> <span data-ttu-id="2730b-198">Eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2730b-198">Perform the following steps:</span></span>
     
     1. <span data-ttu-id="2730b-199">Nella finestra di IntelliJ IDEA in cui è aperta l'applicazione fare clic su **File** (File), su **Project Structure** (Struttura progetto) e quindi su **Libraries** (Librerie).</span><span class="sxs-lookup"><span data-stu-id="2730b-199">From IntelliJ IDEA window where you have the application open, click **File**, click **Project Structure**, and then click **Libraries**.</span></span> 
     2. <span data-ttu-id="2730b-200">Fare clic sull'icona di aggiunta (![icona per l'aggiunta](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), fare clic su **Java**e quindi passare al percorso in cui è stato scaricato il file con estensione jar del driver JDBC.</span><span class="sxs-lookup"><span data-stu-id="2730b-200">Click the add icon (![add icon](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), click **Java**, and then navigate to the location where you downloaded the JDBC driver jar.</span></span> <span data-ttu-id="2730b-201">Seguire le istruzioni per aggiungere il file con estensione jar alla libreria del progetto.</span><span class="sxs-lookup"><span data-stu-id="2730b-201">Follow the prompts to add the jar file to the project library.</span></span>

         <span data-ttu-id="2730b-202">![aggiungere dipendenze mancanti](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Aggiungere file JAR di dipendenza mancanti")</span><span class="sxs-lookup"><span data-stu-id="2730b-202">![add missing dependencies](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Add missing dependency jars")</span></span>
     3. <span data-ttu-id="2730b-203">Fare clic su **Apply**.</span><span class="sxs-lookup"><span data-stu-id="2730b-203">Click **Apply**.</span></span>

7. <span data-ttu-id="2730b-204">Creare il file con estensione jar di output.</span><span class="sxs-lookup"><span data-stu-id="2730b-204">Create the output jar file.</span></span> <span data-ttu-id="2730b-205">Eseguire i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="2730b-205">Perform the following steps.</span></span>

   1. <span data-ttu-id="2730b-206">Nella finestra di dialogo **Project Structure** (Struttura progetto) fare clic su **Artifacts** (Elementi) e quindi sul segno più.</span><span class="sxs-lookup"><span data-stu-id="2730b-206">In the **Project Structure** dialog box, click **Artifacts** and then click the plus symbol.</span></span> <span data-ttu-id="2730b-207">Nella finestra di dialogo popup fare clic su **JAR**, quindi fare clic su **From modules with dependencies** (Da moduli con dipendenze).</span><span class="sxs-lookup"><span data-stu-id="2730b-207">From the pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>      
       
       <span data-ttu-id="2730b-208">![Esempio di streaming Apache Spark - Creazione di un file con estensione jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Esempio di streaming Apache Spark - Creazione di un file con estensione jar")</span><span class="sxs-lookup"><span data-stu-id="2730b-208">![Apache Spark streaming example - create JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Apache Spark streaming example - create JAR")</span></span>
   2. <span data-ttu-id="2730b-209">Nella finestra di dialogo **Create JAR from Modules** (Crea JAR da moduli) fare clic sui puntini di sospensione (![puntini di sospensione](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) relativi a **Main Class** (Classe principale).</span><span class="sxs-lookup"><span data-stu-id="2730b-209">In the **Create JAR from Modules** dialog box, click the ellipsis (![ellipsis](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) against the **Main Class**.</span></span>
   3. <span data-ttu-id="2730b-210">Nella finestra di dialogo **Select Main Class** (Seleziona classe principale) selezionare una delle classi disponibili e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2730b-210">In the **Select Main Class** dialog box, select any of the available classes and then click **OK**.</span></span>
      
       <span data-ttu-id="2730b-211">![Esempio di streaming Apache Spark - Selezionare la classe per un file con estensione jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Esempio di streaming Apache Spark - Selezionare la classe per un file con estensione jar")</span><span class="sxs-lookup"><span data-stu-id="2730b-211">![Apache Spark streaming example - select class for jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark streaming example - select class for jar")</span></span>
   4. <span data-ttu-id="2730b-212">Nella finestra di dialogo **Create JAR from Modules** (Crea JAR da moduli) verificare che l'opzione per **estrarre nel file JAR di destinazione** sia selezionata e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2730b-212">In the **Create JAR from Modules** dialog box, make sure that the option to **extract to the target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="2730b-213">Verrà creato un singolo file con estensione jar con tutte le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="2730b-213">This creates a single JAR with all dependencies.</span></span>
      
       <span data-ttu-id="2730b-214">![Esempio di streaming Apache Spark - Creare un file con estensione jar dai moduli](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Esempio di streaming Apache Spark - Creare un file con estensione jar dai modul")</span><span class="sxs-lookup"><span data-stu-id="2730b-214">![Apache Spark streaming example - create jar from modules](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Apache Spark streaming example - create jar from modules")</span></span>
   5. <span data-ttu-id="2730b-215">Nella scheda **Output Layout** sono elencati tutti i file JAR inclusi nel progetto Maven.</span><span class="sxs-lookup"><span data-stu-id="2730b-215">The **Output Layout** tab lists all the jars that are included as part of the Maven project.</span></span> <span data-ttu-id="2730b-216">È possibile selezionare ed eliminare quelli in cui l'applicazione Scala non ha dipendenze dirette.</span><span class="sxs-lookup"><span data-stu-id="2730b-216">You can select and delete the ones on which the Scala application has no direct dependency.</span></span> <span data-ttu-id="2730b-217">Per l'applicazione che si sta creando è possibile rimuovere tutti i file tranne l'ultimo,**spark-streaming-data-persistence-examples compile output**.</span><span class="sxs-lookup"><span data-stu-id="2730b-217">For the application we are creating here, you can remove all but the last one (**spark-streaming-data-persistence-examples compile output**).</span></span> <span data-ttu-id="2730b-218">Selezionare i file JAR da eliminare e quindi fare clic sull'icona **Delete** (Elimina) (![icona di eliminazione](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span><span class="sxs-lookup"><span data-stu-id="2730b-218">Select the jars to delete and then click the **Delete** icon (![delete icon](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span></span>
      
       <span data-ttu-id="2730b-219">![Esempio di streaming Apache Spark - Eliminare i file con estensione jar estratti](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Esempio di streaming Apache Spark - Eliminare i file con estensione jar estratti")</span><span class="sxs-lookup"><span data-stu-id="2730b-219">![Apache Spark streaming example - delete extracted jars](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark streaming example - delete extracted jars")</span></span>
      
       <span data-ttu-id="2730b-220">Assicurarsi che la casella **Build on make** sia selezionata per garantire che il file jar venga creato ogni volta che il progetto viene creato o aggiornato.</span><span class="sxs-lookup"><span data-stu-id="2730b-220">Make sure **Build on make** box is selected, which ensures that the jar is created every time the project is built or updated.</span></span> <span data-ttu-id="2730b-221">Fare clic su **Apply**.</span><span class="sxs-lookup"><span data-stu-id="2730b-221">Click **Apply**.</span></span>
   6. <span data-ttu-id="2730b-222">Nella scheda **Output Layout** (Layout output) in fondo alla casella **Available Elements** (Elementi disponibili) sono disponibili i file JAR SQL JDBC aggiunti in precedenza alla libreria del progetto.</span><span class="sxs-lookup"><span data-stu-id="2730b-222">In the **Output Layout** tab, right at the bottom of the **Available Elements** box, you have the SQL JDBC jar that you added earlier to the project library.</span></span> <span data-ttu-id="2730b-223">È necessario aggiungerli alla scheda **Output Layout** . Fare clic con il pulsante destro del mouse sul file con estensione jar, quindi scegliere **Extract Into Output Root**.</span><span class="sxs-lookup"><span data-stu-id="2730b-223">You must add this to the **Output Layout** tab. Right-click the jar file, and then click **Extract Into Output Root**.</span></span>
      
       <span data-ttu-id="2730b-224">![Esempio di streaming Apache Spark - Estrarre file con estensione jar di dipendenza](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Esempio di streaming Apache Spark - Estrarre file con estensione jar di dipendenza")</span><span class="sxs-lookup"><span data-stu-id="2730b-224">![Apache Spark streaming example - extract dependency jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark streaming example - extract dependency jar")</span></span>  
      
       <span data-ttu-id="2730b-225">La scheda **Output Layout** dovrebbe essere simile alla seguente.</span><span class="sxs-lookup"><span data-stu-id="2730b-225">The **Output Layout** tab should now look like this.</span></span>
      
       <span data-ttu-id="2730b-226">![Esempio di streaming Apache Spark - Scheda output finale](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Esempio di streaming Apache Spark - Scheda output finale")</span><span class="sxs-lookup"><span data-stu-id="2730b-226">![Apache Spark streaming example - final output tab](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark streaming example - final output tab")</span></span>        
      
       <span data-ttu-id="2730b-227">Nella finestra di dialogo **Project Structure** (Struttura progetto) fare clic su **Apply** (Applica) e quindi su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2730b-227">In the **Project Structure** dialog box, click **Apply** and then click **OK**.</span></span>    
   7. <span data-ttu-id="2730b-228">Sulla barra dei menu fare clic su **Build** (Compila) e quindi su **Make Project** (Crea progetto).</span><span class="sxs-lookup"><span data-stu-id="2730b-228">From the menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="2730b-229">È anche possibile fare clic su **Build Artifacts** per creare il file JAR.</span><span class="sxs-lookup"><span data-stu-id="2730b-229">You can also click **Build Artifacts** to create the jar.</span></span> <span data-ttu-id="2730b-230">Il file JAR di output viene creato in **\classes\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="2730b-230">The output jar is created under **\classes\artifacts**.</span></span>
      
       <span data-ttu-id="2730b-231">![Esempio di streaming Apache Spark - Output dei file con estensione jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Esempio di streaming Apache Spark - Output dei file con estensione jar")</span><span class="sxs-lookup"><span data-stu-id="2730b-231">![Apache Spark streaming example - output JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Apache Spark streaming example - output JAR")</span></span>

## <a name="run-the-application-remotely-on-a-spark-cluster-using-livy"></a><span data-ttu-id="2730b-232">Eseguire l'applicazione in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="2730b-232">Run the application remotely on a Spark cluster using Livy</span></span>

<span data-ttu-id="2730b-233">In questo articolo si usa Livy per eseguire l'applicazione di streaming Apache Spark in modalità remota in un cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="2730b-233">In this article you use Livy to run the Apache Spark streaming application remotely on a Spark cluster.</span></span> <span data-ttu-id="2730b-234">Per informazioni dettagliate sull'uso di Livy il cluster Spark HDInsight, vedere [Inviare processi in modalità remota a un cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="2730b-234">For detailed discussion on how to use Livy with HDInsight Spark cluster, see [Submit jobs remotely to an Apache Spark cluster on Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span> <span data-ttu-id="2730b-235">Prima di avviare l'esecuzione dell'applicazione di streaming Spark, eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="2730b-235">Before you can start running the Spark streaming application, there are a couple of things you should do:</span></span>

1. <span data-ttu-id="2730b-236">Avviare l'applicazione autonoma locale per generare eventi e inviarli all'Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="2730b-236">Start the local standalone application to generate events and sent to Event Hub.</span></span> <span data-ttu-id="2730b-237">A questo scopo, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2730b-237">Use the following command to do so:</span></span>

        java -cp com-microsoft-azure-eventhubs-client-example-0.2.0.jar com.microsoft.eventhubs.client.example.EventhubsClientDriver --eventhubs-namespace "mysbnamespace" --eventhubs-name "myeventhub" --policy-name "mysendpolicy" --policy-key "<policy key>" --message-length 32 --thread-count 32 --message-count -1

2. <span data-ttu-id="2730b-238">Copiare il file con estensione JAR di streaming (**spark-streaming-data-persistence-examples.jar**) nell'archivio BLOB di Azure associato al cluster.</span><span class="sxs-lookup"><span data-stu-id="2730b-238">Copy the streaming jar (**spark-streaming-data-persistence-examples.jar**) to the Azure Blob storage associated with the cluster.</span></span> <span data-ttu-id="2730b-239">Questa operazione rende il file con estensione jar accessibile a Livy.</span><span class="sxs-lookup"><span data-stu-id="2730b-239">This makes the jar accessible to Livy.</span></span> <span data-ttu-id="2730b-240">A tale scopo è possibile usare [**AzCopy**](../storage/common/storage-use-azcopy.md), un'utilità della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="2730b-240">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, to do so.</span></span> <span data-ttu-id="2730b-241">Sono disponibili molti altri client da usare per caricare i dati.</span><span class="sxs-lookup"><span data-stu-id="2730b-241">There are a lot of other clients you can use to upload data.</span></span> <span data-ttu-id="2730b-242">Altre informazioni su questi client sono disponibili in [Caricare dati per processi Hadoop in HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="2730b-242">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
3. <span data-ttu-id="2730b-243">Installare CURL nel computer in cui si eseguono tali applicazioni.</span><span class="sxs-lookup"><span data-stu-id="2730b-243">Install CURL on the computer where you are running these applications from.</span></span> <span data-ttu-id="2730b-244">CURL viene usato per richiamare gli endpoint Livy per eseguire i processi in modalità remota.</span><span class="sxs-lookup"><span data-stu-id="2730b-244">We use CURL to invoke the Livy endpoints to run the jobs remotely.</span></span>

### <a name="run-the-spark-streaming-application-to-receive-the-events-into-an-azure-storage-blob-as-text"></a><span data-ttu-id="2730b-245">Eseguire l'applicazione di streaming Spark per ricevere gli eventi in un BLOB del servizio di archiviazione di Azure come testo</span><span class="sxs-lookup"><span data-stu-id="2730b-245">Run the Spark streaming application to receive the events into an Azure Storage Blob as text</span></span>

<span data-ttu-id="2730b-246">Aprire un prompt dei comandi, passare alla directory in cui è installato CURL ed eseguire il comando seguente (sostituire nome utente/password e nome cluster):</span><span class="sxs-lookup"><span data-stu-id="2730b-246">Open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputBlob.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="2730b-247">I parametri nel file **inputBlob.txt** sono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="2730b-247">The parameters in the file **inputBlob.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsEventCount", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="2730b-248">Ecco una descrizione dei parametri nel file di input:</span><span class="sxs-lookup"><span data-stu-id="2730b-248">Let us understand what the parameters in the input file are:</span></span>

* <span data-ttu-id="2730b-249">**file** è il percorso del file JAR dell'applicazione è già stato copiato nell'account di archiviazione di Azure associato al cluster.</span><span class="sxs-lookup"><span data-stu-id="2730b-249">**file** is the path to the application jar file on the Azure storage account associated with the cluster.</span></span>
* <span data-ttu-id="2730b-250">**className** è il nome della classe nel file JAR.</span><span class="sxs-lookup"><span data-stu-id="2730b-250">**className** is the name of the class in the jar.</span></span>
* <span data-ttu-id="2730b-251">**args** è l'elenco di argomenti richiesti dalla classe.</span><span class="sxs-lookup"><span data-stu-id="2730b-251">**args** is the list of arguments required by the class</span></span>
* <span data-ttu-id="2730b-252">**numExecutors** è il numero di core usati da Spark per eseguire l'applicazione di streaming.</span><span class="sxs-lookup"><span data-stu-id="2730b-252">**numExecutors** is the number of cores used by Spark to run the streaming application.</span></span> <span data-ttu-id="2730b-253">Deve essere sempre almeno il doppio del numero di partizioni dell'Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="2730b-253">This should always be at least twice the number of Event Hub partitions.</span></span>
* <span data-ttu-id="2730b-254">**executorMemory**, **executorCores**, **driverMemory** sono i parametri usati per assegnare le risorse richieste per l'applicazione di streaming.</span><span class="sxs-lookup"><span data-stu-id="2730b-254">**executorMemory**, **executorCores**, **driverMemory** are parameters used to assign required resources to the streaming application.</span></span>

> [!NOTE]
> <span data-ttu-id="2730b-255">Non è necessario creare le cartelle di output (EventCheckpoint, EventCount/EventCount10) usate come parametri,</span><span class="sxs-lookup"><span data-stu-id="2730b-255">You do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="2730b-256">perché vengono create automaticamente dall'applicazione di streaming.</span><span class="sxs-lookup"><span data-stu-id="2730b-256">The streaming application creates them for you.</span></span>
>
>

<span data-ttu-id="2730b-257">Quando si esegue il comando, viene visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="2730b-257">When you run the command, you should see an output like the following:</span></span>

    < HTTP/1.1 201 Created
    < Content-Type: application/json; charset=UTF-8
    < Location: /18
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Tue, 01 Dec 2015 05:39:10 GMT
    < Content-Length: 37
    <
    {"id":1,"state":"starting","log":[]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact

<span data-ttu-id="2730b-258">Prendere nota dell'ID batch nell'ultima riga dell'output. In questo esempio è "1".</span><span class="sxs-lookup"><span data-stu-id="2730b-258">Make a note of the batch ID in the last line of the output (in this example it is '1').</span></span> <span data-ttu-id="2730b-259">Per verificare che l'applicazione venga eseguita correttamente, è possibile esaminare l'account di archiviazione di Azure associato al cluster, dove sarà visualizzata la cartella **/EventCount/EventCount10** creata.</span><span class="sxs-lookup"><span data-stu-id="2730b-259">To verify that the application runs successfully, you can look at your Azure storage account associated with the cluster and you should see the **/EventCount/EventCount10** folder created there.</span></span> <span data-ttu-id="2730b-260">Questa cartella contiene i BLOB che acquisiscono il numero di eventi elaborati durante il periodo di tempo specificato per il parametro **batch-interval-in-seconds**.</span><span class="sxs-lookup"><span data-stu-id="2730b-260">This folder should contain blobs that captures the number of events processed within the time period specified for the parameter **batch-interval-in-seconds**.</span></span>

<span data-ttu-id="2730b-261">L'esecuzione dell'applicazione di streaming Spark continuerà fino a quando non viene terminata.</span><span class="sxs-lookup"><span data-stu-id="2730b-261">The Spark streaming application will continue to run until you kill it.</span></span> <span data-ttu-id="2730b-262">A questo scopo, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2730b-262">To do so, use the following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/1"

### <a name="run-the-applications-to-receive-the-events-into-an-azure-storage-blob-as-json"></a><span data-ttu-id="2730b-263">Eseguire le applicazioni per ricevere gli eventi in un BLOB di archiviazione di Azure come JSON</span><span class="sxs-lookup"><span data-stu-id="2730b-263">Run the applications to receive the events into an Azure Storage Blob as JSON</span></span>
<span data-ttu-id="2730b-264">Aprire un prompt dei comandi, passare alla directory in cui è installato CURL ed eseguire il comando seguente (sostituire nome utente/password e nome cluster):</span><span class="sxs-lookup"><span data-stu-id="2730b-264">Open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputJSON.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="2730b-265">I parametri nel file **inputJSON.txt** sono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="2730b-265">The parameters in the file **inputJSON.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureBlobAsJSON", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-store-folder", "/EventStore10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="2730b-266">I parametri sono simili a quanto specificato per l'output di testo nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="2730b-266">The parameters are similar to what you specified for the text output, in the previous step.</span></span> <span data-ttu-id="2730b-267">Anche in questo caso non è necessario creare le cartelle di output (EventCheckpoint, EventCount/EventCount10) usate come parametri,</span><span class="sxs-lookup"><span data-stu-id="2730b-267">Again, you do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="2730b-268">perché vengono create automaticamente dall'applicazione di streaming.</span><span class="sxs-lookup"><span data-stu-id="2730b-268">The streaming application creates them for you.</span></span>

 <span data-ttu-id="2730b-269">Dopo l'esecuzione del comando, è possibile esaminare l'account di archiviazione di Azure associato al cluster, dove sarà visualizzata la cartella **/EventStore10** creata.</span><span class="sxs-lookup"><span data-stu-id="2730b-269">After you run the command, you can look at your Azure storage account associated with the cluster and you should see the **/EventStore10** folder created there.</span></span> <span data-ttu-id="2730b-270">Aprire un file qualsiasi con prefisso **part-** dove saranno visualizzati gli eventi elaborati in un formato JSON.</span><span class="sxs-lookup"><span data-stu-id="2730b-270">Open any file prefixed with **part-** and you should see the events processed in a JSON format.</span></span>

### <a name="run-the-applications-to-receive-the-events-into-a-hive-table"></a><span data-ttu-id="2730b-271">Eseguire le applicazioni per ricevere gli eventi in una tabella Hive</span><span class="sxs-lookup"><span data-stu-id="2730b-271">Run the applications to receive the events into a Hive table</span></span>
<span data-ttu-id="2730b-272">Per eseguire l'applicazione di streaming Spark che trasmette eventi a una tabella Hive, sono necessari alcuni componenti aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="2730b-272">To run the Spark streaming application that streams events into a Hive table you need some additional components.</span></span> <span data-ttu-id="2730b-273">Si tratta di:</span><span class="sxs-lookup"><span data-stu-id="2730b-273">These are:</span></span>

* <span data-ttu-id="2730b-274">datanucleus-api-jdo-3.2.6.jar</span><span class="sxs-lookup"><span data-stu-id="2730b-274">datanucleus-api-jdo-3.2.6.jar</span></span>
* <span data-ttu-id="2730b-275">datanucleus-rdbms-3.2.9.jar</span><span class="sxs-lookup"><span data-stu-id="2730b-275">datanucleus-rdbms-3.2.9.jar</span></span>
* <span data-ttu-id="2730b-276">datanucleus-core-3.2.10.jar</span><span class="sxs-lookup"><span data-stu-id="2730b-276">datanucleus-core-3.2.10.jar</span></span>
* <span data-ttu-id="2730b-277">hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="2730b-277">hive-site.xml</span></span>

<span data-ttu-id="2730b-278">I file con estensione **jar** sono disponibili nel cluster HDInsight Spark in `/usr/hdp/current/spark-client/lib`.</span><span class="sxs-lookup"><span data-stu-id="2730b-278">The **.jar** files are available on your HDInsight Spark cluster at `/usr/hdp/current/spark-client/lib`.</span></span> <span data-ttu-id="2730b-279">Il file **hive-site.xml** è disponibile in `/usr/hdp/current/spark-client/conf`.</span><span class="sxs-lookup"><span data-stu-id="2730b-279">The **hive-site.xml** is available at `/usr/hdp/current/spark-client/conf`.</span></span>

<span data-ttu-id="2730b-280">È possibile usare [WinScp](http://winscp.net/eng/download.php) per copiare i file dal cluster nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="2730b-280">You can use [WinScp](http://winscp.net/eng/download.php) to copy over these files from the cluster to your local computer.</span></span> <span data-ttu-id="2730b-281">È quindi possibile usare strumenti per copiare questi file nell'account di archiviazione associato al cluster.</span><span class="sxs-lookup"><span data-stu-id="2730b-281">You can then use tools to copy these files over to your storage account associated with the cluster.</span></span> <span data-ttu-id="2730b-282">Per altre informazioni su come caricare i file nell'account di archiviazione, vedere [Caricare dati per processi Hadoop in HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="2730b-282">For more information on how to upload files to the storage account, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

<span data-ttu-id="2730b-283">Dopo avere copiato i file nell'account di archiviazione di Azure, aprire un prompt dei comandi, passare alla directory in cui è installato CURL ed eseguire il comando seguente (sostituire nome utente/password e nome cluster):</span><span class="sxs-lookup"><span data-stu-id="2730b-283">Once you have copied over the files to your Azure storage account, open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputHive.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="2730b-284">I parametri nel file **inputHive.txt** sono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="2730b-284">The parameters in the file **inputHive.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToHiveTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-hive-table", "EventHiveTable10" ], "jars":["wasb:///example/jars/datanucleus-api-jdo-3.2.6.jar", "wasb:///example/jars/datanucleus-rdbms-3.2.9.jar", "wasb:///example/jars/datanucleus-core-3.2.10.jar"], "files":["wasb:///example/jars/hive-site.xml"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="2730b-285">I parametri sono simili a quanto specificato per l'output di testo nei passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="2730b-285">The parameters are similar to what you specified for the text output, in the previous steps.</span></span> <span data-ttu-id="2730b-286">Anche in questo caso non è necessario creare la tabella Hive di output (EventHiveTable10) o le cartelle di output (EventCheckpoint, EventCount/EventCount10) usate come parametri,</span><span class="sxs-lookup"><span data-stu-id="2730b-286">Again, you do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) or the output Hive table (EventHiveTable10) that are used as parameters.</span></span> <span data-ttu-id="2730b-287">perché vengono create automaticamente dall'applicazione di streaming.</span><span class="sxs-lookup"><span data-stu-id="2730b-287">The streaming application creates them for you.</span></span> <span data-ttu-id="2730b-288">Si noti che le opzioni **jars** e **files** includono i percorsi per i file JAR e il file hive-site.xml copiato nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2730b-288">Note that the **jars** and **files** option includes paths to the .jar files and the hive-site.xml that you copied over to the storage account.</span></span>

<span data-ttu-id="2730b-289">Per verificare che la tabella Hive sia stata creata correttamente, è possibile usare SSH nel cluster ed eseguire query Hive.</span><span class="sxs-lookup"><span data-stu-id="2730b-289">To verify that the hive table was successfully created, you can SSH into the cluster and run Hive queries.</span></span> <span data-ttu-id="2730b-290">Per istruzioni, vedere [Usare Hive con Hadoop in HDInsight tramite SSH](hdinsight-hadoop-use-hive-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="2730b-290">For instructions, see [Use Hive with Hadoop in HDInsight with SSH](hdinsight-hadoop-use-hive-ssh.md).</span></span> <span data-ttu-id="2730b-291">Una volta connessi tramite SSH, è possibile eseguire il comando seguente per verificare che la tabella Hive, **EventHiveTable10**, venga creata.</span><span class="sxs-lookup"><span data-stu-id="2730b-291">Once you are connected using SSH, you can run the following command to verify that the Hive table, **EventHiveTable10**, is created.</span></span>

    show tables;

<span data-ttu-id="2730b-292">L'output dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="2730b-292">You should see an output similar to the following:</span></span>

    OK
    eventhivetable10
    hivesampletable

<span data-ttu-id="2730b-293">È anche possibile eseguire una query SELECT per visualizzare il contenuto della tabella.</span><span class="sxs-lookup"><span data-stu-id="2730b-293">You can also run a SELECT query to view the contents of the table.</span></span>

    SELECT * FROM eventhivetable10 LIMIT 10;

<span data-ttu-id="2730b-294">Verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="2730b-294">You should see an output like the following:</span></span>

    ZN90apUSQODDTx7n6Toh6jDbuPngqT4c
    sor2M7xsFwmaRW8W8NDwMneFNMrOVkW1
    o2HcsU735ejSi2bGEcbUSB4btCFmI1lW
    TLuibq4rbj0T9st9eEzIWJwNGtMWYoYS
    HKCpPlWFWAJILwR69MAq863nCWYzDEw6
    Mvx0GQOPYvPR7ezBEpIHYKTKiEhYammQ
    85dRppSBSbZgThLr1s0GMgKqynDUqudr
    5LAWkNqorLj3ZN9a2mfWr9rZqeXKN4pF
    ulf9wSFNjD7BZXCyunozecov9QpEIYmJ
    vWzM3nvOja8DhYcwn0n5eTfOItZ966pa
    Time taken: 4.434 seconds, Fetched: 10 row(s)


### <a name="run-the-applications-to-receive-the-events-into-an-azure-sql-database-table"></a><span data-ttu-id="2730b-295">Eseguire le applicazioni per ricevere gli eventi in una tabella di database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="2730b-295">Run the applications to receive the events into an Azure SQL database table</span></span>
<span data-ttu-id="2730b-296">Prima di eseguire questo passaggio, assicurarsi che sia stato creato un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="2730b-296">Before running this step, make sure you have an Azure SQL database created.</span></span> <span data-ttu-id="2730b-297">Per istruzioni, vedere [Creare un database SQL in pochi minuti](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2730b-297">For instructions, see [Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span> <span data-ttu-id="2730b-298">Per completare questa sezione saranno necessari i valori per il nome del database, il nome del server di database e le credenziali di amministratore del database come parametri.</span><span class="sxs-lookup"><span data-stu-id="2730b-298">To complete this section, you need values for database name, database server name, and the database administrator credentials as parameters.</span></span> <span data-ttu-id="2730b-299">Non è però necessario creare la tabella di database,</span><span class="sxs-lookup"><span data-stu-id="2730b-299">You do not need to create the database table though.</span></span> <span data-ttu-id="2730b-300">perché viene creata automaticamente dall'applicazione di streaming Spark.</span><span class="sxs-lookup"><span data-stu-id="2730b-300">The Spark streaming application creates that for you.</span></span>

<span data-ttu-id="2730b-301">Aprire un prompt dei comandi, passare alla directory in cui è installato CURL ed eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2730b-301">Open a command prompt, navigate to the directory where you installed CURL, and run the following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputSQL.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="2730b-302">I parametri nel file **inputSQL.txt** sono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="2730b-302">The parameters in the file **inputSQL.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureSQLTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--sql-server-fqdn", "<database-server-name>.database.windows.net", "--sql-database-name", "mysparkdatabase", "--database-username", "sparkdbadmin", "--database-password", "<put-password-here>", "--event-sql-table", "EventContent" ], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="2730b-303">Per verificare che l'applicazione venga eseguita correttamente, è possibile connettersi al database SQL di Azure con SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="2730b-303">To verify that the application runs successfully, you can connect to the Azure SQL database using SQL Server Management Studio.</span></span> <span data-ttu-id="2730b-304">Per istruzioni su come eseguire questa operazione, vedere [Connettersi al database SQL con SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="2730b-304">For instructions on how to do that, see [Connect to SQL Database with SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md).</span></span> <span data-ttu-id="2730b-305">Una volta connessi al database, è possibile passare alla tabella il **EventContent** creata dall'applicazione di streaming.</span><span class="sxs-lookup"><span data-stu-id="2730b-305">Once you are connected to the database, you can navigate to the **EventContent** table that was created by the streaming application.</span></span> <span data-ttu-id="2730b-306">È possibile eseguire una query rapida per ottenere i dati dalla tabella.</span><span class="sxs-lookup"><span data-stu-id="2730b-306">You can run a quick query to get the data from the table.</span></span> <span data-ttu-id="2730b-307">Eseguire questa query:</span><span class="sxs-lookup"><span data-stu-id="2730b-307">Run the following query:</span></span>

    SELECT * FROM EventCount

<span data-ttu-id="2730b-308">L'output dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="2730b-308">You should see output similar to the following:</span></span>

    00046b0f-2552-4980-9c3f-8bba5647c8ee
    000b7530-12f9-4081-8e19-90acd26f9c0c
    000bc521-9c1b-4a42-ab08-dc1893b83f3b
    00123a2a-e00d-496a-9104-108920955718
    0017c68f-7a4e-452d-97ad-5cb1fe5ba81b
    001KsmqL2gfu5ZcuQuTqTxQvVyGCqPp9
    001vIZgOStka4DXtud0e3tX7XbfMnZrN
    00220586-3e1a-4d2d-a89b-05c5892e541a
    0029e309-9e54-4e1b-84be-cd04e6fce5ec
    003333cf-874f-4045-9da3-9f98c2b4ea49
    0043c07e-8d73-420a-9af7-1fcb94575356
    004a11a9-0c2c-4bc0-a7d5-2e0ebd947ab9


## <span data-ttu-id="2730b-309"><a name="seealso"></a>Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2730b-309"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="2730b-310">Panoramica: Apache Spark su Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="2730b-310">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)
* [<span data-ttu-id="2730b-311">Design of Receiver-based Connection and Direct DStream</span><span class="sxs-lookup"><span data-stu-id="2730b-311">Design of Receiver-based Connection and Direct DStream</span></span>](https://www.slideshare.net/NanZhu/seattle-sparkmeetup032317)

### <a name="scenarios"></a><span data-ttu-id="2730b-312">Scenari</span><span class="sxs-lookup"><span data-stu-id="2730b-312">Scenarios</span></span>
* [<span data-ttu-id="2730b-313">Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="2730b-313">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="2730b-314">Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC</span><span class="sxs-lookup"><span data-stu-id="2730b-314">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="2730b-315">Spark con Machine Learning: usare Spark in HDInsight per prevedere i risultati del controllo degli alimenti</span><span class="sxs-lookup"><span data-stu-id="2730b-315">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="2730b-316">Analisi dei log del sito Web con Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="2730b-316">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="2730b-317">Creare ed eseguire applicazioni</span><span class="sxs-lookup"><span data-stu-id="2730b-317">Create and run applications</span></span>
* [<span data-ttu-id="2730b-318">Creare un'applicazione autonoma con Scala</span><span class="sxs-lookup"><span data-stu-id="2730b-318">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="2730b-319">Eseguire processi in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="2730b-319">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="2730b-320">Strumenti ed estensioni</span><span class="sxs-lookup"><span data-stu-id="2730b-320">Tools and extensions</span></span>
* [<span data-ttu-id="2730b-321">Usare il plug-in degli strumenti HDInsight per IntelliJ IDEA per creare e inviare applicazioni Spark in Scala</span><span class="sxs-lookup"><span data-stu-id="2730b-321">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="2730b-322">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely (Usare il plug-in Strumenti HDInsight per IntelliJ IDEA per eseguire il debug di applicazioni Spark in remoto)</span><span class="sxs-lookup"><span data-stu-id="2730b-322">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="2730b-323">Usare i notebook di Zeppelin con un cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="2730b-323">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="2730b-324">Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight</span><span class="sxs-lookup"><span data-stu-id="2730b-324">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="2730b-325">Usare pacchetti esterni con i notebook Jupyter</span><span class="sxs-lookup"><span data-stu-id="2730b-325">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="2730b-326">Installare Jupyter Notebook nel computer e connetterlo a un cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="2730b-326">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="2730b-327">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="2730b-327">Manage resources</span></span>
* [<span data-ttu-id="2730b-328">Gestire le risorse del cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="2730b-328">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="2730b-329">Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="2730b-329">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]: ../storage-create-storage-account/
