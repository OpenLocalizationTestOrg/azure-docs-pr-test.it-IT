---
title: aaaUse Apache Spark streaming con hub eventi in Azure HDInsight | Documenti Microsoft
description: "Compila un esempio di flusso Apache Spark in modalità toosend dati tooAzure Hub eventi del flusso e quindi ricevere gli eventi in cluster di HDInsight Spark con un'applicazione di scala."
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
ms.openlocfilehash: 10cc5884047b3b8249fe8a8822a16a19780a4af3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-process-data-from-azure-event-hubs-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="ebee6-104">Streaming Apache Spark: elaborare i dati dall'Hub eventi di Azure con il cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="ebee6-104">Apache Spark streaming: Process data from Azure Event Hubs with Spark cluster on HDInsight</span></span>

<span data-ttu-id="ebee6-105">In questo articolo, si crea un Apache Spark lo streaming di esempio che coinvolge hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ebee6-105">In this article, you create an Apache Spark streaming sample that involves hello following steps:</span></span>

1. <span data-ttu-id="ebee6-106">Utilizzare un messaggio di tooingest applicazione autonoma in un Hub di eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="ebee6-106">You use a standalone application tooingest messages into an Azure Event Hub.</span></span>

2. <span data-ttu-id="ebee6-107">I due diversi approcci, recuperare messaggi hello da Hub di eventi in tempo reale tramite un'applicazione in esecuzione nel cluster Spark in HDInsight di Azure.</span><span class="sxs-lookup"><span data-stu-id="ebee6-107">With two different approaches, you retrieve hello messages from Event Hub in real-time using an application running in Spark cluster on Azure HDInsight.</span></span>

3. <span data-ttu-id="ebee6-108">È compilare pipeline di analisi flusso sistemi di archiviazione toopersist dati toodifferent o ottenere informazioni dettagliate dai dati in tempo reale di hello.</span><span class="sxs-lookup"><span data-stu-id="ebee6-108">You build streaming analytic pipelines toopersist data toodifferent storage systems, or get insights from data on hello fly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ebee6-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ebee6-109">Prerequisites</span></span>

* <span data-ttu-id="ebee6-110">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ebee6-110">An Azure subscription.</span></span> <span data-ttu-id="ebee6-111">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="ebee6-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="ebee6-112">Un cluster Apache Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ebee6-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="ebee6-113">Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="ebee6-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="spark-streaming-concepts"></a><span data-ttu-id="ebee6-114">Concetti relativi allo streaming Spark</span><span class="sxs-lookup"><span data-stu-id="ebee6-114">Spark Streaming concepts</span></span>

<span data-ttu-id="ebee6-115">Per una spiegazione dettagliata dello streaming Spark, vedere [Apache Spark streaming overview](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview) (Panoramica dello streaming in Apache Spark).</span><span class="sxs-lookup"><span data-stu-id="ebee6-115">For a detailed explanation of Spark streaming, see [Apache Spark streaming overview](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span></span> <span data-ttu-id="ebee6-116">HDInsight offre hello del cluster stesso flusso funzionalità tooa Spark in Azure.</span><span class="sxs-lookup"><span data-stu-id="ebee6-116">HDInsight brings hello same streaming features tooa Spark cluster on Azure.</span></span>  

## <a name="what-does-this-solution-do"></a><span data-ttu-id="ebee6-117">Scopo di questa soluzione</span><span class="sxs-lookup"><span data-stu-id="ebee6-117">What does this solution do?</span></span>

<span data-ttu-id="ebee6-118">In questo articolo, toocreate un esempio di flusso Spark, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ebee6-118">In this article, toocreate a Spark streaming example, perform hello following steps:</span></span>

1. <span data-ttu-id="ebee6-119">Creare un Hub eventi di Azure che riceve un flusso di eventi.</span><span class="sxs-lookup"><span data-stu-id="ebee6-119">Create an Azure Event Hub that will receive a stream of events.</span></span>

2. <span data-ttu-id="ebee6-120">Eseguire un'applicazione autonoma locale che genera eventi e lo inserisce toohello Hub di eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="ebee6-120">Run a local standalone application that generates events and pushes it toohello Azure Event Hub.</span></span> <span data-ttu-id="ebee6-121">applicazione di esempio Hello che questa sia pubblicata nel [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span><span class="sxs-lookup"><span data-stu-id="ebee6-121">hello sample application that does this is published at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span>

3. <span data-ttu-id="ebee6-122">Eseguire un'applicazione di streaming in modalità remota in un cluster Spark che legge eventi di streaming provenienti dall'Hub di eventi di Azure ed eseguire varie analisi/elaborazioni di dati.</span><span class="sxs-lookup"><span data-stu-id="ebee6-122">Run a streaming application remotely on a Spark cluster that reads streaming events from Azure Event Hub and perform various data processing/analysis.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="ebee6-123">Creare un Hub di eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="ebee6-123">Create an Azure Event Hub</span></span>

1. <span data-ttu-id="ebee6-124">Accesso toohello [portale Azure](https://ms.portal.azure.com), fare clic su **New** in hello in alto a sinistra della schermata di hello.</span><span class="sxs-lookup"><span data-stu-id="ebee6-124">Log on toohello [Azure Portal](https://ms.portal.azure.com), and click **New** at hello top left of hello screen.</span></span>

2. <span data-ttu-id="ebee6-125">Fare clic su **Internet delle cose** e quindi su **Hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="ebee6-125">Click **Internet of Things**, then click **Event Hubs**.</span></span>

    <span data-ttu-id="ebee6-126">![Creare un hub eventi per l'esempio di streaming Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Creare un hub eventi per l'esempio di streaming Spark")</span><span class="sxs-lookup"><span data-stu-id="ebee6-126">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Create event hub for Spark streaming example")</span></span>

3. <span data-ttu-id="ebee6-127">In hello **Crea spazio dei nomi** pannello, immettere un nome di spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="ebee6-127">In hello **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="ebee6-128">Scegliere hello tariffario (Standard o Basic).</span><span class="sxs-lookup"><span data-stu-id="ebee6-128">choose hello pricing tier (Basic or Standard).</span></span> <span data-ttu-id="ebee6-129">Inoltre, è possibile scegliere una sottoscrizione di Azure, un gruppo di risorse e una posizione nella quale risorsa hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="ebee6-129">Also, choose an Azure subscription, resource group, and location in which toocreate hello resource.</span></span> <span data-ttu-id="ebee6-130">Fare clic su **crea** dello spazio dei nomi di toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="ebee6-130">Click **Create** toocreate hello namespace.</span></span>

      <span data-ttu-id="ebee6-131">![Fornire un nome di hub eventi per l'esempio di streaming Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Fornire un nome di hub eventi per l'esempio di streaming Spark")</span><span class="sxs-lookup"><span data-stu-id="ebee6-131">![Provide an event hub name for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Provide an event hub name for Spark streaming example")</span></span>

    > [!NOTE]
    > <span data-ttu-id="ebee6-132">È consigliabile selezionare hello stesso **percorso** del cluster Apache Spark in HDInsight tooreduce latenza e i costi.</span><span class="sxs-lookup"><span data-stu-id="ebee6-132">You should select hello same **Location** as your Apache Spark cluster in HDInsight tooreduce latency and costs.</span></span>
    >
    >

4. <span data-ttu-id="ebee6-133">Nell'elenco dello spazio dei nomi di hello hub eventi, fare clic su hello nuovo spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="ebee6-133">In hello Event Hubs namespace list, click hello newly-created namespace.</span></span>      


5. <span data-ttu-id="ebee6-134">Nel Pannello di hello dello spazio dei nomi, fare clic su **hub eventi**, quindi fare clic su **+ Hub eventi** toocreate un nuovo Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="ebee6-134">In hello namespace blade, click **Event Hubs**, and then click **+ Event Hub** toocreate a new Event Hub.</span></span>
   
    <span data-ttu-id="ebee6-135">![Creare un hub eventi per l'esempio di streaming Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Creare un hub eventi per l'esempio di streaming Spark")</span><span class="sxs-lookup"><span data-stu-id="ebee6-135">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Create event hub for Spark streaming example")</span></span>

6. <span data-ttu-id="ebee6-136">Digitare un nome per l'Hub eventi, set hello partizione conteggio too10 e too1 di memorizzazione di messaggi.</span><span class="sxs-lookup"><span data-stu-id="ebee6-136">Type a name for your Event Hub, set hello partition count too10, and message retention too1.</span></span> <span data-ttu-id="ebee6-137">Ci stiamo archiviazione messaggi hello in questa soluzione non in modo da lasciare rest hello come impostazione predefinita e quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="ebee6-137">We are not archiving hello messages in this solution so you can leave hello rest as default, and then click **Create**.</span></span>
   
    <span data-ttu-id="ebee6-138">![Fornire i dettagli dell'hub eventi per l'esempio di streaming Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Fornire i dettagli dell'hub eventi per l'esempio di streaming Spark")</span><span class="sxs-lookup"><span data-stu-id="ebee6-138">![Provide event hub details for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Provide event hub details for Spark streaming example")</span></span>

7. <span data-ttu-id="ebee6-139">Hello appena creati Hub eventi è elencato nel Pannello di hello Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="ebee6-139">hello newly created Event Hub is listed in hello Event Hub blade.</span></span>
    
     <span data-ttu-id="ebee6-140">![Visualizzare l'Hub eventi, ad esempio di flusso Spark hello](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "Hub di eventi di visualizzazione per hello nascita streaming di esempio")</span><span class="sxs-lookup"><span data-stu-id="ebee6-140">![View Event Hub for hello Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "View Event Hub for hello Spark streaming example")</span></span>

8. <span data-ttu-id="ebee6-141">Nel pannello dello spazio dei nomi hello (non hello specifico Hub eventi blade), fare clic su **criteri di accesso condiviso**, quindi fare clic su **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="ebee6-141">Back in hello namespace blade (not hello specific Event Hub blade), click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
     <span data-ttu-id="ebee6-142">![Impostare i criteri di Hub eventi, ad esempio di flusso Spark hello](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "criteri impostare Hub di eventi per hello nascita streaming di esempio")</span><span class="sxs-lookup"><span data-stu-id="ebee6-142">![Set Event Hub policies for hello Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "Set Event Hub policies for hello Spark streaming example")</span></span>

9. <span data-ttu-id="ebee6-143">Fare clic su hello toocopy pulsante Copia di hello **RootManageSharedAccessKey** primario chiave e connessione stringa toohello negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="ebee6-143">Click hello copy button toocopy hello **RootManageSharedAccessKey** primary key and connection string toohello clipboard.</span></span> <span data-ttu-id="ebee6-144">Salvare queste toouse più avanti nell'esercitazione di hello.</span><span class="sxs-lookup"><span data-stu-id="ebee6-144">Save these toouse later in hello tutorial.</span></span>
    
     <span data-ttu-id="ebee6-145">![Visualizzare le chiavi di criterio Hub eventi, ad esempio di flusso Spark hello](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "chiavi dei criteri di Hub di eventi di visualizzazione per hello nascita streaming di esempio")</span><span class="sxs-lookup"><span data-stu-id="ebee6-145">![View Event Hub policy keys for hello Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "View Event Hub policy keys for hello Spark streaming example")</span></span>

## <a name="send-messages-tooazure-event-hub-using-a-sample-scala-application"></a><span data-ttu-id="ebee6-146">Inviare i messaggi tooAzure Hub di eventi tramite un'applicazione di esempio Scala</span><span class="sxs-lookup"><span data-stu-id="ebee6-146">Send messages tooAzure Event Hub using a sample Scala application</span></span>

<span data-ttu-id="ebee6-147">In questa sezione si utilizza un'applicazione locale autonomo di una Scala che genera un flusso di eventi e lo invia tooAzure Hub eventi creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ebee6-147">In this section you use a standalone local Scala application that generates a stream of events and sends it tooAzure Event Hub that you created earlier.</span></span> <span data-ttu-id="ebee6-148">Questa applicazione è disponibile in GitHub all'indirizzo [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span><span class="sxs-lookup"><span data-stu-id="ebee6-148">This application is available on GitHub at [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span></span> <span data-ttu-id="ebee6-149">Ecco i passaggi di Hello presuppongono che si è già duplicata questo repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="ebee6-149">hello steps here assume that you have already forked this GitHub repository.</span></span>

1. <span data-ttu-id="ebee6-150">Verificare che sia installato nel computer di hello in cui si esegue l'applicazione segue hello.</span><span class="sxs-lookup"><span data-stu-id="ebee6-150">Make sure you have hello following installed on hello computer where you run this application.</span></span>

    * <span data-ttu-id="ebee6-151">Oracle Java Development Kit.</span><span class="sxs-lookup"><span data-stu-id="ebee6-151">Oracle Java Development kit.</span></span> <span data-ttu-id="ebee6-152">Per installarlo, fare clic [qui](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="ebee6-152">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
    * <span data-ttu-id="ebee6-153">Apache Maven.</span><span class="sxs-lookup"><span data-stu-id="ebee6-153">Apache Maven.</span></span> <span data-ttu-id="ebee6-154">È possibile scaricarlo [qui](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="ebee6-154">You can download it from [here](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="ebee6-155">Sono disponibili istruzioni tooinstall Maven [qui](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="ebee6-155">Instructions tooinstall Maven are available [here](https://maven.apache.org/install.html).</span></span>

2. <span data-ttu-id="ebee6-156">Aprire un prompt dei comandi e passare toohello percorso è stato clonato il repository GitHub hello per un'applicazione hello esempio Scala ed eseguire hello dopo l'applicazione hello toobuild di comando.</span><span class="sxs-lookup"><span data-stu-id="ebee6-156">Open a command prompt and navigate toohello location you cloned hello GitHub repo for hello sample Scala application and run hello following command toobuild hello application.</span></span>

        mvn package

3. <span data-ttu-id="ebee6-157">file jar di output di Hello per un'applicazione hello, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, viene creato in **/destinazione** directory.</span><span class="sxs-lookup"><span data-stu-id="ebee6-157">hello output jar for hello application, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, is created under **/target** directory.</span></span> <span data-ttu-id="ebee6-158">Utilizzare il file JAR più avanti in questa soluzione completa di articolo tootest hello.</span><span class="sxs-lookup"><span data-stu-id="ebee6-158">You use this JAR later in this article tootest hello complete solution.</span></span>

## <a name="create-application-tooreceive-messages-from-event-hub-into-a-spark-cluster"></a><span data-ttu-id="ebee6-159">Creare i messaggi dell'applicazione tooreceive da Hub di eventi in un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="ebee6-159">Create application tooreceive messages from Event Hub into a Spark cluster</span></span> 

<span data-ttu-id="ebee6-160">Sono disponibili due approcci tooconnect, Streaming Spark e hub di eventi di Azure, le connessioni basate su ricevitore e Direct DStream-connessione basata su.</span><span class="sxs-lookup"><span data-stu-id="ebee6-160">We have two approaches tooconnect Spark Streaming and Azure Event Hubs, Receiver-based connection and Direct-DStream-based connection.</span></span> <span data-ttu-id="ebee6-161">Basato su DStream diretta è stato introdotto in gennaio 2017 nella versione di hello 2.0.3.</span><span class="sxs-lookup"><span data-stu-id="ebee6-161">Direct-DStream-based is introduced on Jan of 2017, in hello 2.0.3 release.</span></span> <span data-ttu-id="ebee6-162">Si suppone che la connessione tooreplace hello originale basata su destinatario perché è più efficiente ed efficace a risorsa.</span><span class="sxs-lookup"><span data-stu-id="ebee6-162">It is supposed tooreplace hello original receiver-based connection as it is more performant and resource-efficient.</span></span> <span data-ttu-id="ebee6-163">Altre informazioni sono disponibili su [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span><span class="sxs-lookup"><span data-stu-id="ebee6-163">More details found in [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span></span> <span data-ttu-id="ebee6-164">DStream diretto supporta solo Spark 2.0 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="ebee6-164">Direct DStream only supports Spark 2.0+.</span></span>

### <a name="build-applications-with-hello-dependency-toospark-eventhubs-connector"></a><span data-ttu-id="ebee6-165">Compilazione di applicazioni con connettore di hello dipendenza toospark eventhubs</span><span class="sxs-lookup"><span data-stu-id="ebee6-165">Build applications with hello dependency toospark-eventhubs connector</span></span>

<span data-ttu-id="ebee6-166">Verranno inoltre pubblicate hello versione di Spark-EventHubs in GitHub di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="ebee6-166">We will also publish hello staging version of Spark-EventHubs in GitHub.</span></span> <span data-ttu-id="ebee6-167">versione sosta hello di toouse di Spark EventHubs, hello primo passaggio consiste tooindicate GitHub come hello repository di origine mediante l'aggiunta di hello toopom.xml voce seguente:</span><span class="sxs-lookup"><span data-stu-id="ebee6-167">toouse hello staging version of Spark-EventHubs, hello first step is tooindicate GitHub as hello source repo by adding hello following entry toopom.xml:</span></span>

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

<span data-ttu-id="ebee6-168">È quindi possibile aggiungere hello seguente versione non definitiva di dipendenza tooyour progetto tootake hello.</span><span class="sxs-lookup"><span data-stu-id="ebee6-168">You can then add hello following dependency tooyour project tootake hello pre-released version.</span></span>

<span data-ttu-id="ebee6-169">Dipendenza Maven</span><span class="sxs-lookup"><span data-stu-id="ebee6-169">Maven Dependency</span></span>

```xml
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11 -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>spark-streaming-eventhubs_2.11</artifactId>
    <version>2.0.4</version>
</dependency>
```

<span data-ttu-id="ebee6-170">Dipendenza SBT</span><span class="sxs-lookup"><span data-stu-id="ebee6-170">SBT Dependency</span></span>

```
// https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11
libraryDependencies += "com.microsoft.azure" % "spark-streaming-eventhubs_2.11" % "2.0.4"
```

### <a name="direct-dstream-connection"></a><span data-ttu-id="ebee6-171">Connessione DStream diretto</span><span class="sxs-lookup"><span data-stu-id="ebee6-171">Direct DStream Connection</span></span>

<span data-ttu-id="ebee6-172">È possibile scaricare da [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar) un file con estensione jar preesistente contenente esempi di uso di DStream diretto.</span><span class="sxs-lookup"><span data-stu-id="ebee6-172">A pre-built jar file containing examples using Direct DStream can be downloaded in [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).</span></span>

<span data-ttu-id="ebee6-173">file jar Hello contiene tre esempi sono disponibili in cui il codice sorgente [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span><span class="sxs-lookup"><span data-stu-id="ebee6-173">hello jar file contains three examples whose source code are available at [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span></span>

<span data-ttu-id="ebee6-174">Prendere come esempio [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala):</span><span class="sxs-lookup"><span data-stu-id="ebee6-174">Taking [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) as an example:</span></span>

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

<span data-ttu-id="ebee6-175">In hello sopra riportato, `eventhubParameters` sono hello parametri specifici tooa singola EventHubs istanza e si dispone di toopass è toohello `createDirectStreams` API che costruisce mapping oggetto uno diretto DStream tooa spazio dei nomi degli hub di eventi.</span><span class="sxs-lookup"><span data-stu-id="ebee6-175">In hello above example, `eventhubParameters` are hello parameters specific tooa single EventHubs instance and you have toopass it toohello `createDirectStreams` API which constructs a Direct DStream object mapping tooa Event Hubs namespace.</span></span> <span data-ttu-id="ebee6-176">Oggetto di hello DStream diretto, è possibile chiamare qualsiasi API DStream fornita dal framework Spark Streaming API.</span><span class="sxs-lookup"><span data-stu-id="ebee6-176">Over hello Direct DStream object, you can call any DStream API provided by Spark Streaming API framework.</span></span> <span data-ttu-id="ebee6-177">In questo esempio, si calcola frequenza hello di ogni parola all'interno di intervalli di hello ultimo batch micro 3.</span><span class="sxs-lookup"><span data-stu-id="ebee6-177">In this example, we calculate hello frequency of each word within hello last 3 micro batch intervals.</span></span>

### <a name="receiver-based-connection"></a><span data-ttu-id="ebee6-178">Connessioni basate su ricevitore</span><span class="sxs-lookup"><span data-stu-id="ebee6-178">Receiver-based Connection</span></span>

<span data-ttu-id="ebee6-179">Un Spark streaming scritto in Scala, che riceve gli eventi e destinazioni di route hello toodifferent, l'applicazione di esempio è disponibile all'indirizzo [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span><span class="sxs-lookup"><span data-stu-id="ebee6-179">A Spark streaming example application written in Scala, which receives events and route hello toodifferent destinations, is available at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span> <span data-ttu-id="ebee6-180">Seguire i passaggi hello sotto l'applicazione hello tooupdate per la configurazione di Hub eventi e creare file jar di output di hello.</span><span class="sxs-lookup"><span data-stu-id="ebee6-180">Follow hello steps below tooupdate hello application for your Event Hub configuration and create hello output jar.</span></span>

1. <span data-ttu-id="ebee6-181">Avviare IntelliJ IDEA e avviare schermata selezionare da hello **estrarre dal controllo della versione** e quindi fare clic su **Git**.</span><span class="sxs-lookup"><span data-stu-id="ebee6-181">Launch IntelliJ IDEA and from hello launch screen select **Check out from Version Control** and then click **Git**.</span></span>
   
    <span data-ttu-id="ebee6-182">![Esempio di streaming Apache Spark - Ottenere origini da Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Esempio di streaming Apache Spark - Ottenere origini da Git")</span><span class="sxs-lookup"><span data-stu-id="ebee6-182">![Apache Spark streaming example - get sources from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark streaming example - get sources from Git")</span></span>

2. <span data-ttu-id="ebee6-183">In hello **Clone Repository** nella finestra di dialogo forniscono hello URL toohello Git repository tooclone da specificare hello directory tooclone per e quindi fare clic su **Clone**.</span><span class="sxs-lookup"><span data-stu-id="ebee6-183">In hello **Clone Repository** dialog box, provide hello URL toohello Git repository tooclone from, specify hello directory tooclone to, and then click **Clone**.</span></span>
   
    <span data-ttu-id="ebee6-184">![Esempio di streaming Apache Spark - Clonare da Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Esempio di streaming Apache Spark - Clonare da Git")</span><span class="sxs-lookup"><span data-stu-id="ebee6-184">![Apache Spark streaming example - clone from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark streaming example - clone from Git")</span></span>
3. <span data-ttu-id="ebee6-185">Seguire i prompt di hello fino a quando progetto hello viene completamente duplicato.</span><span class="sxs-lookup"><span data-stu-id="ebee6-185">Follow hello prompts till hello project is completely cloned.</span></span> <span data-ttu-id="ebee6-186">Premere **Alt + 1** tooopen hello **visualizzazione progetto**.</span><span class="sxs-lookup"><span data-stu-id="ebee6-186">Press **Alt + 1** tooopen hello **Project View**.</span></span> <span data-ttu-id="ebee6-187">Dovrebbe essere simile a seguito di hello.</span><span class="sxs-lookup"><span data-stu-id="ebee6-187">It should resemble hello following.</span></span>
   
    <span data-ttu-id="ebee6-188">![Esempio di streaming Apache Spark - Project View](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Esempio di streaming Apache Spark - Project View")</span><span class="sxs-lookup"><span data-stu-id="ebee6-188">![Apache Spark streaming example - Project View](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark streaming example - Project View")</span></span>
4. <span data-ttu-id="ebee6-189">Verificare che il codice dell'applicazione hello viene compilato con Java8.</span><span class="sxs-lookup"><span data-stu-id="ebee6-189">Make sure hello application code is compiled with Java8.</span></span> <span data-ttu-id="ebee6-190">tooensure, fare clic su **File**, fare clic su **struttura del progetto**e in hello **progetto** scheda, assicurarsi che il livello di linguaggio di progetto è stato impostato troppo**8 - espressioni lambda, tipo le annotazioni e così via.**.</span><span class="sxs-lookup"><span data-stu-id="ebee6-190">tooensure this, click **File**, click **Project Structure**, and on hello **Project** tab, make sure Project language level is set too**8 - Lambdas, type annotations, etc.**.</span></span>
   
    <span data-ttu-id="ebee6-191">![Esempio di streaming Apache Spark - Impostare il compilatore](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Esempio di streaming Apache Spark - Impostare il compilatore")</span><span class="sxs-lookup"><span data-stu-id="ebee6-191">![Apache Spark streaming example - Set compiler](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark streaming example - Set compiler")</span></span>
5. <span data-ttu-id="ebee6-192">Aprire hello **pom.xml** e accertarsi che sia corretta versione di hello Spark.</span><span class="sxs-lookup"><span data-stu-id="ebee6-192">Open hello **pom.xml** and make sure hello Spark version is correct.</span></span> <span data-ttu-id="ebee6-193">In `<properties>` nodo, cercare hello seguente frammento di codice e verificare la versione di hello Spark.</span><span class="sxs-lookup"><span data-stu-id="ebee6-193">Under `<properties>` node, look for hello following snippet and verify hello Spark version.</span></span>

        <scala.version>2.11.8</scala.version>
        <scala.compat.version>2.11.8</scala.compat.version>
        <scala.binary.version>2.11</scala.binary.version>
        <spark.version>2.0.0</spark.version>

6. <span data-ttu-id="ebee6-194">un'applicazione Hello richiede un file jar dipendenza chiamato **jar driver JDBC**.</span><span class="sxs-lookup"><span data-stu-id="ebee6-194">hello application requires a dependency jar called **JDBC driver jar**.</span></span> <span data-ttu-id="ebee6-195">Si tratta di messaggi hello toowrite obbligatorio ricevuti da Hub di eventi in un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="ebee6-195">This is required toowrite hello messages received from Event Hub into an Azure SQL database.</span></span> <span data-ttu-id="ebee6-196">È possibile scaricare la versione 4.1 o successiva di questo file con estensione jar [qui](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span><span class="sxs-lookup"><span data-stu-id="ebee6-196">You can download this jar (v4.1 or later) from [here](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span></span> <span data-ttu-id="ebee6-197">Aggiungi riferimento toothis jar nella libreria di progetto hello.</span><span class="sxs-lookup"><span data-stu-id="ebee6-197">Add reference toothis jar in hello project library.</span></span> <span data-ttu-id="ebee6-198">Eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ebee6-198">Perform hello following steps:</span></span>
     
     1. <span data-ttu-id="ebee6-199">Nella finestra in cui è aperta un'applicazione hello IDEA IntelliJ **File**, fare clic su **struttura del progetto**e quindi fare clic su **librerie**.</span><span class="sxs-lookup"><span data-stu-id="ebee6-199">From IntelliJ IDEA window where you have hello application open, click **File**, click **Project Structure**, and then click **Libraries**.</span></span> 
     2. <span data-ttu-id="ebee6-200">Fare clic su hello icona Aggiungi (![icona Aggiungi](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), fare clic su **Java**, quindi passare toohello percorso in cui sono stati scaricati file jar di driver JDBC hello.</span><span class="sxs-lookup"><span data-stu-id="ebee6-200">Click hello add icon (![add icon](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), click **Java**, and then navigate toohello location where you downloaded hello JDBC driver jar.</span></span> <span data-ttu-id="ebee6-201">Seguire hello richieste tooadd hello jar file toohello libreria del progetto.</span><span class="sxs-lookup"><span data-stu-id="ebee6-201">Follow hello prompts tooadd hello jar file toohello project library.</span></span>

         <span data-ttu-id="ebee6-202">![aggiungere dipendenze mancanti](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Aggiungere file JAR di dipendenza mancanti")</span><span class="sxs-lookup"><span data-stu-id="ebee6-202">![add missing dependencies](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Add missing dependency jars")</span></span>
     3. <span data-ttu-id="ebee6-203">Fare clic su **Apply**.</span><span class="sxs-lookup"><span data-stu-id="ebee6-203">Click **Apply**.</span></span>

7. <span data-ttu-id="ebee6-204">Creare il file jar di hello output.</span><span class="sxs-lookup"><span data-stu-id="ebee6-204">Create hello output jar file.</span></span> <span data-ttu-id="ebee6-205">Eseguire hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="ebee6-205">Perform hello following steps.</span></span>

   1. <span data-ttu-id="ebee6-206">In hello **struttura del progetto** la finestra di dialogo, fare clic su **elementi** e quindi fare clic su hello e simboli.</span><span class="sxs-lookup"><span data-stu-id="ebee6-206">In hello **Project Structure** dialog box, click **Artifacts** and then click hello plus symbol.</span></span> <span data-ttu-id="ebee6-207">Nella finestra di dialogo popup hello, fare clic su **JAR**, quindi fare clic su **dai moduli con dipendenze**.</span><span class="sxs-lookup"><span data-stu-id="ebee6-207">From hello pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>      
       
       <span data-ttu-id="ebee6-208">![Esempio di streaming Apache Spark - Creazione di un file con estensione jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Esempio di streaming Apache Spark - Creazione di un file con estensione jar")</span><span class="sxs-lookup"><span data-stu-id="ebee6-208">![Apache Spark streaming example - create JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Apache Spark streaming example - create JAR")</span></span>
   2. <span data-ttu-id="ebee6-209">In hello **creare JAR dai moduli** finestra di dialogo, fare clic sui puntini di sospensione hello (![i puntini di sospensione](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) contro hello **classe Main**.</span><span class="sxs-lookup"><span data-stu-id="ebee6-209">In hello **Create JAR from Modules** dialog box, click hello ellipsis (![ellipsis](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) against hello **Main Class**.</span></span>
   3. <span data-ttu-id="ebee6-210">In hello **Seleziona classe Main** finestra di dialogo selezionare una qualsiasi delle classi disponibili hello e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="ebee6-210">In hello **Select Main Class** dialog box, select any of hello available classes and then click **OK**.</span></span>
      
       <span data-ttu-id="ebee6-211">![Esempio di streaming Apache Spark - Selezionare la classe per un file con estensione jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Esempio di streaming Apache Spark - Selezionare la classe per un file con estensione jar")</span><span class="sxs-lookup"><span data-stu-id="ebee6-211">![Apache Spark streaming example - select class for jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark streaming example - select class for jar")</span></span>
   4. <span data-ttu-id="ebee6-212">In hello **creare JAR dai moduli** finestra di dialogo, accertarsi che l'opzione hello troppo**estrarre toohello destinazione JAR** sia selezionata e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="ebee6-212">In hello **Create JAR from Modules** dialog box, make sure that hello option too**extract toohello target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="ebee6-213">Verrà creato un singolo file con estensione jar con tutte le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="ebee6-213">This creates a single JAR with all dependencies.</span></span>
      
       <span data-ttu-id="ebee6-214">![Esempio di streaming Apache Spark - Creare un file con estensione jar dai moduli](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Esempio di streaming Apache Spark - Creare un file con estensione jar dai modul")</span><span class="sxs-lookup"><span data-stu-id="ebee6-214">![Apache Spark streaming example - create jar from modules](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Apache Spark streaming example - create jar from modules")</span></span>
   5. <span data-ttu-id="ebee6-215">Hello **Output Layout** scheda vengono elencati tutti JAR hello che sono inclusi come parte del progetto di Maven hello.</span><span class="sxs-lookup"><span data-stu-id="ebee6-215">hello **Output Layout** tab lists all hello jars that are included as part of hello Maven project.</span></span> <span data-ttu-id="ebee6-216">È possibile selezionare e quelli in cui hello Scala applicazione hello di eliminazione non ha alcuna dipendenza diretta.</span><span class="sxs-lookup"><span data-stu-id="ebee6-216">You can select and delete hello ones on which hello Scala application has no direct dependency.</span></span> <span data-ttu-id="ebee6-217">Per un'applicazione hello viene creata in questo caso, è possibile rimuovere tutto tranne hello ultimo (**spark-streaming--persistenza-esempi di dati compilare output**).</span><span class="sxs-lookup"><span data-stu-id="ebee6-217">For hello application we are creating here, you can remove all but hello last one (**spark-streaming-data-persistence-examples compile output**).</span></span> <span data-ttu-id="ebee6-218">Selezionare toodelete JAR hello e quindi fare clic su hello **eliminare** icona (![icona Elimina](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span><span class="sxs-lookup"><span data-stu-id="ebee6-218">Select hello jars toodelete and then click hello **Delete** icon (![delete icon](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span></span>
      
       <span data-ttu-id="ebee6-219">![Esempio di streaming Apache Spark - Eliminare i file con estensione jar estratti](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Esempio di streaming Apache Spark - Eliminare i file con estensione jar estratti")</span><span class="sxs-lookup"><span data-stu-id="ebee6-219">![Apache Spark streaming example - delete extracted jars](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark streaming example - delete extracted jars")</span></span>
      
       <span data-ttu-id="ebee6-220">Assicurarsi che **compilare su verificare** casella è selezionata, che assicura che jar hello viene creato ogni volta che il progetto hello viene compilato o aggiornato.</span><span class="sxs-lookup"><span data-stu-id="ebee6-220">Make sure **Build on make** box is selected, which ensures that hello jar is created every time hello project is built or updated.</span></span> <span data-ttu-id="ebee6-221">Fare clic su **Apply**.</span><span class="sxs-lookup"><span data-stu-id="ebee6-221">Click **Apply**.</span></span>
   6. <span data-ttu-id="ebee6-222">In hello **Output Layout** scheda nella parte inferiore di hello di hello **elementi disponibili** casella, si dispone di jar SQL JDBC hello di libreria del progetto precedente toohello aggiunto.</span><span class="sxs-lookup"><span data-stu-id="ebee6-222">In hello **Output Layout** tab, right at hello bottom of hello **Available Elements** box, you have hello SQL JDBC jar that you added earlier toohello project library.</span></span> <span data-ttu-id="ebee6-223">È necessario aggiungere questo toohello **Output Layout** scheda. Fare clic sul file jar hello e quindi fare clic su **estrarre nell'Output radice**.</span><span class="sxs-lookup"><span data-stu-id="ebee6-223">You must add this toohello **Output Layout** tab. Right-click hello jar file, and then click **Extract Into Output Root**.</span></span>
      
       <span data-ttu-id="ebee6-224">![Esempio di streaming Apache Spark - Estrarre file con estensione jar di dipendenza](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Esempio di streaming Apache Spark - Estrarre file con estensione jar di dipendenza")</span><span class="sxs-lookup"><span data-stu-id="ebee6-224">![Apache Spark streaming example - extract dependency jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark streaming example - extract dependency jar")</span></span>  
      
       <span data-ttu-id="ebee6-225">Hello **Output Layout** scheda dovrebbe essere simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="ebee6-225">hello **Output Layout** tab should now look like this.</span></span>
      
       <span data-ttu-id="ebee6-226">![Esempio di streaming Apache Spark - Scheda output finale](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Esempio di streaming Apache Spark - Scheda output finale")</span><span class="sxs-lookup"><span data-stu-id="ebee6-226">![Apache Spark streaming example - final output tab](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark streaming example - final output tab")</span></span>        
      
       <span data-ttu-id="ebee6-227">In hello **struttura del progetto** la finestra di dialogo, fare clic su **applica** e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="ebee6-227">In hello **Project Structure** dialog box, click **Apply** and then click **OK**.</span></span>    
   7. <span data-ttu-id="ebee6-228">Dalla barra dei menu hello, fare clic su **compilare**, quindi fare clic su **Crea progetto**.</span><span class="sxs-lookup"><span data-stu-id="ebee6-228">From hello menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="ebee6-229">È anche possibile fare clic su **artefatti di compilazione** jar hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="ebee6-229">You can also click **Build Artifacts** toocreate hello jar.</span></span> <span data-ttu-id="ebee6-230">Hello jar output viene creato in **\classes\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="ebee6-230">hello output jar is created under **\classes\artifacts**.</span></span>
      
       <span data-ttu-id="ebee6-231">![Esempio di streaming Apache Spark - Output dei file con estensione jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Esempio di streaming Apache Spark - Output dei file con estensione jar")</span><span class="sxs-lookup"><span data-stu-id="ebee6-231">![Apache Spark streaming example - output JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Apache Spark streaming example - output JAR")</span></span>

## <a name="run-hello-application-remotely-on-a-spark-cluster-using-livy"></a><span data-ttu-id="ebee6-232">Eseguire un'applicazione hello in modalità remota in un cluster Spark usando inserire il</span><span class="sxs-lookup"><span data-stu-id="ebee6-232">Run hello application remotely on a Spark cluster using Livy</span></span>

<span data-ttu-id="ebee6-233">In questo articolo è utilizzare applicazione flusso di inserire il toorun hello Apache Spark in modalità remota in un cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="ebee6-233">In this article you use Livy toorun hello Apache Spark streaming application remotely on a Spark cluster.</span></span> <span data-ttu-id="ebee6-234">Per informazioni dettagliate su come inserire il con HDInsight Spark toouse cluster, vedere [invia i processi in modalità remota tooan Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="ebee6-234">For detailed discussion on how toouse Livy with HDInsight Spark cluster, see [Submit jobs remotely tooan Apache Spark cluster on Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span> <span data-ttu-id="ebee6-235">Prima di iniziare l'esecuzione di un'applicazione hello Spark streaming, sono disponibili un paio di operazioni che è necessario eseguire:</span><span class="sxs-lookup"><span data-stu-id="ebee6-235">Before you can start running hello Spark streaming application, there are a couple of things you should do:</span></span>

1. <span data-ttu-id="ebee6-236">Avviare gli eventi di toogenerate hello autonomo locale dell'applicazione e inviati tooEvent Hub.</span><span class="sxs-lookup"><span data-stu-id="ebee6-236">Start hello local standalone application toogenerate events and sent tooEvent Hub.</span></span> <span data-ttu-id="ebee6-237">Utilizzare hello successivo comando toodo pertanto:</span><span class="sxs-lookup"><span data-stu-id="ebee6-237">Use hello following command toodo so:</span></span>

        java -cp com-microsoft-azure-eventhubs-client-example-0.2.0.jar com.microsoft.eventhubs.client.example.EventhubsClientDriver --eventhubs-namespace "mysbnamespace" --eventhubs-name "myeventhub" --policy-name "mysendpolicy" --policy-key "<policy key>" --message-length 32 --thread-count 32 --message-count -1

2. <span data-ttu-id="ebee6-238">Hello copia streaming jar (**spark-streaming-data-persistenza-examples.jar**) toohello associato hello cluster nell'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="ebee6-238">Copy hello streaming jar (**spark-streaming-data-persistence-examples.jar**) toohello Azure Blob storage associated with hello cluster.</span></span> <span data-ttu-id="ebee6-239">In questo modo hello jar accessibile tooLivy.</span><span class="sxs-lookup"><span data-stu-id="ebee6-239">This makes hello jar accessible tooLivy.</span></span> <span data-ttu-id="ebee6-240">È possibile utilizzare [ **AzCopy**](../storage/common/storage-use-azcopy.md), della riga di comando utilità, toodo così.</span><span class="sxs-lookup"><span data-stu-id="ebee6-240">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, toodo so.</span></span> <span data-ttu-id="ebee6-241">Esistono molti degli altri client è possibile utilizzare dati tooupload.</span><span class="sxs-lookup"><span data-stu-id="ebee6-241">There are a lot of other clients you can use tooupload data.</span></span> <span data-ttu-id="ebee6-242">Altre informazioni in merito sono disponibili in [Caricare dati per processi Hadoop in HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="ebee6-242">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
3. <span data-ttu-id="ebee6-243">Installare CURL computer hello in cui si eseguono tali applicazioni.</span><span class="sxs-lookup"><span data-stu-id="ebee6-243">Install CURL on hello computer where you are running these applications from.</span></span> <span data-ttu-id="ebee6-244">Utilizziamo CURL tooinvoke hello hello toorun gli endpoint di inserire il processi in modalità remota.</span><span class="sxs-lookup"><span data-stu-id="ebee6-244">We use CURL tooinvoke hello Livy endpoints toorun hello jobs remotely.</span></span>

### <a name="run-hello-spark-streaming-application-tooreceive-hello-events-into-an-azure-storage-blob-as-text"></a><span data-ttu-id="ebee6-245">Eseguire hello Spark streaming tooreceive hello gli eventi dell'applicazione in un Blob di archiviazione di Azure come testo</span><span class="sxs-lookup"><span data-stu-id="ebee6-245">Run hello Spark streaming application tooreceive hello events into an Azure Storage Blob as text</span></span>

<span data-ttu-id="ebee6-246">Aprire un prompt dei comandi, passare toohello directory in cui è installato CURL ed eseguire hello comando (nome sostituire nome utente/password e cluster) seguente:</span><span class="sxs-lookup"><span data-stu-id="ebee6-246">Open a command prompt, navigate toohello directory where you installed CURL, and run hello following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputBlob.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="ebee6-247">Hello parametri nel file hello **inputBlob.txt** sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="ebee6-247">hello parameters in hello file **inputBlob.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsEventCount", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="ebee6-248">Segnalare il problema, comprendere quali sono i parametri di hello nel file di input hello:</span><span class="sxs-lookup"><span data-stu-id="ebee6-248">Let us understand what hello parameters in hello input file are:</span></span>

* <span data-ttu-id="ebee6-249">**file** file jar nell'account di archiviazione di Azure hello associato hello cluster hello percorso toohello dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ebee6-249">**file** is hello path toohello application jar file on hello Azure storage account associated with hello cluster.</span></span>
* <span data-ttu-id="ebee6-250">**className** hello nome della classe hello in jar hello.</span><span class="sxs-lookup"><span data-stu-id="ebee6-250">**className** is hello name of hello class in hello jar.</span></span>
* <span data-ttu-id="ebee6-251">**args** hello elenco di argomenti richiesto dalla classe hello</span><span class="sxs-lookup"><span data-stu-id="ebee6-251">**args** is hello list of arguments required by hello class</span></span>
* <span data-ttu-id="ebee6-252">**numExecutors** hello numero di core usati da hello toorun Spark streaming dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ebee6-252">**numExecutors** is hello number of cores used by Spark toorun hello streaming application.</span></span> <span data-ttu-id="ebee6-253">Deve essere sempre almeno due volte i numero di hello di partizioni di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="ebee6-253">This should always be at least twice hello number of Event Hub partitions.</span></span>
* <span data-ttu-id="ebee6-254">**executorMemory**, **executorCores**, **driverMemory** vengono utilizzati parametri tooassign necessarie risorse applicazione streaming toohello.</span><span class="sxs-lookup"><span data-stu-id="ebee6-254">**executorMemory**, **executorCores**, **driverMemory** are parameters used tooassign required resources toohello streaming application.</span></span>

> [!NOTE]
> <span data-ttu-id="ebee6-255">Non è necessario cartelle di output di hello toocreate (EventCheckpoint, EventCount/EventCount10) che vengono utilizzate come parametri.</span><span class="sxs-lookup"><span data-stu-id="ebee6-255">You do not need toocreate hello output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="ebee6-256">lo streaming dell'applicazione Hello verranno creati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ebee6-256">hello streaming application creates them for you.</span></span>
>
>

<span data-ttu-id="ebee6-257">Quando si esegue il comando hello, verrà visualizzato un output simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="ebee6-257">When you run hello command, you should see an output like hello following:</span></span>

    < HTTP/1.1 201 Created
    < Content-Type: application/json; charset=UTF-8
    < Location: /18
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Tue, 01 Dec 2015 05:39:10 GMT
    < Content-Length: 37
    <
    {"id":1,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact

<span data-ttu-id="ebee6-258">Prendere nota dell'ID batch hello nell'ultima riga di hello dell'output di hello (in questo esempio è '1').</span><span class="sxs-lookup"><span data-stu-id="ebee6-258">Make a note of hello batch ID in hello last line of hello output (in this example it is '1').</span></span> <span data-ttu-id="ebee6-259">tooverify che hello applicazione viene eseguita correttamente, è possibile esaminare l'account di archiviazione di Azure associato al cluster hello e dovrebbe essere hello **EventCount/EventCount10** cartella creato.</span><span class="sxs-lookup"><span data-stu-id="ebee6-259">tooverify that hello application runs successfully, you can look at your Azure storage account associated with hello cluster and you should see hello **/EventCount/EventCount10** folder created there.</span></span> <span data-ttu-id="ebee6-260">Questa cartella deve contenere blob che acquisisce il numero di hello di eventi elaborati all'interno di hello periodo di tempo specificato per il parametro hello **batch intervallo in secondi**.</span><span class="sxs-lookup"><span data-stu-id="ebee6-260">This folder should contain blobs that captures hello number of events processed within hello time period specified for hello parameter **batch-interval-in-seconds**.</span></span>

<span data-ttu-id="ebee6-261">un'applicazione Hello Spark streaming continuerà toorun fino a quando non si terminarlo.</span><span class="sxs-lookup"><span data-stu-id="ebee6-261">hello Spark streaming application will continue toorun until you kill it.</span></span> <span data-ttu-id="ebee6-262">toodo in tal caso, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ebee6-262">toodo so, use hello following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/1"

### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-storage-blob-as-json"></a><span data-ttu-id="ebee6-263">Eseguire applicazioni hello eventi hello tooreceive in un Blob di archiviazione di Azure come JSON</span><span class="sxs-lookup"><span data-stu-id="ebee6-263">Run hello applications tooreceive hello events into an Azure Storage Blob as JSON</span></span>
<span data-ttu-id="ebee6-264">Aprire un prompt dei comandi, passare toohello directory in cui è installato CURL ed eseguire hello comando (nome sostituire nome utente/password e cluster) seguente:</span><span class="sxs-lookup"><span data-stu-id="ebee6-264">Open a command prompt, navigate toohello directory where you installed CURL, and run hello following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputJSON.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="ebee6-265">Hello parametri nel file hello **inputJSON.txt** sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="ebee6-265">hello parameters in hello file **inputJSON.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureBlobAsJSON", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-store-folder", "/EventStore10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="ebee6-266">i parametri di Hello sono simili toowhat specificato per l'output di testo hello, nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="ebee6-266">hello parameters are similar toowhat you specified for hello text output, in hello previous step.</span></span> <span data-ttu-id="ebee6-267">Nuovamente, non è necessario cartelle di output di hello toocreate (EventCheckpoint, EventCount/EventCount10) che vengono utilizzate come parametri.</span><span class="sxs-lookup"><span data-stu-id="ebee6-267">Again, you do not need toocreate hello output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="ebee6-268">lo streaming dell'applicazione Hello verranno creati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ebee6-268">hello streaming application creates them for you.</span></span>

 <span data-ttu-id="ebee6-269">Dopo l'esecuzione di comandi hello, è possibile esaminare l'account di archiviazione di Azure associato al cluster hello e dovrebbe essere hello **/EventStore10** cartella creato.</span><span class="sxs-lookup"><span data-stu-id="ebee6-269">After you run hello command, you can look at your Azure storage account associated with hello cluster and you should see hello **/EventStore10** folder created there.</span></span> <span data-ttu-id="ebee6-270">Aprire qualsiasi file con prefisso **parte -** dovrebbe essere possibile visualizzare gli eventi di hello elaborati in un formato JSON.</span><span class="sxs-lookup"><span data-stu-id="ebee6-270">Open any file prefixed with **part-** and you should see hello events processed in a JSON format.</span></span>

### <a name="run-hello-applications-tooreceive-hello-events-into-a-hive-table"></a><span data-ttu-id="ebee6-271">Eseguire applicazioni hello eventi hello tooreceive in una tabella Hive</span><span class="sxs-lookup"><span data-stu-id="ebee6-271">Run hello applications tooreceive hello events into a Hive table</span></span>
<span data-ttu-id="ebee6-272">hello toorun applicazione di streaming Spark che gli eventi di flussi in un Hive della tabella è necessario alcuni componenti aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="ebee6-272">toorun hello Spark streaming application that streams events into a Hive table you need some additional components.</span></span> <span data-ttu-id="ebee6-273">Si tratta di:</span><span class="sxs-lookup"><span data-stu-id="ebee6-273">These are:</span></span>

* <span data-ttu-id="ebee6-274">datanucleus-api-jdo-3.2.6.jar</span><span class="sxs-lookup"><span data-stu-id="ebee6-274">datanucleus-api-jdo-3.2.6.jar</span></span>
* <span data-ttu-id="ebee6-275">datanucleus-rdbms-3.2.9.jar</span><span class="sxs-lookup"><span data-stu-id="ebee6-275">datanucleus-rdbms-3.2.9.jar</span></span>
* <span data-ttu-id="ebee6-276">datanucleus-core-3.2.10.jar</span><span class="sxs-lookup"><span data-stu-id="ebee6-276">datanucleus-core-3.2.10.jar</span></span>
* <span data-ttu-id="ebee6-277">hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="ebee6-277">hive-site.xml</span></span>

<span data-ttu-id="ebee6-278">Hello **JAR** file sono disponibili nel cluster HDInsight Spark in `/usr/hdp/current/spark-client/lib`.</span><span class="sxs-lookup"><span data-stu-id="ebee6-278">hello **.jar** files are available on your HDInsight Spark cluster at `/usr/hdp/current/spark-client/lib`.</span></span> <span data-ttu-id="ebee6-279">Hello **hive-Site.XML** è disponibile all'indirizzo `/usr/hdp/current/spark-client/conf`.</span><span class="sxs-lookup"><span data-stu-id="ebee6-279">hello **hive-site.xml** is available at `/usr/hdp/current/spark-client/conf`.</span></span>

<span data-ttu-id="ebee6-280">È possibile utilizzare [WinScp](http://winscp.net/eng/download.php) toocopy i file dal computer locale di hello cluster tooyour.</span><span class="sxs-lookup"><span data-stu-id="ebee6-280">You can use [WinScp](http://winscp.net/eng/download.php) toocopy over these files from hello cluster tooyour local computer.</span></span> <span data-ttu-id="ebee6-281">Quindi, è possibile utilizzare strumenti toocopy questi file tramite l'account di archiviazione tooyour associati a cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ebee6-281">You can then use tools toocopy these files over tooyour storage account associated with hello cluster.</span></span> <span data-ttu-id="ebee6-282">Per ulteriori informazioni sulla modalità tooupload file toohello account di archiviazione, vedere [caricare dati per i processi di Hadoop in HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="ebee6-282">For more information on how tooupload files toohello storage account, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

<span data-ttu-id="ebee6-283">Dopo aver copiato i file di hello tooyour account di archiviazione di Azure, aprire un prompt dei comandi, passare toohello directory in cui è installato CURL ed eseguire hello comando (nome sostituire nome utente/password e cluster) seguente:</span><span class="sxs-lookup"><span data-stu-id="ebee6-283">Once you have copied over hello files tooyour Azure storage account, open a command prompt, navigate toohello directory where you installed CURL, and run hello following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputHive.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="ebee6-284">Hello parametri nel file hello **inputHive.txt** sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="ebee6-284">hello parameters in hello file **inputHive.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToHiveTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-hive-table", "EventHiveTable10" ], "jars":["wasb:///example/jars/datanucleus-api-jdo-3.2.6.jar", "wasb:///example/jars/datanucleus-rdbms-3.2.9.jar", "wasb:///example/jars/datanucleus-core-3.2.10.jar"], "files":["wasb:///example/jars/hive-site.xml"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="ebee6-285">i parametri di Hello sono simili toowhat specificato per l'output di testo hello, nei passaggi precedenti hello.</span><span class="sxs-lookup"><span data-stu-id="ebee6-285">hello parameters are similar toowhat you specified for hello text output, in hello previous steps.</span></span> <span data-ttu-id="ebee6-286">Nuovamente, non è necessario output di hello toocreate cartelle (EventCheckpoint, EventCount/EventCount10) o hello tabella Hive (EventHiveTable10) che vengono utilizzate come parametri di output.</span><span class="sxs-lookup"><span data-stu-id="ebee6-286">Again, you do not need toocreate hello output folders (EventCheckpoint, EventCount/EventCount10) or hello output Hive table (EventHiveTable10) that are used as parameters.</span></span> <span data-ttu-id="ebee6-287">lo streaming dell'applicazione Hello verranno creati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ebee6-287">hello streaming application creates them for you.</span></span> <span data-ttu-id="ebee6-288">Si noti che hello **JAR** e **file** opzione include i file JAR di percorsi toohello e hello hive-Site.XML che si è copiato toohello account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ebee6-288">Note that hello **jars** and **files** option includes paths toohello .jar files and hello hive-site.xml that you copied over toohello storage account.</span></span>

<span data-ttu-id="ebee6-289">tooverify che hello tabella hive è stato creato correttamente, è possibile SSH in cluster hello e l'esecuzione di query Hive.</span><span class="sxs-lookup"><span data-stu-id="ebee6-289">tooverify that hello hive table was successfully created, you can SSH into hello cluster and run Hive queries.</span></span> <span data-ttu-id="ebee6-290">Per istruzioni, vedere [Usare Hive con Hadoop in HDInsight tramite SSH](hdinsight-hadoop-use-hive-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="ebee6-290">For instructions, see [Use Hive with Hadoop in HDInsight with SSH](hdinsight-hadoop-use-hive-ssh.md).</span></span> <span data-ttu-id="ebee6-291">Quando si è connessi tramite SSH, è possibile eseguire hello successivo comando tooverify tabella Hive, hello **EventHiveTable10**, viene creato.</span><span class="sxs-lookup"><span data-stu-id="ebee6-291">Once you are connected using SSH, you can run hello following command tooverify that hello Hive table, **EventHiveTable10**, is created.</span></span>

    show tables;

<span data-ttu-id="ebee6-292">Verrà visualizzato un segue toohello simili di output:</span><span class="sxs-lookup"><span data-stu-id="ebee6-292">You should see an output similar toohello following:</span></span>

    OK
    eventhivetable10
    hivesampletable

<span data-ttu-id="ebee6-293">È anche possibile eseguire una query SELECT contenuto hello tooview della tabella hello.</span><span class="sxs-lookup"><span data-stu-id="ebee6-293">You can also run a SELECT query tooview hello contents of hello table.</span></span>

    SELECT * FROM eventhivetable10 LIMIT 10;

<span data-ttu-id="ebee6-294">Verrà visualizzato un output simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="ebee6-294">You should see an output like hello following:</span></span>

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


### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-sql-database-table"></a><span data-ttu-id="ebee6-295">Eseguire applicazioni hello eventi hello tooreceive in una tabella di database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="ebee6-295">Run hello applications tooreceive hello events into an Azure SQL database table</span></span>
<span data-ttu-id="ebee6-296">Prima di eseguire questo passaggio, assicurarsi che sia stato creato un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="ebee6-296">Before running this step, make sure you have an Azure SQL database created.</span></span> <span data-ttu-id="ebee6-297">Per istruzioni, vedere [Creare un database SQL in pochi minuti](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ebee6-297">For instructions, see [Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span> <span data-ttu-id="ebee6-298">toocomplete in questa sezione, sono necessari i valori per nome del database, nome del server di database e le credenziali di amministratore di database hello come parametri.</span><span class="sxs-lookup"><span data-stu-id="ebee6-298">toocomplete this section, you need values for database name, database server name, and hello database administrator credentials as parameters.</span></span> <span data-ttu-id="ebee6-299">Tabella di database hello toocreate non è necessario tuttavia.</span><span class="sxs-lookup"><span data-stu-id="ebee6-299">You do not need toocreate hello database table though.</span></span> <span data-ttu-id="ebee6-300">che l'applicazione streaming Spark Hello creata.</span><span class="sxs-lookup"><span data-stu-id="ebee6-300">hello Spark streaming application creates that for you.</span></span>

<span data-ttu-id="ebee6-301">Aprire un prompt dei comandi, passare toohello directory in cui è installato CURL ed eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ebee6-301">Open a command prompt, navigate toohello directory where you installed CURL, and run hello following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputSQL.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="ebee6-302">Hello parametri nel file hello **inputSQL.txt** sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="ebee6-302">hello parameters in hello file **inputSQL.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureSQLTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--sql-server-fqdn", "<database-server-name>.database.windows.net", "--sql-database-name", "mysparkdatabase", "--database-username", "sparkdbadmin", "--database-password", "<put-password-here>", "--event-sql-table", "EventContent" ], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="ebee6-303">tooverify che hello applicazione viene eseguita correttamente, è possibile connettersi a database SQL di Azure toohello utilizzando SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="ebee6-303">tooverify that hello application runs successfully, you can connect toohello Azure SQL database using SQL Server Management Studio.</span></span> <span data-ttu-id="ebee6-304">Per istruzioni su come toodo che, vedere [connettersi tooSQL Database con SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="ebee6-304">For instructions on how toodo that, see [Connect tooSQL Database with SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md).</span></span> <span data-ttu-id="ebee6-305">Dopo avere connesso toohello database, è possibile passare toohello **EventContent** tabella in cui è stata creata da hello streaming dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ebee6-305">Once you are connected toohello database, you can navigate toohello **EventContent** table that was created by hello streaming application.</span></span> <span data-ttu-id="ebee6-306">È possibile eseguire dei dati di query rapida tooget hello dalla tabella hello.</span><span class="sxs-lookup"><span data-stu-id="ebee6-306">You can run a quick query tooget hello data from hello table.</span></span> <span data-ttu-id="ebee6-307">Eseguire hello seguente query:</span><span class="sxs-lookup"><span data-stu-id="ebee6-307">Run hello following query:</span></span>

    SELECT * FROM EventCount

<span data-ttu-id="ebee6-308">Verrà visualizzato il seguente toohello simili di output:</span><span class="sxs-lookup"><span data-stu-id="ebee6-308">You should see output similar toohello following:</span></span>

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


## <span data-ttu-id="ebee6-309"><a name="seealso"></a>Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ebee6-309"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="ebee6-310">Panoramica: Apache Spark su Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="ebee6-310">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)
* [<span data-ttu-id="ebee6-311">Design of Receiver-based Connection and Direct DStream</span><span class="sxs-lookup"><span data-stu-id="ebee6-311">Design of Receiver-based Connection and Direct DStream</span></span>](https://www.slideshare.net/NanZhu/seattle-sparkmeetup032317)

### <a name="scenarios"></a><span data-ttu-id="ebee6-312">Scenari</span><span class="sxs-lookup"><span data-stu-id="ebee6-312">Scenarios</span></span>
* [<span data-ttu-id="ebee6-313">Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="ebee6-313">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="ebee6-314">Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC</span><span class="sxs-lookup"><span data-stu-id="ebee6-314">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="ebee6-315">Spark con Machine Learning: usare Spark in HDInsight risultati dell'ispezione alimentare toopredict</span><span class="sxs-lookup"><span data-stu-id="ebee6-315">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="ebee6-316">Analisi dei log del sito Web mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="ebee6-316">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="ebee6-317">Creare ed eseguire applicazioni</span><span class="sxs-lookup"><span data-stu-id="ebee6-317">Create and run applications</span></span>
* [<span data-ttu-id="ebee6-318">Creare un'applicazione autonoma con Scala</span><span class="sxs-lookup"><span data-stu-id="ebee6-318">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="ebee6-319">Eseguire processi in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="ebee6-319">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="ebee6-320">Strumenti ed estensioni</span><span class="sxs-lookup"><span data-stu-id="ebee6-320">Tools and extensions</span></span>
* [<span data-ttu-id="ebee6-321">Utilizzare i plug-in strumenti di HDInsight per toocreate IntelliJ IDEA e inviare applicazioni Spark Scala</span><span class="sxs-lookup"><span data-stu-id="ebee6-321">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="ebee6-322">Utilizzare i plug-in strumenti di HDInsight per le applicazioni di Spark toodebug IntelliJ IDEA in modalità remota</span><span class="sxs-lookup"><span data-stu-id="ebee6-322">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="ebee6-323">Usare i notebook di Zeppelin con un cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="ebee6-323">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="ebee6-324">Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight</span><span class="sxs-lookup"><span data-stu-id="ebee6-324">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="ebee6-325">Usare pacchetti esterni con i notebook Jupyter</span><span class="sxs-lookup"><span data-stu-id="ebee6-325">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="ebee6-326">Installare Jupyter nel computer e connettere il cluster HDInsight Spark tooan</span><span class="sxs-lookup"><span data-stu-id="ebee6-326">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="ebee6-327">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="ebee6-327">Manage resources</span></span>
* [<span data-ttu-id="ebee6-328">Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure</span><span class="sxs-lookup"><span data-stu-id="ebee6-328">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="ebee6-329">Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="ebee6-329">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]: ../storage-create-storage-account/
