---
title: Analizzare i dati dei sensori con Apache Storm e HBase | Documentazione Microsoft
description: Informazioni su come connettersi ad Apache Storm con una rete virtuale. Usare Storm con HBase per elaborare i dati del sensore da un hub eventi e visualizzarli con D3.js.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a9a1ac8e-5708-4833-b965-e453815e671f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/09/2017
ms.author: larryfr
ms.openlocfilehash: 0d1cc959c87bd64ed728f8b56c9b9156fa492a8b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="analyze-sensor-data-with-apache-storm-event-hub-and-hbase-in-hdinsight-hadoop"></a><span data-ttu-id="bb254-104">Analizzare i dati del sensore con Apache Storm, hub eventi e HBase in HDInsight (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="bb254-104">Analyze sensor data with Apache Storm, Event Hub, and HBase in HDInsight (Hadoop)</span></span>

<span data-ttu-id="bb254-105">Informazioni su come usare Apache Storm in HDInsight per elaborare i dati del sensore dall'hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="bb254-105">Learn how to use Apache Storm on HDInsight to process sensor data from Azure Event Hub.</span></span> <span data-ttu-id="bb254-106">I dati vengono quindi archiviati in Apache HBase in HDInsight e visualizzati con D3.js.</span><span class="sxs-lookup"><span data-stu-id="bb254-106">The data is then stored into Apache HBase on HDInsight, and visualized using D3.js.</span></span>

<span data-ttu-id="bb254-107">Il modello di Azure Resource Manager usato in questo documento illustra come creare più risorse di Azure in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="bb254-107">The Azure Resource Manager template used in this document demonstrates how to create multiple Azure resources in a resource group.</span></span> <span data-ttu-id="bb254-108">Il modello crea una rete virtuale di Azure, due cluster HDInsight (Storm e HBase) e un'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="bb254-108">The template creates an Azure Virtual Network, two HDInsight clusters (Storm and HBase) and an Azure Web App.</span></span> <span data-ttu-id="bb254-109">Un'implementazione di Node. js di un dashboard Web in tempo reale viene distribuita automaticamente all'app web.</span><span class="sxs-lookup"><span data-stu-id="bb254-109">A node.js implementation of a real-time web dashboard is automatically deployed to the web app.</span></span>

> [!NOTE]
> <span data-ttu-id="bb254-110">Le informazioni e l'esempio riportati in questo documento richiedono HDInsight versione 3.6.</span><span class="sxs-lookup"><span data-stu-id="bb254-110">The information in this document and example in this document require HDInsight version 3.6.</span></span>
>
> <span data-ttu-id="bb254-111">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="bb254-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="bb254-112">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="bb254-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb254-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bb254-113">Prerequisites</span></span>

* <span data-ttu-id="bb254-114">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="bb254-114">An Azure subscription.</span></span>
* <span data-ttu-id="bb254-115">[Node.js](http://nodejs.org/): viene usato per visualizzare in anteprima il dashboard Web in locale nell'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="bb254-115">[Node.js](http://nodejs.org/): Used to preview the web dashboard locally on your development environment.</span></span>
* <span data-ttu-id="bb254-116">[Java e JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): usati per sviluppare la topologia Storm.</span><span class="sxs-lookup"><span data-stu-id="bb254-116">[Java and the JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): Used to develop the Storm topology.</span></span>
* <span data-ttu-id="bb254-117">[Maven](http://maven.apache.org/what-is-maven.html): usato per generare e compilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="bb254-117">[Maven](http://maven.apache.org/what-is-maven.html): Used to build and compile the project.</span></span>
* <span data-ttu-id="bb254-118">[Git](http://git-scm.com/): usato per scaricare il progetto da GitHub.</span><span class="sxs-lookup"><span data-stu-id="bb254-118">[Git](http://git-scm.com/): Used to download the project from GitHub.</span></span>
* <span data-ttu-id="bb254-119">Client **SSH** : usato per connettersi al cluster HDInsight basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="bb254-119">An **SSH** client: Used to connect to the Linux-based HDInsight clusters.</span></span> <span data-ttu-id="bb254-120">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="bb254-120">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="bb254-121">Non è necessario un cluster HDInsight esistente.</span><span class="sxs-lookup"><span data-stu-id="bb254-121">You do not need an existing HDInsight cluster.</span></span> <span data-ttu-id="bb254-122">La procedura descritta in questo documento consente di creare le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="bb254-122">The steps in this document create the following resources:</span></span>
> 
> * <span data-ttu-id="bb254-123">Una rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="bb254-123">An Azure Virtual Network</span></span>
> * <span data-ttu-id="bb254-124">Un cluster Storm in HDInsight (basato su Linux con due nodi del ruolo di lavoro)</span><span class="sxs-lookup"><span data-stu-id="bb254-124">A Storm on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="bb254-125">Un cluster HBase in HDInsight (basato su Linux con due nodi del ruolo di lavoro)</span><span class="sxs-lookup"><span data-stu-id="bb254-125">An HBase on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="bb254-126">Un'app Web di Azure che ospita il dashboard Web</span><span class="sxs-lookup"><span data-stu-id="bb254-126">An Azure Web App that hosts the web dashboard</span></span>

## <a name="architecture"></a><span data-ttu-id="bb254-127">Architettura</span><span class="sxs-lookup"><span data-stu-id="bb254-127">Architecture</span></span>

![diagramma dell'architettura](./media/hdinsight-storm-sensor-data-analysis/devicesarchitecture.png)

<span data-ttu-id="bb254-129">Questo esempio è costituito dai componenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="bb254-129">This example consists of the following components:</span></span>

* <span data-ttu-id="bb254-130">**Hub eventi di Azure**: include i dati raccolti dai sensori.</span><span class="sxs-lookup"><span data-stu-id="bb254-130">**Azure Event Hubs**: Contains data that is collected from sensors.</span></span>
* <span data-ttu-id="bb254-131">**Storm in HDInsight**: assicura l'elaborazione in tempo reale dei dati provenienti dall'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="bb254-131">**Storm on HDInsight**: Provides real-time processing of data from Event Hub.</span></span>
* <span data-ttu-id="bb254-132">**HBase in HDInsight**: fornisce un archivio dati NoSQL persistente per i dati, dopo l'elaborazione tramite Storm.</span><span class="sxs-lookup"><span data-stu-id="bb254-132">**HBase on HDInsight**: Provides a persistent NoSQL data store for data after it has been processed by Storm.</span></span>
* <span data-ttu-id="bb254-133">**Servizio Rete virtuale di Azure**: abilita la comunicazione sicura tra i cluster Storm in HDInsight e HBase in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bb254-133">**Azure Virtual Network service**: Enables secure communications between the Storm on HDInsight and HBase on HDInsight clusters.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="bb254-134">Quando si usa l'API del client Java HBase, è necessaria una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="bb254-134">A virtual network is required when using the Java HBase client API.</span></span> <span data-ttu-id="bb254-135">non esposta nel gateway pubblico per i cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="bb254-135">It is not exposed over the public gateway for HBase clusters.</span></span> <span data-ttu-id="bb254-136">L'installazione di cluster HBase e Storm nella stessa rete virtuale consente al cluster Storm, o a qualsiasi altro sistema nella rete virtuale, di accedere direttamente a HBase tramite l'API del client.</span><span class="sxs-lookup"><span data-stu-id="bb254-136">Installing HBase and Storm clusters into the same virtual network allows the Storm cluster (or any other system on the virtual network) to directly access HBase using client API.</span></span>

* <span data-ttu-id="bb254-137">**Sito Web del dashboard**: dashboard di esempio che rappresenta graficamente i dati in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="bb254-137">**Dashboard website**: An example dashboard that charts data in real time.</span></span>
  
  * <span data-ttu-id="bb254-138">Il sito Web viene implementato in Node.js.</span><span class="sxs-lookup"><span data-stu-id="bb254-138">The website is implemented in Node.js.</span></span>
  * <span data-ttu-id="bb254-139">[Socket.io](http://socket.io/) viene usato per le comunicazioni in tempo reale tra la topologia Storm e il sito Web.</span><span class="sxs-lookup"><span data-stu-id="bb254-139">[Socket.io](http://socket.io/) is used for real-time communication between the Storm topology and the website.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="bb254-140">L'uso di Socket.io per la comunicazione è un dettaglio di implementazione.</span><span class="sxs-lookup"><span data-stu-id="bb254-140">Using Socket.io for communication is an implementation detail.</span></span> <span data-ttu-id="bb254-141">È possibile usare qualsiasi framework di comunicazione, ad esempio WebSocket o SignalR non elaborato.</span><span class="sxs-lookup"><span data-stu-id="bb254-141">You can use any communications framework, such as raw WebSockets or SignalR.</span></span>

  * <span data-ttu-id="bb254-142">[D3.js](http://d3js.org/) viene usato per creare un grafico dei dati inviati al sito Web.</span><span class="sxs-lookup"><span data-stu-id="bb254-142">[D3.js](http://d3js.org/) is used to graph the data that is sent to the website.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bb254-143">Sono necessari due cluster perché non è supportato alcun metodo per la creazione di un unico cluster HDInsight per Storm e HBase.</span><span class="sxs-lookup"><span data-stu-id="bb254-143">Two clusters are required, as there is no supported method to create one HDInsight cluster for both Storm and HBase.</span></span>

<span data-ttu-id="bb254-144">La topologia legge i dati dall'hub eventi tramite la classe [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) e scrive i dati in HBase usando la classe [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html).</span><span class="sxs-lookup"><span data-stu-id="bb254-144">The topology reads data from Event Hub by using the [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) class, and writes data into HBase using the [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) class.</span></span> <span data-ttu-id="bb254-145">Per la comunicazione con il sito Web viene usato [socket.io-client.java](https://github.com/nkzawa/socket.io-client.java).</span><span class="sxs-lookup"><span data-stu-id="bb254-145">Communication with the website is accomplished by using [socket.io-client.java](https://github.com/nkzawa/socket.io-client.java).</span></span>

<span data-ttu-id="bb254-146">Nel diagramma seguente viene illustrato il layout della topologia:</span><span class="sxs-lookup"><span data-stu-id="bb254-146">The following diagram explains the layout of the topology:</span></span>

![diagramma della topologia](./media/hdinsight-storm-sensor-data-analysis/sensoranalysis.png)

> [!NOTE]
> <span data-ttu-id="bb254-148">Questo diagramma è una visualizzazione semplificata della topologia.</span><span class="sxs-lookup"><span data-stu-id="bb254-148">This diagram is a simplified view of the topology.</span></span> <span data-ttu-id="bb254-149">Per ogni partizione dell'hub eventi viene creata un'istanza di ogni componente.</span><span class="sxs-lookup"><span data-stu-id="bb254-149">An instance of each component is created for each partition in your Event Hub.</span></span> <span data-ttu-id="bb254-150">Queste istanze vengono distribuite tra i nodi del cluster e i dati vengono instradati tra di essi, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="bb254-150">These instances are distributed across the nodes in the cluster, and data is routed between them as follows:</span></span>
> 
> * <span data-ttu-id="bb254-151">I dati trasmessi dallo spout al parser sono sottoposti a bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="bb254-151">Data from the spout to the parser is load balanced.</span></span>
> * <span data-ttu-id="bb254-152">I dati dal parser al dashboard e ad HBase vengono raggruppati per ID dispositivo, in modo che il flusso di messaggi provenienti dallo stesso dispositivo siano indirizzati sempre allo stesso componente.</span><span class="sxs-lookup"><span data-stu-id="bb254-152">Data from the parser to the Dashboard and HBase is grouped by Device ID, so that messages from the same device always flow to the same component.</span></span>

### <a name="topology-components"></a><span data-ttu-id="bb254-153">Componenti della topologia</span><span class="sxs-lookup"><span data-stu-id="bb254-153">Topology components</span></span>

* <span data-ttu-id="bb254-154">**EventHub Spout**: lo spout viene fornito come parte di Apache Storm 0.10.0 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="bb254-154">**Event Hub Spout**: The spout is provided as part of Apache Storm version 0.10.0 and higher.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="bb254-155">Lo spout dell'hub eventi usato in questo esempio richiede un cluster Storm in HDInsight versione 3.5 o 3.6.</span><span class="sxs-lookup"><span data-stu-id="bb254-155">The Event Hub spout used in this example requires a Storm on HDInsight cluster version 3.5 or 3.6.</span></span>

* <span data-ttu-id="bb254-156">**ParserBolt.java**: i dati generati dallo spout sono dati JSON non elaborati. In alcuni casi vengono generati più eventi alla volta.</span><span class="sxs-lookup"><span data-stu-id="bb254-156">**ParserBolt.java**: The data that is emitted by the spout is raw JSON, and occasionally more than one event is emitted at a time.</span></span> <span data-ttu-id="bb254-157">Il bolt legge i dati generati dallo spout e analizza il messaggio JSON.</span><span class="sxs-lookup"><span data-stu-id="bb254-157">This bolt reads the data emitted by the spout and parses the JSON message.</span></span> <span data-ttu-id="bb254-158">Il bolt genera quindi i dati come tupla contenente più campi.</span><span class="sxs-lookup"><span data-stu-id="bb254-158">The bolt then emits the data as a tuple that contains multiple fields.</span></span>
* <span data-ttu-id="bb254-159">**DashboardBolt.java**: questo componente mostra come usare la libreria client Socket.io per Java per inviare dati in tempo reale al dashboard Web.</span><span class="sxs-lookup"><span data-stu-id="bb254-159">**DashboardBolt.java**: This component demonstrates how to use the Socket.io client library for Java to send data in real time to the web dashboard.</span></span>
* <span data-ttu-id="bb254-160">**no-hbase.yaml**: definizione della topologia usata per l'esecuzione in modalità locale.</span><span class="sxs-lookup"><span data-stu-id="bb254-160">**no-hbase.yaml**: The topology definition used when running in local mode.</span></span> <span data-ttu-id="bb254-161">Non usa componenti HBase.</span><span class="sxs-lookup"><span data-stu-id="bb254-161">It does not use HBase components.</span></span>
* <span data-ttu-id="bb254-162">**with-hbase.yaml**: definizione della topologia usata per l'esecuzione della topologia nel cluster.</span><span class="sxs-lookup"><span data-stu-id="bb254-162">**with-hbase.yaml**: The topology definition used when running the topology on the cluster.</span></span> <span data-ttu-id="bb254-163">Usa componenti HBase.</span><span class="sxs-lookup"><span data-stu-id="bb254-163">It does use HBase components.</span></span>
* <span data-ttu-id="bb254-164">**dev.properties**: informazioni di configurazione per lo spout dell'hub eventi, il bolt HBase e i componenti del dashboard.</span><span class="sxs-lookup"><span data-stu-id="bb254-164">**dev.properties**: The configuration information for the Event Hub spout, HBase bolt, and dashboard components.</span></span>

## <a name="prepare-your-environment"></a><span data-ttu-id="bb254-165">Preparare l'ambiente</span><span class="sxs-lookup"><span data-stu-id="bb254-165">Prepare your environment</span></span>

<span data-ttu-id="bb254-166">Prima di usare questo esempio, è necessario creare un hub eventi di Azure, che viene letto dalla topologia Storm.</span><span class="sxs-lookup"><span data-stu-id="bb254-166">Before you use this example, you must create an Azure Event Hub, which the Storm topology reads from.</span></span>

### <a name="configure-event-hub"></a><span data-ttu-id="bb254-167">Configurare l'hub eventi</span><span class="sxs-lookup"><span data-stu-id="bb254-167">Configure Event Hub</span></span>

<span data-ttu-id="bb254-168">L'hub eventi è l'origine dati per questo esempio.</span><span class="sxs-lookup"><span data-stu-id="bb254-168">Event Hub is the data source for this example.</span></span> <span data-ttu-id="bb254-169">Per creare un nuovo hub eventi, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="bb254-169">Use the following steps to create an Event Hub.</span></span>

1. <span data-ttu-id="bb254-170">Dal [portale di Azure](https://portal.azure.com) selezionare **+ Nuovo** -> **Internet delle cose** -> **Hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="bb254-170">From the [Azure portal](https://portal.azure.com), select **+ New** -> **Internet of Things** -> **Event Hubs**.</span></span>
2. <span data-ttu-id="bb254-171">Nella sezione **Crea spazio dei nomi** eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="bb254-171">In the **Create Namespace** section, perform the following tasks:</span></span>
   
   1. <span data-ttu-id="bb254-172">Immettere un **nome** per lo spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="bb254-172">Enter a **Name** for the namespace.</span></span>
   2. <span data-ttu-id="bb254-173">Selezione di un piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="bb254-173">Select a pricing tier.</span></span> <span data-ttu-id="bb254-174">**Basic** è sufficiente per questo esempio.</span><span class="sxs-lookup"><span data-stu-id="bb254-174">**Basic** is sufficient for this example.</span></span>
   3. <span data-ttu-id="bb254-175">Selezionare la **sottoscrizione** di Azure da usare.</span><span class="sxs-lookup"><span data-stu-id="bb254-175">Select the Azure **Subscription** to use.</span></span>
   4. <span data-ttu-id="bb254-176">Selezionare un gruppo di risorse esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="bb254-176">Either select an existing resource group or create a new one.</span></span>
   5. <span data-ttu-id="bb254-177">Selezionare il **percorso** per l'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="bb254-177">Select the **Location** for the Event Hub.</span></span>
   6. <span data-ttu-id="bb254-178">Selezionare **Aggiungi al dashboard** e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="bb254-178">Select **Pin to dashboard**, and then click **Create**.</span></span>

3. <span data-ttu-id="bb254-179">Al termine del processo di creazione, vengono visualizzate le informazioni relative agli hub eventi per lo spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="bb254-179">When the creation process completes, the Event Hubs information for your namespace is displayed.</span></span> <span data-ttu-id="bb254-180">Da qui, scegliere **+ Aggiungi hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="bb254-180">From here, select **+ Add Event Hub**.</span></span> <span data-ttu-id="bb254-181">Nella sezione **Crea hub eventi** immettere un nome per **sensordata** e quindi selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="bb254-181">In the **Create Event Hub** section, enter a name of **sensordata**, and then select **Create**.</span></span> <span data-ttu-id="bb254-182">Mantenere i valori predefiniti per gli altri campi.</span><span class="sxs-lookup"><span data-stu-id="bb254-182">Leave the other fields at the default values.</span></span>
4. <span data-ttu-id="bb254-183">Dalla visualizzazione Hub eventi per lo spazio dei nomi selezionare **Hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="bb254-183">From the Event Hubs view for your namespace, select **Event Hubs**.</span></span> <span data-ttu-id="bb254-184">Selezionare la voce **sensordata** .</span><span class="sxs-lookup"><span data-stu-id="bb254-184">Select the **sensordata** entry.</span></span>
5. <span data-ttu-id="bb254-185">Dall'hub eventi per sensordata selezionare **Criteri di accesso condiviso**.</span><span class="sxs-lookup"><span data-stu-id="bb254-185">From the sensordata Event Hub, select **Shared access policies**.</span></span> <span data-ttu-id="bb254-186">Utilizzare il collegamento **+ Aggiungi** per aggiungere i seguenti criteri:</span><span class="sxs-lookup"><span data-stu-id="bb254-186">Use the **+ Add** link to add the following policies:</span></span>

    | <span data-ttu-id="bb254-187">Nome criterio</span><span class="sxs-lookup"><span data-stu-id="bb254-187">Policy name</span></span> | <span data-ttu-id="bb254-188">Claims</span><span class="sxs-lookup"><span data-stu-id="bb254-188">Claims</span></span> |
    | ----- | ----- |
    | <span data-ttu-id="bb254-189">devices</span><span class="sxs-lookup"><span data-stu-id="bb254-189">devices</span></span> | <span data-ttu-id="bb254-190">Invio</span><span class="sxs-lookup"><span data-stu-id="bb254-190">Send</span></span> |
    | <span data-ttu-id="bb254-191">storm</span><span class="sxs-lookup"><span data-stu-id="bb254-191">storm</span></span> | <span data-ttu-id="bb254-192">Attesa</span><span class="sxs-lookup"><span data-stu-id="bb254-192">Listen</span></span> |

1. <span data-ttu-id="bb254-193">Selezionare entrambi i criteri e annotare il valore **PRIMARY KEY** .</span><span class="sxs-lookup"><span data-stu-id="bb254-193">Select both policies and make a note of the **PRIMARY KEY** value.</span></span> <span data-ttu-id="bb254-194">Il valore di entrambi i criteri servirà nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="bb254-194">You need the value for both policies in future steps.</span></span>

## <a name="download-and-configure-the-project"></a><span data-ttu-id="bb254-195">Scaricare e configurare il progetto</span><span class="sxs-lookup"><span data-stu-id="bb254-195">Download and configure the project</span></span>

<span data-ttu-id="bb254-196">Usare il comando seguente per scaricare il progetto da GitHub.</span><span class="sxs-lookup"><span data-stu-id="bb254-196">Use the following to download the project from GitHub.</span></span>

    git clone https://github.com/Blackmist/hdinsight-eventhub-example

<span data-ttu-id="bb254-197">Dopo aver eseguito il comando, si otterrà la struttura di directory seguente:</span><span class="sxs-lookup"><span data-stu-id="bb254-197">After the command completes, you have the following directory structure:</span></span>

    hdinsight-eventhub-example/
        TemperatureMonitor/ - this contains the topology
            resources/
                log4j2.xml - set logging to minimal.
                no-hbase.yaml - topology definition without hbase components.
                with-hbase.yaml - topology definition with hbase components.
            src/main/java/com/microsoft/examples/bolts/
                ParserBolt.java - parses JSON data into tuples
                DashboardBolt.java - sends data over Socket.IO to the web dashboard.
        dashboard/nodejs/ - this is the node.js web dashboard.
        SendEvents/ - utilities to send fake sensor data.

> [!NOTE]
> <span data-ttu-id="bb254-198">Questo documento non fornisce i dettagli completi del codice incluso nell'esempio.</span><span class="sxs-lookup"><span data-stu-id="bb254-198">This document does not go in to full details of the code included in this example.</span></span> <span data-ttu-id="bb254-199">Il codice, tuttavia, è completamente commentato.</span><span class="sxs-lookup"><span data-stu-id="bb254-199">However, the code is fully commented.</span></span>

<span data-ttu-id="bb254-200">Per configurare il progetto da leggere dall'hub eventi, aprire il file `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` e aggiungere le informazioni relative all'hub eventi alle righe seguenti:</span><span class="sxs-lookup"><span data-stu-id="bb254-200">To configure the project to read from Event Hub, open the `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` file and add your Event Hub information to the following lines:</span></span>

```bash
eventhub.read.policy.name: your_read_policy_name
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: your_event_hub_name
eventhub.partitions: 2
```

## <a name="compile-and-test-locally"></a><span data-ttu-id="bb254-201">Compilare ed eseguire il test in locale</span><span class="sxs-lookup"><span data-stu-id="bb254-201">Compile and test locally</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bb254-202">L'uso della topologia in locale richiede un ambiente di sviluppo Storm funzionante.</span><span class="sxs-lookup"><span data-stu-id="bb254-202">Using the topology locally requires a working Storm development environment.</span></span> <span data-ttu-id="bb254-203">Per altre informazioni, vedere [Setting up a development environment](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) (Impostazione di un ambiente di sviluppo) in Apache.org.</span><span class="sxs-lookup"><span data-stu-id="bb254-203">For more information, see [Setting up a Storm development environment](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) at Apache.org.</span></span>

> [!WARNING]
> <span data-ttu-id="bb254-204">Se si usa un ambiente di sviluppo Windows, si potrebbe ricevere un'eccezione `java.io.IOException` quando si esegue la topologia in locale.</span><span class="sxs-lookup"><span data-stu-id="bb254-204">If you are using a Windows development environment, you may receive a `java.io.IOException` when running the topology locally.</span></span> <span data-ttu-id="bb254-205">In questo caso, eseguire la topologia in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bb254-205">If so, move on to running the topology on HDInsight.</span></span>

<span data-ttu-id="bb254-206">Prima di eseguire il test, è necessario avviare il dashboard per visualizzare l'output della topologia e generare i dati da archiviare nell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="bb254-206">Before testing, you must start the dashboard to view the output of the topology and generate data to store in Event Hub.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bb254-207">Il componente HBase di questa topologia non è attivo durante il test locale,</span><span class="sxs-lookup"><span data-stu-id="bb254-207">The HBase component of this topology is not active when testing locally.</span></span> <span data-ttu-id="bb254-208">L'API Java per il cluster HBase non è accessibile dall'esterno della rete virtuale di Azure che contiene i cluster.</span><span class="sxs-lookup"><span data-stu-id="bb254-208">The Java API for the HBase cluster cannot be accessed from outside the Azure Virtual Network that contains the clusters.</span></span>

### <a name="start-the-web-application"></a><span data-ttu-id="bb254-209">Avviare l'applicazione Web</span><span class="sxs-lookup"><span data-stu-id="bb254-209">Start the web application</span></span>

1. <span data-ttu-id="bb254-210">Aprire un prompt dei comandi e passare alla directory `hdinsight-eventhub-example/dashboard`.</span><span class="sxs-lookup"><span data-stu-id="bb254-210">Open a command prompt and change directories to `hdinsight-eventhub-example/dashboard`.</span></span> <span data-ttu-id="bb254-211">Usare il comando seguente per installare le dipendenze richieste dall'applicazione Web:</span><span class="sxs-lookup"><span data-stu-id="bb254-211">Use the following command to install the dependencies needed by the web application:</span></span>
   
    ```bash
    npm install
    ```

2. <span data-ttu-id="bb254-212">Usare il comando seguente per avviare l'applicazione Web:</span><span class="sxs-lookup"><span data-stu-id="bb254-212">Use the following command to start the web application:</span></span>
   
    ```bash
    node server.js
    ```
   
    <span data-ttu-id="bb254-213">Verrà visualizzato un messaggio simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="bb254-213">You see a message similar to the following text:</span></span>
   
        Server listening at port 3000

3. <span data-ttu-id="bb254-214">Aprire un Web browser e immettere `http://localhost:3000/` come indirizzo.</span><span class="sxs-lookup"><span data-stu-id="bb254-214">Open a web browser and enter `http://localhost:3000/` as the address.</span></span> <span data-ttu-id="bb254-215">Viene visualizzata una pagina simile all'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="bb254-215">A page similar to the following image is displayed:</span></span>
   
    ![dashboard Web](./media/hdinsight-storm-sensor-data-analysis/emptydashboard.png)
   
    <span data-ttu-id="bb254-217">Lasciare il prompt dei comandi aperto.</span><span class="sxs-lookup"><span data-stu-id="bb254-217">Leave this command prompt open.</span></span> <span data-ttu-id="bb254-218">Al termine del test, usare CTRL+C per arrestare il server Web.</span><span class="sxs-lookup"><span data-stu-id="bb254-218">After testing, use Ctrl-C to stop the web server.</span></span>

### <a name="generate-data"></a><span data-ttu-id="bb254-219">Generare i dati</span><span class="sxs-lookup"><span data-stu-id="bb254-219">Generate data</span></span>

> [!NOTE]
> <span data-ttu-id="bb254-220">I passaggi descritti in questa sezione usano Node.js, così da poter essere usati su qualsiasi piattaforma.</span><span class="sxs-lookup"><span data-stu-id="bb254-220">The steps in this section use Node.js so that they can be used on any platform.</span></span> <span data-ttu-id="bb254-221">Per esempi in altri linguaggi, vedere la directory `SendEvents`.</span><span class="sxs-lookup"><span data-stu-id="bb254-221">For other language examples, see the `SendEvents` directory.</span></span>

1. <span data-ttu-id="bb254-222">Aprire un nuovo prompt, shell o terminale e passare alla directory `hdinsight-eventhub-example/SendEvents/nodejs`.</span><span class="sxs-lookup"><span data-stu-id="bb254-222">Open a new prompt, shell, or terminal, and change directories to `hdinsight-eventhub-example/SendEvents/nodejs`.</span></span> <span data-ttu-id="bb254-223">Usare il comando seguente per installare le dipendenze richieste dall'applicazione:</span><span class="sxs-lookup"><span data-stu-id="bb254-223">To install the dependencies needed by the application, use the following command:</span></span>

    ```bash
    npm install
    ```

2. <span data-ttu-id="bb254-224">Aprire il file `app.js` in un editor di testo e aggiungere le informazioni relative all'hub eventi ottenute in precedenza:</span><span class="sxs-lookup"><span data-stu-id="bb254-224">Open the `app.js` file in a text editor and add the Event Hub information you obtained earlier:</span></span>
   
    ```javascript
    // ServiceBus Namespace
    var namespace = 'YourNamespace';
    // Event Hub Name
    var hubname ='sensordata';
    // Shared access Policy name and key (from Event Hub configuration)
    var my_key_name = 'devices';
    var my_key = 'YourKey';
    ```
   
   > [!NOTE]
   > <span data-ttu-id="bb254-225">Questo esempio presuppone che sia stato usato `sensordata` come nome dell'hub eventi</span><span class="sxs-lookup"><span data-stu-id="bb254-225">This example assumes that you have used `sensordata` as the name of your Event Hub.</span></span> <span data-ttu-id="bb254-226">e `devices` come nome del criterio che include un'attestazione `Send`.</span><span class="sxs-lookup"><span data-stu-id="bb254-226">And that `devices` as the name of the policy that has a `Send` claim.</span></span>

3. <span data-ttu-id="bb254-227">Usare il comando seguente per inserire nuove voci nell'hub eventi:</span><span class="sxs-lookup"><span data-stu-id="bb254-227">Use the following command to insert new entries in Event Hub:</span></span>
   
    ```bash
    node app.js
    ```
   
    <span data-ttu-id="bb254-228">Verranno visualizzate diverse righe di output contenenti i dati inviati all'hub eventi:</span><span class="sxs-lookup"><span data-stu-id="bb254-228">You see several lines of output that contain the data sent to Event Hub:</span></span>
   
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"0","Temperature":7}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"1","Temperature":39}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"2","Temperature":86}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"3","Temperature":29}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"4","Temperature":30}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"5","Temperature":5}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"6","Temperature":24}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"7","Temperature":40}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"8","Temperature":43}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"9","Temperature":84}

### <a name="build-and-start-the-topology"></a><span data-ttu-id="bb254-229">Creare e avviare la topologia</span><span class="sxs-lookup"><span data-stu-id="bb254-229">Build and start the topology</span></span>

1. <span data-ttu-id="bb254-230">Aprire un nuovo prompt dei comandi e passare alla directory `hdinsight-eventhub-example/TemperatureMonitor`.</span><span class="sxs-lookup"><span data-stu-id="bb254-230">Open a new command prompt and change directories to `hdinsight-eventhub-example/TemperatureMonitor`.</span></span> <span data-ttu-id="bb254-231">Per compilare e creare la topologia, usare il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="bb254-231">To build and package the topology, use the following command:</span></span> 

    ```bash
    mvn clean package
    ```

2. <span data-ttu-id="bb254-232">Per avviare la topologia in modalità locale, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="bb254-232">To start the topology in local mode, use the following command:</span></span>

    ```bash
    storm jar target/TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local --filter dev.properties resources/no-hbase.yaml
    ```

    * <span data-ttu-id="bb254-233">`--local` avvia la topologia in modalità locale.</span><span class="sxs-lookup"><span data-stu-id="bb254-233">`--local` starts the topology in local mode.</span></span>
    * <span data-ttu-id="bb254-234">`--filter` usa il file `dev.properties` per immettere i parametri nella definizione della topologia.</span><span class="sxs-lookup"><span data-stu-id="bb254-234">`--filter` uses the `dev.properties` file to populate parameters in the topology definition.</span></span>
    * <span data-ttu-id="bb254-235">`resources/no-hbase.yaml` usa la definizione di topologia `no-hbase.yaml`.</span><span class="sxs-lookup"><span data-stu-id="bb254-235">`resources/no-hbase.yaml` uses the `no-hbase.yaml` topology definition.</span></span>
 
   <span data-ttu-id="bb254-236">Una volta avviata, la topologia legge le voci dall'hub eventi e le invia al dashboard in esecuzione sul computer locale.</span><span class="sxs-lookup"><span data-stu-id="bb254-236">Once started, the topology reads entries from Event Hub, and sends them to the dashboard running on your local machine.</span></span> <span data-ttu-id="bb254-237">Nel dashboard Web dovrebbero comparire linee simili a quelle nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="bb254-237">You should see lines appear in the web dashboard, similar to the following image:</span></span>
   
    ![dashboard con dati](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

2. <span data-ttu-id="bb254-239">Mentre il dashboard è in esecuzione, usare il comando `node app.js` dai passaggi precedenti per inviare nuovi dati agli hub eventi.</span><span class="sxs-lookup"><span data-stu-id="bb254-239">While the dashboard is running, use the `node app.js` command from the previous steps to send new data to Event Hubs.</span></span> <span data-ttu-id="bb254-240">Poiché i valori di temperatura vengono generati in modo casuale, il grafico deve aggiornarsi per visualizzare le modifiche estese della temperatura.</span><span class="sxs-lookup"><span data-stu-id="bb254-240">Because the temperature values are randomly generated, the graph should update to show large changes in temperature.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bb254-241">Per usare il comando `node app.js` è necessario trovarsi nella directory **hdinsight-eventhub-example/SendEvents/Nodejs**.</span><span class="sxs-lookup"><span data-stu-id="bb254-241">You must be in the **hdinsight-eventhub-example/SendEvents/Nodejs** directory when using the `node app.js` command.</span></span>

3. <span data-ttu-id="bb254-242">Dopo aver verificato il corretto aggiornamento del dashboard, arrestare la topologia usando CTRL+C.</span><span class="sxs-lookup"><span data-stu-id="bb254-242">After verifying that the dashboard updates, stop the topology using Ctrl+C.</span></span> <span data-ttu-id="bb254-243">È possibile usare CTRL+C anche per arrestare il server Web locale.</span><span class="sxs-lookup"><span data-stu-id="bb254-243">You can use Ctrl+C to stop the local web server also.</span></span>

## <a name="create-a-storm-and-hbase-cluster"></a><span data-ttu-id="bb254-244">Creare un cluster Storm e HBase</span><span class="sxs-lookup"><span data-stu-id="bb254-244">Create a Storm and HBase cluster</span></span>

<span data-ttu-id="bb254-245">Per i passaggi in questa sezione, usare un [modello di Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) per creare una rete virtuale di Azure e un cluster Storm e HBase nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="bb254-245">The steps in this section use an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) to create an Azure Virtual Network and a Storm and HBase cluster on the virtual network.</span></span> <span data-ttu-id="bb254-246">Il modello crea anche un'app Web di Azure e consente di distribuire una copia del dashboard al suo interno.</span><span class="sxs-lookup"><span data-stu-id="bb254-246">The template also creates an Azure Web App and deploys a copy of the dashboard into it.</span></span>

> [!NOTE]
> <span data-ttu-id="bb254-247">Viene usata una rete virtuale in modo che la topologia in esecuzione nel cluster Storm possa comunicare direttamente con il cluster HBase tramite l'API Java HBase.</span><span class="sxs-lookup"><span data-stu-id="bb254-247">A virtual network is used so that the topology running on the Storm cluster can directly communicate with the HBase cluster using the HBase Java API.</span></span>

<span data-ttu-id="bb254-248">Il modello di Resource Manager usato in questo documento si trova in un contenitore BLOB pubblico all'indirizzo **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span><span class="sxs-lookup"><span data-stu-id="bb254-248">The Resource Manager template used in this document is located in a public blob container at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span></span>

1. <span data-ttu-id="bb254-249">Fare clic sul pulsante seguente per accedere ad Azure e aprire il modello di Resource Manager nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="bb254-249">Click the following button to sign in to Azure and open the Resource Manager template in the Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-storm-cluster-in-vnet-3.6.json" target="_blank"><img src="./media/hdinsight-storm-sensor-data-analysis/deploy-to-azure.png" alt="Deploy to Azure"></a>

2. <span data-ttu-id="bb254-250">Immettere i valori seguenti dalla sezione **Distribuzione personalizzata**:</span><span class="sxs-lookup"><span data-stu-id="bb254-250">From the **Custom deployment** section, enter the following values:</span></span>
   
    ![Parametri di HDInsight](./media/hdinsight-storm-sensor-data-analysis/parameters.png)
   
   * <span data-ttu-id="bb254-252">**Base Cluster Name** (Nome di base del cluster): questo valore viene usato come nome di base per i cluster Storm e HBase.</span><span class="sxs-lookup"><span data-stu-id="bb254-252">**Base Cluster Name**: This value is used as the base name for the Storm and HBase clusters.</span></span> <span data-ttu-id="bb254-253">Ad esempio, se si immette **abc** verranno creati un cluster Storm denominato **storm-abc** e un cluster HBase denominato **hbase-abc**.</span><span class="sxs-lookup"><span data-stu-id="bb254-253">For example, entering **abc** creates a Storm cluster named **storm-abc** and an HBase cluster named **hbase-abc**.</span></span>
   * <span data-ttu-id="bb254-254">**Cluster Login User Name** (Nome utente di accesso del cluster): il nome utente amministratore per i cluster Storm e HBase.</span><span class="sxs-lookup"><span data-stu-id="bb254-254">**Cluster Login User Name**: The admin user name for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="bb254-255">**Password dell'account di accesso del cluster**: la password amministratore per i cluster Storm e HBase.</span><span class="sxs-lookup"><span data-stu-id="bb254-255">**Cluster Login Password**: The admin user password for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="bb254-256">**Nome utente SSH**: l'utente SSH da creare per i cluster Storm e HBase.</span><span class="sxs-lookup"><span data-stu-id="bb254-256">**SSH User Name**: The SSH user to create for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="bb254-257">**Password SSH**: la password dell'utente SSH per i cluster Storm e HBase.</span><span class="sxs-lookup"><span data-stu-id="bb254-257">**SSH Password**: The password for the SSH user for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="bb254-258">**Location** (Località): area in cui vengono creati i cluster.</span><span class="sxs-lookup"><span data-stu-id="bb254-258">**Location**: The region that the clusters are created in.</span></span>
     
     <span data-ttu-id="bb254-259">Fare clic su **OK** per salvare i parametri.</span><span class="sxs-lookup"><span data-stu-id="bb254-259">Click **OK** to save the parameters.</span></span>

3. <span data-ttu-id="bb254-260">Usare la sezione **Generale** per creare un gruppo di risorse o selezionarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="bb254-260">Use the **Basics** section to create a resource group or select an existing one.</span></span>
4. <span data-ttu-id="bb254-261">Nel menu a discesa **Località del gruppo di risorse** selezionare la stessa località selezionata per il parametro **Località** nella sezione **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="bb254-261">In the **Resource group location** dropdown menu, select the same location as you selected for the **Location** parameter in the **Settings** section.</span></span>
5. <span data-ttu-id="bb254-262">Leggere le condizioni, quindi selezionare **Accetto le condizioni riportate sopra**.</span><span class="sxs-lookup"><span data-stu-id="bb254-262">Read the terms and conditions, and then select **I agree to the terms and conditions stated above**.</span></span>
6. <span data-ttu-id="bb254-263">Selezionare infine **Aggiungi al dashboard** e quindi **Acquista**.</span><span class="sxs-lookup"><span data-stu-id="bb254-263">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="bb254-264">La creazione dei cluster richiede circa 20 minuti.</span><span class="sxs-lookup"><span data-stu-id="bb254-264">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="bb254-265">Dopo avere creato le risorse, vengono visualizzate le informazioni sul gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="bb254-265">Once the resources have been created, information about the resource group is displayed.</span></span>

![Gruppo di risorse per la rete virtuale e i cluster](./media/hdinsight-storm-sensor-data-analysis/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="bb254-267">Si noti che i nomi dei cluster HDInsight sono **storm-BASENAME** e **hbase-BASENAME**, dove BASENAME è il nome specificato per il modello.</span><span class="sxs-lookup"><span data-stu-id="bb254-267">Notice that the names of the HDInsight clusters are **storm-BASENAME** and **hbase-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="bb254-268">Questi nomi verranno usati in un passaggio successivo per la connessione ai cluster.</span><span class="sxs-lookup"><span data-stu-id="bb254-268">You use these names in a later step when connecting to the clusters.</span></span> <span data-ttu-id="bb254-269">Si noti inoltre che il nome del sito dashboard è **basename-dashboard**.</span><span class="sxs-lookup"><span data-stu-id="bb254-269">Also note that the name of the dashboard site is **basename-dashboard**.</span></span> <span data-ttu-id="bb254-270">Questo valore viene usato più avanti in questo documento.</span><span class="sxs-lookup"><span data-stu-id="bb254-270">This value is used later in this document.</span></span>

## <a name="configure-the-dashboard-bolt"></a><span data-ttu-id="bb254-271">Configurare il bolt Dashboard</span><span class="sxs-lookup"><span data-stu-id="bb254-271">Configure the Dashboard bolt</span></span>

<span data-ttu-id="bb254-272">Per inviare dati al dashboard distribuito come app Web, è necessario modificare la riga seguente nel file `dev.properties`:</span><span class="sxs-lookup"><span data-stu-id="bb254-272">To send data to the dashboard deployed as a web app, you must modify the following line in the `dev.properties`file:</span></span>

```yaml
dashboard.uri: http://localhost:3000
```

<span data-ttu-id="bb254-273">Modificare `http://localhost:3000` in `http://BASENAME-dashboard.azurewebsites.net` e salvare il file.</span><span class="sxs-lookup"><span data-stu-id="bb254-273">Change `http://localhost:3000` to `http://BASENAME-dashboard.azurewebsites.net` and save the file.</span></span> <span data-ttu-id="bb254-274">Sostituire **BASENAME** con il nome di base fornito nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="bb254-274">Replace **BASENAME** with the base name you provided in the previous step.</span></span> <span data-ttu-id="bb254-275">È anche possibile usare il gruppo di risorse creato in precedenza per selezionare il dashboard e visualizzare l'URL.</span><span class="sxs-lookup"><span data-stu-id="bb254-275">You can also use the resource group created previously to select the dashboard and view the URL.</span></span>

## <a name="create-the-hbase-table"></a><span data-ttu-id="bb254-276">Creare una tabella HBase</span><span class="sxs-lookup"><span data-stu-id="bb254-276">Create the HBase table</span></span>

<span data-ttu-id="bb254-277">Per archiviare i dati in HBase, è necessario creare prima di tutto una tabella.</span><span class="sxs-lookup"><span data-stu-id="bb254-277">To store data in HBase, we must first create a table.</span></span> <span data-ttu-id="bb254-278">Creare prima le risorse in cui Storm dovrà scrivere, perché creare risorse dall'interno di una topologia Storm può comportare la creazione di più istanze che tentano di creare la stessa risorsa.</span><span class="sxs-lookup"><span data-stu-id="bb254-278">Pre-create resources that Storm needs to write to, as trying to create resources from inside a Storm topology can result in multiple instances trying to create the same resource.</span></span> <span data-ttu-id="bb254-279">Creare le risorse all'esterno della topologia e usare Storm per operazioni di lettura/scrittura e analisi.</span><span class="sxs-lookup"><span data-stu-id="bb254-279">Create the resources outside the topology and use Storm for reading/writing and analytics.</span></span>

1. <span data-ttu-id="bb254-280">Usare SSH per connettersi al cluster HBase usando il nome utente e la password SSH forniti nel modello durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="bb254-280">Use SSH to connect to the HBase cluster using the SSH user and password you supplied to the template during cluster creation.</span></span> <span data-ttu-id="bb254-281">Ad esempio, se la connessione viene stabilita tramite il comando `ssh` , usare la sintassi seguente:</span><span class="sxs-lookup"><span data-stu-id="bb254-281">For example, if connecting using the `ssh` command, you would use the following syntax:</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```
   
    <span data-ttu-id="bb254-282">Sostituire `sshuser` con il nome utente SSH specificato durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="bb254-282">Replace `sshuser` with the SSH user name you provided when creating the cluster.</span></span> <span data-ttu-id="bb254-283">Sostituire `clustername` con il nome del cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="bb254-283">Replace `clustername` with the HBase cluster name.</span></span>

2. <span data-ttu-id="bb254-284">Dalla sessione SSH avviare la shell di HBase.</span><span class="sxs-lookup"><span data-stu-id="bb254-284">From the SSH session, start the HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="bb254-285">Dopo il caricamento della shell, verrà visualizzato un prompt `hbase(main):001:0>`.</span><span class="sxs-lookup"><span data-stu-id="bb254-285">Once the shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="bb254-286">Dalla shell HBase immettere il comando seguente per creare una tabella in cui archiviare i dati del sensore:</span><span class="sxs-lookup"><span data-stu-id="bb254-286">From the HBase shell, enter the following command to create a table to store the sensor data:</span></span>
   
    ```hbase
    create 'SensorData', 'cf'
    ```

4. <span data-ttu-id="bb254-287">Verificare la corretta creazione della tabella con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="bb254-287">Verify that the table has been created by using the following command:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="bb254-288">Tale comando restituisce informazioni simili alle seguenti, che indicano che nella tabella ci sono 0 righe disponibili.</span><span class="sxs-lookup"><span data-stu-id="bb254-288">This returns information similar to the following example, indicating that there are 0 rows in the table.</span></span>
   
        ROW                   COLUMN+CELL                                       0 row(s) in 0.1900 seconds

5. <span data-ttu-id="bb254-289">Immettere `exit` per uscire dalla shell HBase:</span><span class="sxs-lookup"><span data-stu-id="bb254-289">Enter `exit` to exit the HBase shell:</span></span>

## <a name="configure-the-hbase-bolt"></a><span data-ttu-id="bb254-290">Configurare il bolt HBase</span><span class="sxs-lookup"><span data-stu-id="bb254-290">Configure the HBase bolt</span></span>

<span data-ttu-id="bb254-291">Per scrivere in HBase dal cluster Storm, è necessario fornire al bolt HBase i dettagli di configurazione del cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="bb254-291">To write to HBase from the Storm cluster, you must provide the HBase bolt with the configuration details of your HBase cluster.</span></span>

1. <span data-ttu-id="bb254-292">Usare uno degli esempi seguenti per recuperare il quorum di Zookeeper per il cluster HBase:</span><span class="sxs-lookup"><span data-stu-id="bb254-292">Use one of the following examples to retrieve the Zookeeper quorum for your HBase cluster:</span></span>

    ```bash
    CLUSTERNAME='your_HDInsight_cluster_name'
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HBASE/components/HBASE_MASTER" | jq '.metrics.hbase.master.ZookeeperQuorum'
    ```

    > [!NOTE]
    > <span data-ttu-id="bb254-293">Sostituire `your_HDInsight_cluster_name` con il nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bb254-293">Replace `your_HDInsight_cluster_name` with the name of your HDInsight cluster.</span></span> <span data-ttu-id="bb254-294">Per altre informazioni sull'installazione dell'utilità `jq`, vedere [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="bb254-294">For more information on installing the `jq` utility, see [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span></span>
    >
    > <span data-ttu-id="bb254-295">Quando richiesto, immettere la password per l'account di accesso amministratore di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bb254-295">When prompted, enter the password for the HDInsight admin login.</span></span>

    ```powershell
    $clusterName = 'your_HDInsight_cluster_name`
    $creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HBASE/components/HBASE_MASTER" -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.metrics.hbase.master.ZookeeperQuorum
    ```

    > [!NOTE]
    > <span data-ttu-id="bb254-296">Sostituire 'your_HDInsight_cluster_name' con il nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bb254-296">Replace \`your_HDInsight_cluster_name with the name of your HDInsight cluster.</span></span> <span data-ttu-id="bb254-297">Quando richiesto, immettere la password per l'account di accesso amministratore di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bb254-297">When prompted, enter the password for the HDInsight admin login.</span></span>
    >
    > <span data-ttu-id="bb254-298">Questo esempio richiede Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bb254-298">This example requires Azure PowerShell.</span></span> <span data-ttu-id="bb254-299">Per altre informazioni sull'uso di Azure PowerShell, vedere [Getting started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6) (Introduzione ad Azure PowerShell)</span><span class="sxs-lookup"><span data-stu-id="bb254-299">For more information on using Azure PowerShell, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)</span></span>

    <span data-ttu-id="bb254-300">Le informazioni restituite da questi esempi sono simili al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="bb254-300">The information returned by these examples is similar to the following text:</span></span>

    `zk2-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk0-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk3-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181`

    <span data-ttu-id="bb254-301">Queste informazioni vengono usate da Storm per comunicare con il cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="bb254-301">This information is used by Storm to communicate with the HBase cluster.</span></span>

2. <span data-ttu-id="bb254-302">Modificare il file `dev.properties` e aggiungere le informazioni sul quorum di Zookeeper alla riga seguente:</span><span class="sxs-lookup"><span data-stu-id="bb254-302">Modify the `dev.properties` file and add the Zookeeper quorum information to the following line:</span></span>

    ```yaml
    hbase.zookeeper.quorum: your_hbase_quorum
    ```

## <a name="build-package-and-deploy-the-solution-to-hdinsight"></a><span data-ttu-id="bb254-303">Compilare la soluzione, creare il pacchetto e distribuirla in HDInsight</span><span class="sxs-lookup"><span data-stu-id="bb254-303">Build, package, and deploy the solution to HDInsight</span></span>

<span data-ttu-id="bb254-304">Nell'ambiente di sviluppo seguire questa procedura per distribuire la topologia Temperature nel cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="bb254-304">In your development environment, use the following steps to deploy the Storm topology to the storm cluster.</span></span>

1. <span data-ttu-id="bb254-305">Dalla directory `TemperatureMonitor` eseguire una nuova compilazione e creare un pacchetto JAR dal progetto usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="bb254-305">From the `TemperatureMonitor` directory, use the following command to perform a new build and create a JAR package from your project:</span></span>
   
        mvn clean package
   
    <span data-ttu-id="bb254-306">Questo comando crea un file denominato `TemperatureMonitor-1.0-SNAPSHOT.jar in the ` nella directory "target" del progetto.</span><span class="sxs-lookup"><span data-stu-id="bb254-306">This command creates a file named `TemperatureMonitor-1.0-SNAPSHOT.jar in the `target\` directory of your project.</span></span>

2. <span data-ttu-id="bb254-307">Usare scp per caricare i file `TemperatureMonitor-1.0-SNAPSHOT.jar` e `dev.properties` nel cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="bb254-307">Use scp to upload the `TemperatureMonitor-1.0-SNAPSHOT.jar` and `dev.properties` files to your Storm cluster.</span></span> <span data-ttu-id="bb254-308">Nell'esempio seguente sostituire `sshuser` con l'utente SSH specificato durante la creazione del cluster e `clustername` con il nome del cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="bb254-308">In the following example, replace `sshuser` with the SSH user you provided when creating the cluster, and `clustername` with the name of your Storm cluster.</span></span> <span data-ttu-id="bb254-309">Quando richiesto, immettere la password per l'utente SSH.</span><span class="sxs-lookup"><span data-stu-id="bb254-309">When prompted, enter the password for the SSH user.</span></span>
   
    ```bash
    scp target/TemperatureMonitor-1.0-SNAPSHOT.jar dev.properties sshuser@clustername-ssh.azurehdinsight.net:
    ```

   > [!NOTE]
   > <span data-ttu-id="bb254-310">Il caricamento dei file può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="bb254-310">It may take several minutes to upload the files.</span></span>

    <span data-ttu-id="bb254-311">Per altre informazioni sull'uso dei comandi `scp` e `ssh` con HDInsight, vedere [Usare SSH con HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="bb254-311">For more information on using the `scp` and `ssh` commands with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

3. <span data-ttu-id="bb254-312">Al termine del caricamento del file, connettersi al cluster Storm tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="bb254-312">Once the file has been uploaded, connect to the Storm cluster using SSH.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="bb254-313">Sostituire `sshuser` con il nome utente SSH.</span><span class="sxs-lookup"><span data-stu-id="bb254-313">Replace `sshuser` with the SSH user name.</span></span> <span data-ttu-id="bb254-314">Sostituire `clustername` con il nome del cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="bb254-314">Replace `clustername` with the Storm cluster name.</span></span>

4. <span data-ttu-id="bb254-315">Nella sessione SSH usare il comando seguente per avviare la topologia:</span><span class="sxs-lookup"><span data-stu-id="bb254-315">To start the topology, use the following command from the SSH session:</span></span>
   
    ```bash
    storm jar TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote --filter dev.properties -R /with-hbase.yaml
    ```

    * <span data-ttu-id="bb254-316">`--remote` invia la topologia al servizio Nimbus, che lo distribuisce ai nodi supervisore nel cluster.</span><span class="sxs-lookup"><span data-stu-id="bb254-316">`--remote` submits the topology to the Nimbus service, which distributes it to the supervisor nodes in the cluster.</span></span>
    * <span data-ttu-id="bb254-317">`--filter` usa il file `dev.properties` per immettere i parametri nella definizione della topologia.</span><span class="sxs-lookup"><span data-stu-id="bb254-317">`--filter` uses the `dev.properties` file to populate parameters in the topology definition.</span></span>
    * <span data-ttu-id="bb254-318">`-R /with-hbase.yaml` usa la topologia `with-hbase.yaml` inclusa nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bb254-318">`-R /with-hbase.yaml` uses the `with-hbase.yaml` topology included in the package.</span></span>

5. <span data-ttu-id="bb254-319">Dopo aver avviato la topologia, aprire un browser al sito Web pubblicato in Azure e quindi usare il comando `node app.js` per inviare dati all'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="bb254-319">After the topology has started, open a browser to the website you published on Azure, then use the `node app.js` command to send data to Event Hub.</span></span> <span data-ttu-id="bb254-320">Verrà visualizzato il dashboard Web aggiornato per mostrare le informazioni.</span><span class="sxs-lookup"><span data-stu-id="bb254-320">You should see the web dashboard update to display the information.</span></span>
   
    ![dashboard](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

## <a name="view-hbase-data"></a><span data-ttu-id="bb254-322">Visualizzare i dati di HBase</span><span class="sxs-lookup"><span data-stu-id="bb254-322">View HBase data</span></span>

<span data-ttu-id="bb254-323">Usare la procedura seguente per connettersi a HBase e verificare che i dati siano stati scritti nella tabella:</span><span class="sxs-lookup"><span data-stu-id="bb254-323">Use the following steps to connect to HBase and verify that the data has been written to the table:</span></span>

1. <span data-ttu-id="bb254-324">Usare SSH per connettersi al cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="bb254-324">Use SSH to connect to the HBase cluster.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="bb254-325">Sostituire `sshuser` con il nome utente SSH.</span><span class="sxs-lookup"><span data-stu-id="bb254-325">Replace `sshuser` with the SSH user name.</span></span> <span data-ttu-id="bb254-326">Sostituire `clustername` con il nome del cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="bb254-326">Replace `clustername` with the HBase cluster name.</span></span>

2. <span data-ttu-id="bb254-327">Dalla sessione SSH avviare la shell di HBase.</span><span class="sxs-lookup"><span data-stu-id="bb254-327">From the SSH session, start the HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="bb254-328">Dopo il caricamento della shell, verrà visualizzato un prompt `hbase(main):001:0>`.</span><span class="sxs-lookup"><span data-stu-id="bb254-328">Once the shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="bb254-329">Visualizzare le righe dalla tabella:</span><span class="sxs-lookup"><span data-stu-id="bb254-329">View rows from the table:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="bb254-330">Questo comando restituisce informazioni simili al testo seguente, che indicano che nella tabella sono presenti dati.</span><span class="sxs-lookup"><span data-stu-id="bb254-330">This command returns information similar to the following text, indicating that there is data in the table.</span></span>
   
        hbase(main):002:0> scan 'SensorData'
        ROW                             COLUMN+CELL
        \x00\x00\x00\x00               column=cf:temperature, timestamp=1467290788277, value=\x00\x00\x00\x04
        \x00\x00\x00\x00               column=cf:timestamp, timestamp=1467290788277, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x01               column=cf:temperature, timestamp=1467290788348, value=\x00\x00\x00M
        \x00\x00\x00\x01               column=cf:timestamp, timestamp=1467290788348, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x02               column=cf:temperature, timestamp=1467290788268, value=\x00\x00\x00R
        \x00\x00\x00\x02               column=cf:timestamp, timestamp=1467290788268, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x03               column=cf:temperature, timestamp=1467290788269, value=\x00\x00\x00#
        \x00\x00\x00\x03               column=cf:timestamp, timestamp=1467290788269, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x04               column=cf:temperature, timestamp=1467290788356, value=\x00\x00\x00>
        \x00\x00\x00\x04               column=cf:timestamp, timestamp=1467290788356, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x05               column=cf:temperature, timestamp=1467290788326, value=\x00\x00\x00\x0D
        \x00\x00\x00\x05               column=cf:timestamp, timestamp=1467290788326, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x06               column=cf:temperature, timestamp=1467290788253, value=\x00\x00\x009
        \x00\x00\x00\x06               column=cf:timestamp, timestamp=1467290788253, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x07               column=cf:temperature, timestamp=1467290788229, value=\x00\x00\x00\x12
        \x00\x00\x00\x07               column=cf:timestamp, timestamp=1467290788229, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x08               column=cf:temperature, timestamp=1467290788336, value=\x00\x00\x00\x16
        \x00\x00\x00\x08               column=cf:timestamp, timestamp=1467290788336, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x09               column=cf:temperature, timestamp=1467290788246, value=\x00\x00\x001
        \x00\x00\x00\x09               column=cf:timestamp, timestamp=1467290788246, value=2015-02-10T14:43.05.00320Z
        10 row(s) in 0.1800 seconds
   
   > [!NOTE]
   > <span data-ttu-id="bb254-331">Questa operazione di analisi restituisce un massimo di 10 righe dalla tabella.</span><span class="sxs-lookup"><span data-stu-id="bb254-331">This scan operation returns a maximum of 10 rows from the table.</span></span>

## <a name="delete-your-clusters"></a><span data-ttu-id="bb254-332">Eliminare i cluster</span><span class="sxs-lookup"><span data-stu-id="bb254-332">Delete your clusters</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="bb254-333">Per eliminare il cluster, la risorsa di archiviazione e l'app Web contemporaneamente, eliminare il gruppo di risorse che li contiene.</span><span class="sxs-lookup"><span data-stu-id="bb254-333">To delete the clusters, storage, and web app at one time, delete the resource group that contains them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb254-334">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bb254-334">Next steps</span></span>

<span data-ttu-id="bb254-335">Per altri esempi di topologie Storm con HDInsight, vedere [Topologie di esempio per Storm in HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="bb254-335">For more examples of Storm topologies with HDInsight, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md)</span></span>

<span data-ttu-id="bb254-336">Per altre informazioni su Apache Storm, visitare il sito Web [Apache Storm](https://storm.incubator.apache.org/) .</span><span class="sxs-lookup"><span data-stu-id="bb254-336">For more information about Apache Storm, see the [Apache Storm](https://storm.incubator.apache.org/) site.</span></span>

<span data-ttu-id="bb254-337">Per altre informazioni su HBase in HDInsight, vedere la [panoramica su HBase con HDInsight](hdinsight-hbase-overview.md)</span><span class="sxs-lookup"><span data-stu-id="bb254-337">For more information about HBase on HDInsight, see the [HBase with HDInsight Overview](hdinsight-hbase-overview.md).</span></span>

<span data-ttu-id="bb254-338">Per altre informazioni su Socket.io, visitare il sito Web [socket.io](http://socket.io/) .</span><span class="sxs-lookup"><span data-stu-id="bb254-338">For more information about Socket.io, see the [socket.io](http://socket.io/) site.</span></span>

<span data-ttu-id="bb254-339">Per altre informazioni su D3.js, vedere [D3.js - Data Driven Documents](http://d3js.org/).</span><span class="sxs-lookup"><span data-stu-id="bb254-339">For more information about D3.js, see [D3.js - Data Driven Documents](http://d3js.org/).</span></span>

<span data-ttu-id="bb254-340">Per altre informazioni sulla creazione di topologie in Java, vedere [Sviluppo di topologie basate su Java per Apache Storm in HDInsight](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="bb254-340">For information about creating topologies in Java, see [Develop Java topologies for Apache Storm on HDInsight](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="bb254-341">Per altre informazioni sulla creazione di topologie in .NET, vedere [Sviluppare topologie C# per Apache Storm in HDInsight tramite Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="bb254-341">For information about creating topologies in .NET, see [Develop C# topologies for Apache Storm on HDInsight using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

[azure-portal]: https://portal.azure.com
