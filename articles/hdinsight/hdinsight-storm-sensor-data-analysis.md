---
title: dati del sensore aaaAnalyze con Apache Storm e HBase | Documenti Microsoft
description: Informazioni su come tooconnect tooApache Storm con una rete virtuale. Utilizzare Storm con dati del sensore tooprocess HBase da un hub eventi e visualizzarla con D3.js.
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
ms.openlocfilehash: e54fe9ffc720b0089f90e302b24a9438bd43999a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-with-apache-storm-event-hub-and-hbase-in-hdinsight-hadoop"></a><span data-ttu-id="76be0-104">Analizzare i dati del sensore con Apache Storm, hub eventi e HBase in HDInsight (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="76be0-104">Analyze sensor data with Apache Storm, Event Hub, and HBase in HDInsight (Hadoop)</span></span>

<span data-ttu-id="76be0-105">Informazioni su come toouse Apache Storm HDInsight tooprocess dei dati del sensore di Hub di eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="76be0-105">Learn how toouse Apache Storm on HDInsight tooprocess sensor data from Azure Event Hub.</span></span> <span data-ttu-id="76be0-106">Hello dati vengono quindi archiviati in Apache HBase in HDInsight e visualizzato tramite D3.js.</span><span class="sxs-lookup"><span data-stu-id="76be0-106">hello data is then stored into Apache HBase on HDInsight, and visualized using D3.js.</span></span>

<span data-ttu-id="76be0-107">modello di gestione risorse di Azure Hello utilizzato in questo documento illustra come toocreate più risorse di Azure in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="76be0-107">hello Azure Resource Manager template used in this document demonstrates how toocreate multiple Azure resources in a resource group.</span></span> <span data-ttu-id="76be0-108">Hello modello consente di creare una rete virtuale di Azure, due cluster HDInsight (Storm e HBase) e un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="76be0-108">hello template creates an Azure Virtual Network, two HDInsight clusters (Storm and HBase) and an Azure Web App.</span></span> <span data-ttu-id="76be0-109">Un'implementazione di node.js di un dashboard web in tempo reale viene automaticamente distribuito toohello web app.</span><span class="sxs-lookup"><span data-stu-id="76be0-109">A node.js implementation of a real-time web dashboard is automatically deployed toohello web app.</span></span>

> [!NOTE]
> <span data-ttu-id="76be0-110">informazioni di Hello in questo documento e un esempio in questo documento richiedono HDInsight versione 3.6.</span><span class="sxs-lookup"><span data-stu-id="76be0-110">hello information in this document and example in this document require HDInsight version 3.6.</span></span>
>
> <span data-ttu-id="76be0-111">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="76be0-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="76be0-112">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="76be0-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76be0-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="76be0-113">Prerequisites</span></span>

* <span data-ttu-id="76be0-114">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="76be0-114">An Azure subscription.</span></span>
* <span data-ttu-id="76be0-115">[Node.js](http://nodejs.org/): dashboard web di hello toopreview utilizzate in ambiente di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="76be0-115">[Node.js](http://nodejs.org/): Used toopreview hello web dashboard locally on your development environment.</span></span>
* <span data-ttu-id="76be0-116">[Java e hello JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): utilizzata una topologia di Storm toodevelop hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-116">[Java and hello JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): Used toodevelop hello Storm topology.</span></span>
* <span data-ttu-id="76be0-117">[Maven](http://maven.apache.org/what-is-maven.html): progetto di hello toobuild e compilazione utilizzato.</span><span class="sxs-lookup"><span data-stu-id="76be0-117">[Maven](http://maven.apache.org/what-is-maven.html): Used toobuild and compile hello project.</span></span>
* <span data-ttu-id="76be0-118">[GIT](http://git-scm.com/): progetto hello toodownload utilizzato da GitHub.</span><span class="sxs-lookup"><span data-stu-id="76be0-118">[Git](http://git-scm.com/): Used toodownload hello project from GitHub.</span></span>
* <span data-ttu-id="76be0-119">Un **SSH** client: tooconnect toohello HDInsight basati su Linux cluster usati.</span><span class="sxs-lookup"><span data-stu-id="76be0-119">An **SSH** client: Used tooconnect toohello Linux-based HDInsight clusters.</span></span> <span data-ttu-id="76be0-120">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="76be0-120">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="76be0-121">Non è necessario un cluster HDInsight esistente.</span><span class="sxs-lookup"><span data-stu-id="76be0-121">You do not need an existing HDInsight cluster.</span></span> <span data-ttu-id="76be0-122">procedura di Hello in questo documento consente di creare hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="76be0-122">hello steps in this document create hello following resources:</span></span>
> 
> * <span data-ttu-id="76be0-123">Una rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="76be0-123">An Azure Virtual Network</span></span>
> * <span data-ttu-id="76be0-124">Un cluster Storm in HDInsight (basato su Linux con due nodi del ruolo di lavoro)</span><span class="sxs-lookup"><span data-stu-id="76be0-124">A Storm on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="76be0-125">Un cluster HBase in HDInsight (basato su Linux con due nodi del ruolo di lavoro)</span><span class="sxs-lookup"><span data-stu-id="76be0-125">An HBase on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="76be0-126">Un'App Web di Azure che ospita dashboard web hello</span><span class="sxs-lookup"><span data-stu-id="76be0-126">An Azure Web App that hosts hello web dashboard</span></span>

## <a name="architecture"></a><span data-ttu-id="76be0-127">Architettura</span><span class="sxs-lookup"><span data-stu-id="76be0-127">Architecture</span></span>

![diagramma dell'architettura](./media/hdinsight-storm-sensor-data-analysis/devicesarchitecture.png)

<span data-ttu-id="76be0-129">Questo esempio è costituito da hello seguenti componenti:</span><span class="sxs-lookup"><span data-stu-id="76be0-129">This example consists of hello following components:</span></span>

* <span data-ttu-id="76be0-130">**Hub eventi di Azure**: include i dati raccolti dai sensori.</span><span class="sxs-lookup"><span data-stu-id="76be0-130">**Azure Event Hubs**: Contains data that is collected from sensors.</span></span>
* <span data-ttu-id="76be0-131">**Storm in HDInsight**: assicura l'elaborazione in tempo reale dei dati provenienti dall'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="76be0-131">**Storm on HDInsight**: Provides real-time processing of data from Event Hub.</span></span>
* <span data-ttu-id="76be0-132">**HBase in HDInsight**: fornisce un archivio dati NoSQL persistente per i dati, dopo l'elaborazione tramite Storm.</span><span class="sxs-lookup"><span data-stu-id="76be0-132">**HBase on HDInsight**: Provides a persistent NoSQL data store for data after it has been processed by Storm.</span></span>
* <span data-ttu-id="76be0-133">**Servizio di rete virtuale Azure**: consente di proteggere le comunicazioni tra hello Storm in HDInsight e HBase nei cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="76be0-133">**Azure Virtual Network service**: Enables secure communications between hello Storm on HDInsight and HBase on HDInsight clusters.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="76be0-134">Una rete virtuale è obbligatoria quando si utilizza l'API client di HBase Java hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-134">A virtual network is required when using hello Java HBase client API.</span></span> <span data-ttu-id="76be0-135">Non è esposta tramite il gateway pubblica hello per cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="76be0-135">It is not exposed over hello public gateway for HBase clusters.</span></span> <span data-ttu-id="76be0-136">Cluster HBase l'installazione e Storm nella stessa rete virtuale consente di hello hello cluster Storm (o qualsiasi altro sistema sulla rete virtuale hello) toodirectly accedere tramite l'API del client.</span><span class="sxs-lookup"><span data-stu-id="76be0-136">Installing HBase and Storm clusters into hello same virtual network allows hello Storm cluster (or any other system on hello virtual network) toodirectly access HBase using client API.</span></span>

* <span data-ttu-id="76be0-137">**Sito Web del dashboard**: dashboard di esempio che rappresenta graficamente i dati in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="76be0-137">**Dashboard website**: An example dashboard that charts data in real time.</span></span>
  
  * <span data-ttu-id="76be0-138">sito Web di Hello viene implementato in Node.js.</span><span class="sxs-lookup"><span data-stu-id="76be0-138">hello website is implemented in Node.js.</span></span>
  * <span data-ttu-id="76be0-139">[Socket.IO](http://socket.io/) utilizzato per la comunicazione in tempo reale tra topologia Storm hello e hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-139">[Socket.io](http://socket.io/) is used for real-time communication between hello Storm topology and hello website.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="76be0-140">L'uso di Socket.io per la comunicazione è un dettaglio di implementazione.</span><span class="sxs-lookup"><span data-stu-id="76be0-140">Using Socket.io for communication is an implementation detail.</span></span> <span data-ttu-id="76be0-141">È possibile usare qualsiasi framework di comunicazione, ad esempio WebSocket o SignalR non elaborato.</span><span class="sxs-lookup"><span data-stu-id="76be0-141">You can use any communications framework, such as raw WebSockets or SignalR.</span></span>

  * <span data-ttu-id="76be0-142">[D3.js](http://d3js.org/) toograph utilizzati hello dati del sito Web toohello inviato.</span><span class="sxs-lookup"><span data-stu-id="76be0-142">[D3.js](http://d3js.org/) is used toograph hello data that is sent toohello website.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="76be0-143">Due cluster sono necessari, perché non esiste alcun cluster di HDInsight un metodo supportato toocreate Storm sia HBase.</span><span class="sxs-lookup"><span data-stu-id="76be0-143">Two clusters are required, as there is no supported method toocreate one HDInsight cluster for both Storm and HBase.</span></span>

<span data-ttu-id="76be0-144">Hello topologia legge i dati provenienti dall'Hub eventi tramite hello [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) classe e scrive i dati in HBase tramite hello [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) classe.</span><span class="sxs-lookup"><span data-stu-id="76be0-144">hello topology reads data from Event Hub by using hello [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) class, and writes data into HBase using hello [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) class.</span></span> <span data-ttu-id="76be0-145">La comunicazione con il sito hello viene eseguita utilizzando [socket.io client.java](https://github.com/nkzawa/socket.io-client.java).</span><span class="sxs-lookup"><span data-stu-id="76be0-145">Communication with hello website is accomplished by using [socket.io-client.java](https://github.com/nkzawa/socket.io-client.java).</span></span>

<span data-ttu-id="76be0-146">Hello seguente diagramma illustra il layout di hello della topologia hello:</span><span class="sxs-lookup"><span data-stu-id="76be0-146">hello following diagram explains hello layout of hello topology:</span></span>

![diagramma della topologia](./media/hdinsight-storm-sensor-data-analysis/sensoranalysis.png)

> [!NOTE]
> <span data-ttu-id="76be0-148">Questo diagramma è una visualizzazione semplificata della topologia hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-148">This diagram is a simplified view of hello topology.</span></span> <span data-ttu-id="76be0-149">Per ogni partizione dell'hub eventi viene creata un'istanza di ogni componente.</span><span class="sxs-lookup"><span data-stu-id="76be0-149">An instance of each component is created for each partition in your Event Hub.</span></span> <span data-ttu-id="76be0-150">Queste istanze vengono distribuite tra i nodi nel cluster hello hello e dati viene instradati tra di essi, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="76be0-150">These instances are distributed across hello nodes in hello cluster, and data is routed between them as follows:</span></span>
> 
> * <span data-ttu-id="76be0-151">I dati dal parser di toohello beccuccio hello sono con carico bilanciato.</span><span class="sxs-lookup"><span data-stu-id="76be0-151">Data from hello spout toohello parser is load balanced.</span></span>
> * <span data-ttu-id="76be0-152">Dati da hello parser toohello Dashboard e HBase vengono raggruppati per ID dispositivo, in modo che i messaggi da hello stesso dispositivo sempre flusso toohello stesso componente.</span><span class="sxs-lookup"><span data-stu-id="76be0-152">Data from hello parser toohello Dashboard and HBase is grouped by Device ID, so that messages from hello same device always flow toohello same component.</span></span>

### <a name="topology-components"></a><span data-ttu-id="76be0-153">Componenti della topologia</span><span class="sxs-lookup"><span data-stu-id="76be0-153">Topology components</span></span>

* <span data-ttu-id="76be0-154">**Hub di eventi Spout**: beccuccio hello è fornito come parte della versione di Apache Storm 0.10.0 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="76be0-154">**Event Hub Spout**: hello spout is provided as part of Apache Storm version 0.10.0 and higher.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="76be0-155">beccuccio Hub eventi Hello utilizzato in questo esempio richiede un elevato numero di versione di cluster HDInsight 3.5 o 3.6.</span><span class="sxs-lookup"><span data-stu-id="76be0-155">hello Event Hub spout used in this example requires a Storm on HDInsight cluster version 3.5 or 3.6.</span></span>

* <span data-ttu-id="76be0-156">**ParserBolt.java**: dati hello emesso dal beccuccio hello JSON non elaborati e in alcuni casi più di un evento viene generato alla volta.</span><span class="sxs-lookup"><span data-stu-id="76be0-156">**ParserBolt.java**: hello data that is emitted by hello spout is raw JSON, and occasionally more than one event is emitted at a time.</span></span> <span data-ttu-id="76be0-157">Questo fulmine legge dati hello generati da hello spout e analizza il messaggio JSON hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-157">This bolt reads hello data emitted by hello spout and parses hello JSON message.</span></span> <span data-ttu-id="76be0-158">fulmine Hello genera quindi i dati di hello come una tupla che contiene più campi.</span><span class="sxs-lookup"><span data-stu-id="76be0-158">hello bolt then emits hello data as a tuple that contains multiple fields.</span></span>
* <span data-ttu-id="76be0-159">**DashboardBolt.java**: questo componente viene illustrato come toouse hello Socket.io di libreria client per i dati toosend Java nel dashboard in tempo reale toohello web.</span><span class="sxs-lookup"><span data-stu-id="76be0-159">**DashboardBolt.java**: This component demonstrates how toouse hello Socket.io client library for Java toosend data in real time toohello web dashboard.</span></span>
* <span data-ttu-id="76be0-160">**No-hbase.yaml**: hello definizione della topologia utilizzata durante l'esecuzione in modalità locale.</span><span class="sxs-lookup"><span data-stu-id="76be0-160">**no-hbase.yaml**: hello topology definition used when running in local mode.</span></span> <span data-ttu-id="76be0-161">Non usa componenti HBase.</span><span class="sxs-lookup"><span data-stu-id="76be0-161">It does not use HBase components.</span></span>
* <span data-ttu-id="76be0-162">**con hbase.yaml**: hello usato quando si esegue la topologia hello in cluster hello definizione della topologia.</span><span class="sxs-lookup"><span data-stu-id="76be0-162">**with-hbase.yaml**: hello topology definition used when running hello topology on hello cluster.</span></span> <span data-ttu-id="76be0-163">Usa componenti HBase.</span><span class="sxs-lookup"><span data-stu-id="76be0-163">It does use HBase components.</span></span>
* <span data-ttu-id="76be0-164">**DEV.Properties**: hello informazioni di configurazione per beccuccio Hub eventi hello fulmine HBase e componenti del dashboard.</span><span class="sxs-lookup"><span data-stu-id="76be0-164">**dev.properties**: hello configuration information for hello Event Hub spout, HBase bolt, and dashboard components.</span></span>

## <a name="prepare-your-environment"></a><span data-ttu-id="76be0-165">Preparare l'ambiente</span><span class="sxs-lookup"><span data-stu-id="76be0-165">Prepare your environment</span></span>

<span data-ttu-id="76be0-166">Prima di usare questo esempio, è necessario creare un Hub di eventi di Azure, la topologia di Storm hello letta.</span><span class="sxs-lookup"><span data-stu-id="76be0-166">Before you use this example, you must create an Azure Event Hub, which hello Storm topology reads from.</span></span>

### <a name="configure-event-hub"></a><span data-ttu-id="76be0-167">Configurare l'hub eventi</span><span class="sxs-lookup"><span data-stu-id="76be0-167">Configure Event Hub</span></span>

<span data-ttu-id="76be0-168">Hub eventi è l'origine dati hello per questo esempio.</span><span class="sxs-lookup"><span data-stu-id="76be0-168">Event Hub is hello data source for this example.</span></span> <span data-ttu-id="76be0-169">Utilizzare hello seguendo i passaggi toocreate un Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="76be0-169">Use hello following steps toocreate an Event Hub.</span></span>

1. <span data-ttu-id="76be0-170">Da hello [portale di Azure](https://portal.azure.com)selezionare **+ nuovo** -> **Internet of Things** -> **hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="76be0-170">From hello [Azure portal](https://portal.azure.com), select **+ New** -> **Internet of Things** -> **Event Hubs**.</span></span>
2. <span data-ttu-id="76be0-171">In hello **creare Namespace** seguire hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="76be0-171">In hello **Create Namespace** section, perform hello following tasks:</span></span>
   
   1. <span data-ttu-id="76be0-172">Immettere un **nome** per spazio dei nomi hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-172">Enter a **Name** for hello namespace.</span></span>
   2. <span data-ttu-id="76be0-173">Selezione di un piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="76be0-173">Select a pricing tier.</span></span> <span data-ttu-id="76be0-174">**Basic** è sufficiente per questo esempio.</span><span class="sxs-lookup"><span data-stu-id="76be0-174">**Basic** is sufficient for this example.</span></span>
   3. <span data-ttu-id="76be0-175">Seleziona hello Azure **sottoscrizione** toouse.</span><span class="sxs-lookup"><span data-stu-id="76be0-175">Select hello Azure **Subscription** toouse.</span></span>
   4. <span data-ttu-id="76be0-176">Selezionare un gruppo di risorse esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="76be0-176">Either select an existing resource group or create a new one.</span></span>
   5. <span data-ttu-id="76be0-177">Seleziona hello **percorso** per hello Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="76be0-177">Select hello **Location** for hello Event Hub.</span></span>
   6. <span data-ttu-id="76be0-178">Selezionare **Pin toodashboard**, quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="76be0-178">Select **Pin toodashboard**, and then click **Create**.</span></span>

3. <span data-ttu-id="76be0-179">Al termine del processo di creazione di hello, hello informazioni hub eventi per lo spazio dei nomi viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="76be0-179">When hello creation process completes, hello Event Hubs information for your namespace is displayed.</span></span> <span data-ttu-id="76be0-180">Da qui, scegliere **+ Aggiungi hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="76be0-180">From here, select **+ Add Event Hub**.</span></span> <span data-ttu-id="76be0-181">In hello **creare Hub eventi** sezione, immettere un nome di **sensordata**, quindi selezionare **crea**.</span><span class="sxs-lookup"><span data-stu-id="76be0-181">In hello **Create Event Hub** section, enter a name of **sensordata**, and then select **Create**.</span></span> <span data-ttu-id="76be0-182">Lasciare hello altri campi valori predefiniti di hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-182">Leave hello other fields at hello default values.</span></span>
4. <span data-ttu-id="76be0-183">Dall'hub di eventi hello visualizzare dello spazio dei nomi, seleziona **hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="76be0-183">From hello Event Hubs view for your namespace, select **Event Hubs**.</span></span> <span data-ttu-id="76be0-184">Seleziona hello **sensordata** voce.</span><span class="sxs-lookup"><span data-stu-id="76be0-184">Select hello **sensordata** entry.</span></span>
5. <span data-ttu-id="76be0-185">Hello sensordata Hub eventi, selezionare **criteri di accesso condiviso**.</span><span class="sxs-lookup"><span data-stu-id="76be0-185">From hello sensordata Event Hub, select **Shared access policies**.</span></span> <span data-ttu-id="76be0-186">Hello utilizzare **+ Aggiungi** hello tooadd collegamento seguenti criteri:</span><span class="sxs-lookup"><span data-stu-id="76be0-186">Use hello **+ Add** link tooadd hello following policies:</span></span>

    | <span data-ttu-id="76be0-187">Nome criterio</span><span class="sxs-lookup"><span data-stu-id="76be0-187">Policy name</span></span> | <span data-ttu-id="76be0-188">Claims</span><span class="sxs-lookup"><span data-stu-id="76be0-188">Claims</span></span> |
    | ----- | ----- |
    | <span data-ttu-id="76be0-189">devices</span><span class="sxs-lookup"><span data-stu-id="76be0-189">devices</span></span> | <span data-ttu-id="76be0-190">Invio</span><span class="sxs-lookup"><span data-stu-id="76be0-190">Send</span></span> |
    | <span data-ttu-id="76be0-191">storm</span><span class="sxs-lookup"><span data-stu-id="76be0-191">storm</span></span> | <span data-ttu-id="76be0-192">Attesa</span><span class="sxs-lookup"><span data-stu-id="76be0-192">Listen</span></span> |

1. <span data-ttu-id="76be0-193">Selezionare entrambi i criteri e prendere nota di hello **chiave primaria** valore.</span><span class="sxs-lookup"><span data-stu-id="76be0-193">Select both policies and make a note of hello **PRIMARY KEY** value.</span></span> <span data-ttu-id="76be0-194">È necessario il valore di hello per entrambi i criteri in passaggi futuri.</span><span class="sxs-lookup"><span data-stu-id="76be0-194">You need hello value for both policies in future steps.</span></span>

## <a name="download-and-configure-hello-project"></a><span data-ttu-id="76be0-195">Scaricare e configurare il progetto hello</span><span class="sxs-lookup"><span data-stu-id="76be0-195">Download and configure hello project</span></span>

<span data-ttu-id="76be0-196">Utilizzare hello seguente progetto hello toodownload da GitHub.</span><span class="sxs-lookup"><span data-stu-id="76be0-196">Use hello following toodownload hello project from GitHub.</span></span>

    git clone https://github.com/Blackmist/hdinsight-eventhub-example

<span data-ttu-id="76be0-197">Al termine del comando di hello, è necessario hello seguente struttura di directory:</span><span class="sxs-lookup"><span data-stu-id="76be0-197">After hello command completes, you have hello following directory structure:</span></span>

    hdinsight-eventhub-example/
        TemperatureMonitor/ - this contains hello topology
            resources/
                log4j2.xml - set logging toominimal.
                no-hbase.yaml - topology definition without hbase components.
                with-hbase.yaml - topology definition with hbase components.
            src/main/java/com/microsoft/examples/bolts/
                ParserBolt.java - parses JSON data into tuples
                DashboardBolt.java - sends data over Socket.IO toohello web dashboard.
        dashboard/nodejs/ - this is hello node.js web dashboard.
        SendEvents/ - utilities toosend fake sensor data.

> [!NOTE]
> <span data-ttu-id="76be0-198">Questo documento non va nei dettagli toofull di codice hello inclusi in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="76be0-198">This document does not go in toofull details of hello code included in this example.</span></span> <span data-ttu-id="76be0-199">Tuttavia, il codice hello è completamente impostata come commento.</span><span class="sxs-lookup"><span data-stu-id="76be0-199">However, hello code is fully commented.</span></span>

<span data-ttu-id="76be0-200">tooconfigure hello progetto tooread dall'Hub di eventi, aprire hello `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` file e aggiungere il toohello informazioni Hub eventi seguenti righe:</span><span class="sxs-lookup"><span data-stu-id="76be0-200">tooconfigure hello project tooread from Event Hub, open hello `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` file and add your Event Hub information toohello following lines:</span></span>

```bash
eventhub.read.policy.name: your_read_policy_name
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: your_event_hub_name
eventhub.partitions: 2
```

## <a name="compile-and-test-locally"></a><span data-ttu-id="76be0-201">Compilare ed eseguire il test in locale</span><span class="sxs-lookup"><span data-stu-id="76be0-201">Compile and test locally</span></span>

> [!IMPORTANT]
> <span data-ttu-id="76be0-202">Utilizzando la topologia hello locale richiede un ambiente di sviluppo Storm funzionante.</span><span class="sxs-lookup"><span data-stu-id="76be0-202">Using hello topology locally requires a working Storm development environment.</span></span> <span data-ttu-id="76be0-203">Per altre informazioni, vedere [Setting up a development environment](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) (Impostazione di un ambiente di sviluppo) in Apache.org.</span><span class="sxs-lookup"><span data-stu-id="76be0-203">For more information, see [Setting up a Storm development environment](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) at Apache.org.</span></span>

> [!WARNING]
> <span data-ttu-id="76be0-204">Se si utilizza un ambiente di sviluppo di Windows, si potrebbe ricevere un `java.io.IOException` quando si esegue la topologia hello in locale.</span><span class="sxs-lookup"><span data-stu-id="76be0-204">If you are using a Windows development environment, you may receive a `java.io.IOException` when running hello topology locally.</span></span> <span data-ttu-id="76be0-205">In questo caso, spostare sulla topologia di hello toorunning in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="76be0-205">If so, move on toorunning hello topology on HDInsight.</span></span>

<span data-ttu-id="76be0-206">Prima di testare, è necessario avviare l'output di hello dashboard tooview hello della topologia hello e generare dati toostore in Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="76be0-206">Before testing, you must start hello dashboard tooview hello output of hello topology and generate data toostore in Event Hub.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="76be0-207">componente di HBase Hello di questa topologia non è attivo durante il test in locale.</span><span class="sxs-lookup"><span data-stu-id="76be0-207">hello HBase component of this topology is not active when testing locally.</span></span> <span data-ttu-id="76be0-208">Hello API Java per cluster HBase hello non è accessibile dall'esterno hello rete virtuale di Azure che contiene il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-208">hello Java API for hello HBase cluster cannot be accessed from outside hello Azure Virtual Network that contains hello clusters.</span></span>

### <a name="start-hello-web-application"></a><span data-ttu-id="76be0-209">Avviare l'applicazione web hello</span><span class="sxs-lookup"><span data-stu-id="76be0-209">Start hello web application</span></span>

1. <span data-ttu-id="76be0-210">Aprire un prompt dei comandi e passare alla directory troppo`hdinsight-eventhub-example/dashboard`.</span><span class="sxs-lookup"><span data-stu-id="76be0-210">Open a command prompt and change directories too`hdinsight-eventhub-example/dashboard`.</span></span> <span data-ttu-id="76be0-211">Utilizzare hello dipendenze hello tooinstall di comando necessari per un'applicazione hello web seguente:</span><span class="sxs-lookup"><span data-stu-id="76be0-211">Use hello following command tooinstall hello dependencies needed by hello web application:</span></span>
   
    ```bash
    npm install
    ```

2. <span data-ttu-id="76be0-212">Utilizzare hello dopo l'applicazione web di comando toostart hello:</span><span class="sxs-lookup"><span data-stu-id="76be0-212">Use hello following command toostart hello web application:</span></span>
   
    ```bash
    node server.js
    ```
   
    <span data-ttu-id="76be0-213">Viene visualizzato un toohello simile messaggio seguente testo:</span><span class="sxs-lookup"><span data-stu-id="76be0-213">You see a message similar toohello following text:</span></span>
   
        Server listening at port 3000

3. <span data-ttu-id="76be0-214">Aprire un web browser e immettere `http://localhost:3000/` come indirizzo hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-214">Open a web browser and enter `http://localhost:3000/` as hello address.</span></span> <span data-ttu-id="76be0-215">Viene visualizzato un toohello simile pagina seguente immagine:</span><span class="sxs-lookup"><span data-stu-id="76be0-215">A page similar toohello following image is displayed:</span></span>
   
    ![dashboard Web](./media/hdinsight-storm-sensor-data-analysis/emptydashboard.png)
   
    <span data-ttu-id="76be0-217">Lasciare il prompt dei comandi aperto.</span><span class="sxs-lookup"><span data-stu-id="76be0-217">Leave this command prompt open.</span></span> <span data-ttu-id="76be0-218">Al termine del test, utilizzare Ctrl-C toostop hello web server.</span><span class="sxs-lookup"><span data-stu-id="76be0-218">After testing, use Ctrl-C toostop hello web server.</span></span>

### <a name="generate-data"></a><span data-ttu-id="76be0-219">Generare i dati</span><span class="sxs-lookup"><span data-stu-id="76be0-219">Generate data</span></span>

> [!NOTE]
> <span data-ttu-id="76be0-220">Hello passaggi in questa sezione utilizzano Node. js in modo che possono essere utilizzati su qualsiasi piattaforma.</span><span class="sxs-lookup"><span data-stu-id="76be0-220">hello steps in this section use Node.js so that they can be used on any platform.</span></span> <span data-ttu-id="76be0-221">Per altri esempi di linguaggio, vedere hello `SendEvents` directory.</span><span class="sxs-lookup"><span data-stu-id="76be0-221">For other language examples, see hello `SendEvents` directory.</span></span>

1. <span data-ttu-id="76be0-222">Aprire un nuovo prompt dei comandi, una shell o terminal e passare alla directory troppo`hdinsight-eventhub-example/SendEvents/nodejs`.</span><span class="sxs-lookup"><span data-stu-id="76be0-222">Open a new prompt, shell, or terminal, and change directories too`hdinsight-eventhub-example/SendEvents/nodejs`.</span></span> <span data-ttu-id="76be0-223">dipendenze di hello tooinstall necessarie per un'applicazione hello, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="76be0-223">tooinstall hello dependencies needed by hello application, use hello following command:</span></span>

    ```bash
    npm install
    ```

2. <span data-ttu-id="76be0-224">Aprire hello `app.js` file in un editor di testo e aggiungere hello informazioni Hub eventi è ottenuto in precedenza:</span><span class="sxs-lookup"><span data-stu-id="76be0-224">Open hello `app.js` file in a text editor and add hello Event Hub information you obtained earlier:</span></span>
   
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
   > <span data-ttu-id="76be0-225">Questo esempio si presuppone che si usa `sensordata` come nome hello dell'Hub di eventi.</span><span class="sxs-lookup"><span data-stu-id="76be0-225">This example assumes that you have used `sensordata` as hello name of your Event Hub.</span></span> <span data-ttu-id="76be0-226">E che `devices` come nome hello del criterio di hello un `Send` attestazione.</span><span class="sxs-lookup"><span data-stu-id="76be0-226">And that `devices` as hello name of hello policy that has a `Send` claim.</span></span>

3. <span data-ttu-id="76be0-227">Comando che segue di hello utilizzare tooinsert nuove voci in Hub eventi:</span><span class="sxs-lookup"><span data-stu-id="76be0-227">Use hello following command tooinsert new entries in Event Hub:</span></span>
   
    ```bash
    node app.js
    ```
   
    <span data-ttu-id="76be0-228">Viene visualizzato più righe di output che contengono dati hello inviati tooEvent Hub:</span><span class="sxs-lookup"><span data-stu-id="76be0-228">You see several lines of output that contain hello data sent tooEvent Hub:</span></span>
   
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

### <a name="build-and-start-hello-topology"></a><span data-ttu-id="76be0-229">Compilare e avviare topologia hello</span><span class="sxs-lookup"><span data-stu-id="76be0-229">Build and start hello topology</span></span>

1. <span data-ttu-id="76be0-230">Aprire un nuovo prompt dei comandi e passare alla directory troppo`hdinsight-eventhub-example/TemperatureMonitor`.</span><span class="sxs-lookup"><span data-stu-id="76be0-230">Open a new command prompt and change directories too`hdinsight-eventhub-example/TemperatureMonitor`.</span></span> <span data-ttu-id="76be0-231">toobuild e pacchetto hello topologia, usare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="76be0-231">toobuild and package hello topology, use hello following command:</span></span> 

    ```bash
    mvn clean package
    ```

2. <span data-ttu-id="76be0-232">toostart hello topologia in modalità locale, usare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="76be0-232">toostart hello topology in local mode, use hello following command:</span></span>

    ```bash
    storm jar target/TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local --filter dev.properties resources/no-hbase.yaml
    ```

    * <span data-ttu-id="76be0-233">`--local`topologia di hello viene avviato in modalità locale.</span><span class="sxs-lookup"><span data-stu-id="76be0-233">`--local` starts hello topology in local mode.</span></span>
    * <span data-ttu-id="76be0-234">`--filter`Usa hello `dev.properties` file toopopulate parametri nella definizione della topologia hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-234">`--filter` uses hello `dev.properties` file toopopulate parameters in hello topology definition.</span></span>
    * <span data-ttu-id="76be0-235">`resources/no-hbase.yaml`Usa hello `no-hbase.yaml` definizione della topologia.</span><span class="sxs-lookup"><span data-stu-id="76be0-235">`resources/no-hbase.yaml` uses hello `no-hbase.yaml` topology definition.</span></span>
 
   <span data-ttu-id="76be0-236">Una volta avviata, topologia hello legge le voci da Hub di eventi e li invia dashboard toohello in esecuzione sul computer locale.</span><span class="sxs-lookup"><span data-stu-id="76be0-236">Once started, hello topology reads entries from Event Hub, and sends them toohello dashboard running on your local machine.</span></span> <span data-ttu-id="76be0-237">È necessario visualizzare le righe vengono visualizzati nel dashboard web hello, simile toohello seguente immagine:</span><span class="sxs-lookup"><span data-stu-id="76be0-237">You should see lines appear in hello web dashboard, similar toohello following image:</span></span>
   
    ![dashboard con dati](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

2. <span data-ttu-id="76be0-239">Durante l'esecuzione di dashboard hello utilizzare hello `node app.js` comando hello precedente passaggi toosend nuovi dati tooEvent hub.</span><span class="sxs-lookup"><span data-stu-id="76be0-239">While hello dashboard is running, use hello `node app.js` command from hello previous steps toosend new data tooEvent Hubs.</span></span> <span data-ttu-id="76be0-240">Poiché i valori della temperatura hello generati in modo casuale, grafico hello deve aggiornare le modifiche di grandi dimensioni tooshow della temperatura.</span><span class="sxs-lookup"><span data-stu-id="76be0-240">Because hello temperature values are randomly generated, hello graph should update tooshow large changes in temperature.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="76be0-241">È necessario essere in hello **hdinsight-eventhub-esempio/SendEvents/Nodejs** directory quando si utilizza hello `node app.js` comando.</span><span class="sxs-lookup"><span data-stu-id="76be0-241">You must be in hello **hdinsight-eventhub-example/SendEvents/Nodejs** directory when using hello `node app.js` command.</span></span>

3. <span data-ttu-id="76be0-242">Dopo la verifica degli aggiornamenti di dashboard hello, topologia hello stop utilizzando Ctrl + C.</span><span class="sxs-lookup"><span data-stu-id="76be0-242">After verifying that hello dashboard updates, stop hello topology using Ctrl+C.</span></span> <span data-ttu-id="76be0-243">È possibile utilizzare anche i server web locale hello toostop di Ctrl + C.</span><span class="sxs-lookup"><span data-stu-id="76be0-243">You can use Ctrl+C toostop hello local web server also.</span></span>

## <a name="create-a-storm-and-hbase-cluster"></a><span data-ttu-id="76be0-244">Creare un cluster Storm e HBase</span><span class="sxs-lookup"><span data-stu-id="76be0-244">Create a Storm and HBase cluster</span></span>

<span data-ttu-id="76be0-245">Hello i passaggi in questa sezione viene utilizzata una [modello di Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) toocreate un cluster di rete virtuale di Azure e un elevato numero di e HBase in rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-245">hello steps in this section use an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) toocreate an Azure Virtual Network and a Storm and HBase cluster on hello virtual network.</span></span> <span data-ttu-id="76be0-246">modello di Hello, inoltre, crea un'App Web di Azure e distribuisce una copia del dashboard hello al suo interno.</span><span class="sxs-lookup"><span data-stu-id="76be0-246">hello template also creates an Azure Web App and deploys a copy of hello dashboard into it.</span></span>

> [!NOTE]
> <span data-ttu-id="76be0-247">Una rete virtuale viene utilizzata in modo che topologia hello in esecuzione nel cluster Storm hello può comunicare direttamente con i cluster di HBase hello tramite API Java HBase hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-247">A virtual network is used so that hello topology running on hello Storm cluster can directly communicate with hello HBase cluster using hello HBase Java API.</span></span>

<span data-ttu-id="76be0-248">modello di gestione risorse di Hello utilizzato in questo documento si trova in un contenitore di blob pubblici in **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span><span class="sxs-lookup"><span data-stu-id="76be0-248">hello Resource Manager template used in this document is located in a public blob container at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span></span>

1. <span data-ttu-id="76be0-249">Fare clic su hello seguente pulsante toosign in tooAzure e il modello di gestione risorse hello Apri nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-249">Click hello following button toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-storm-cluster-in-vnet-3.6.json" target="_blank"><img src="./media/hdinsight-storm-sensor-data-analysis/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="76be0-250">Da hello **distribuzione personalizzata** immettere hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="76be0-250">From hello **Custom deployment** section, enter hello following values:</span></span>
   
    ![Parametri di HDInsight](./media/hdinsight-storm-sensor-data-analysis/parameters.png)
   
   * <span data-ttu-id="76be0-252">**Nome del Cluster di base**: questo valore viene utilizzato come nome di base per i cluster Storm e HBase hello hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-252">**Base Cluster Name**: This value is used as hello base name for hello Storm and HBase clusters.</span></span> <span data-ttu-id="76be0-253">Ad esempio, se si immette **abc** verranno creati un cluster Storm denominato **storm-abc** e un cluster HBase denominato **hbase-abc**.</span><span class="sxs-lookup"><span data-stu-id="76be0-253">For example, entering **abc** creates a Storm cluster named **storm-abc** and an HBase cluster named **hbase-abc**.</span></span>
   * <span data-ttu-id="76be0-254">**Nome utente di accesso del cluster**: nome utente amministratore di hello per i cluster Storm e HBase hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-254">**Cluster Login User Name**: hello admin user name for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="76be0-255">**Password di account di accesso cluster**: password dell'utente per i cluster Storm e HBase hello hello admin.</span><span class="sxs-lookup"><span data-stu-id="76be0-255">**Cluster Login Password**: hello admin user password for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="76be0-256">**Nome utente SSH**: hello toocreate utente SSH per i cluster Storm e HBase hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-256">**SSH User Name**: hello SSH user toocreate for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="76be0-257">**Password SSH**: password hello per utente SSH hello per i cluster Storm e HBase hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-257">**SSH Password**: hello password for hello SSH user for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="76be0-258">**Percorso**: area hello creati in cluster hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-258">**Location**: hello region that hello clusters are created in.</span></span>
     
     <span data-ttu-id="76be0-259">Fare clic su **OK** parametri hello toosave.</span><span class="sxs-lookup"><span data-stu-id="76be0-259">Click **OK** toosave hello parameters.</span></span>

3. <span data-ttu-id="76be0-260">Hello utilizzare **nozioni di base** sezione toocreate un gruppo di risorse o selezionarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="76be0-260">Use hello **Basics** section toocreate a resource group or select an existing one.</span></span>
4. <span data-ttu-id="76be0-261">In hello **percorso del gruppo di risorse** menu a discesa, seleziona hello nello stesso percorso come selezionato per hello **percorso** parametro hello **impostazioni** sezione.</span><span class="sxs-lookup"><span data-stu-id="76be0-261">In hello **Resource group location** dropdown menu, select hello same location as you selected for hello **Location** parameter in hello **Settings** section.</span></span>
5. <span data-ttu-id="76be0-262">Leggere le condizioni di hello e quindi selezionare **accetto le condizioni indicate in precedenza toohello**.</span><span class="sxs-lookup"><span data-stu-id="76be0-262">Read hello terms and conditions, and then select **I agree toohello terms and conditions stated above**.</span></span>
6. <span data-ttu-id="76be0-263">Infine, controllare **Pin toodashboard** e quindi selezionare **acquisto**.</span><span class="sxs-lookup"><span data-stu-id="76be0-263">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="76be0-264">Sono necessari circa 20 minuti toocreate cluster hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-264">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="76be0-265">Dopo avere create le risorse di hello, informazioni sui gruppi di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-265">Once hello resources have been created, information about hello resource group is displayed.</span></span>

![Gruppo di risorse per la rete virtuale hello e cluster](./media/hdinsight-storm-sensor-data-analysis/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="76be0-267">Si noti che sono nomi hello dei cluster HDInsight hello **storm BASENAME** e **hbase BASENAME**, dove BASENAME è nome hello toohello modello specificato.</span><span class="sxs-lookup"><span data-stu-id="76be0-267">Notice that hello names of hello HDInsight clusters are **storm-BASENAME** and **hbase-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="76be0-268">Utilizzare questi nomi in un passaggio successivo durante la connessione toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="76be0-268">You use these names in a later step when connecting toohello clusters.</span></span> <span data-ttu-id="76be0-269">È anche nota che hello nome del sito dashboard hello **basename dashboard**.</span><span class="sxs-lookup"><span data-stu-id="76be0-269">Also note that hello name of hello dashboard site is **basename-dashboard**.</span></span> <span data-ttu-id="76be0-270">Questo valore viene usato più avanti in questo documento.</span><span class="sxs-lookup"><span data-stu-id="76be0-270">This value is used later in this document.</span></span>

## <a name="configure-hello-dashboard-bolt"></a><span data-ttu-id="76be0-271">Configurare fulmine Dashboard hello</span><span class="sxs-lookup"><span data-stu-id="76be0-271">Configure hello Dashboard bolt</span></span>

<span data-ttu-id="76be0-272">i dashboard di toohello dati toosend distribuiti come un'app web, è necessario modificare hello seguente riga hello `dev.properties`file:</span><span class="sxs-lookup"><span data-stu-id="76be0-272">toosend data toohello dashboard deployed as a web app, you must modify hello following line in hello `dev.properties`file:</span></span>

```yaml
dashboard.uri: http://localhost:3000
```

<span data-ttu-id="76be0-273">Modifica `http://localhost:3000` troppo`http://BASENAME-dashboard.azurewebsites.net` e salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-273">Change `http://localhost:3000` too`http://BASENAME-dashboard.azurewebsites.net` and save hello file.</span></span> <span data-ttu-id="76be0-274">Sostituire **BASENAME** con il nome di base hello specificato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-274">Replace **BASENAME** with hello base name you provided in hello previous step.</span></span> <span data-ttu-id="76be0-275">È anche possibile utilizzare il gruppo di risorse hello creato in precedenza hello tooselect dashboard e visualizzare URL hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-275">You can also use hello resource group created previously tooselect hello dashboard and view hello URL.</span></span>

## <a name="create-hello-hbase-table"></a><span data-ttu-id="76be0-276">Creare una tabella HBase hello</span><span class="sxs-lookup"><span data-stu-id="76be0-276">Create hello HBase table</span></span>

<span data-ttu-id="76be0-277">toostore dati in HBase, è innanzitutto necessario creare una tabella.</span><span class="sxs-lookup"><span data-stu-id="76be0-277">toostore data in HBase, we must first create a table.</span></span> <span data-ttu-id="76be0-278">Creazione preliminare di Storm deve toowrite per le risorse, in quanto durante il tentativo toocreate risorse all'interno di una topologia di Storm possono generare più istanze durante il tentativo toocreate hello stessa risorsa.</span><span class="sxs-lookup"><span data-stu-id="76be0-278">Pre-create resources that Storm needs toowrite to, as trying toocreate resources from inside a Storm topology can result in multiple instances trying toocreate hello same resource.</span></span> <span data-ttu-id="76be0-279">Creare risorse hello esterne topologia hello e utilizzare Storm per analitica e di lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="76be0-279">Create hello resources outside hello topology and use Storm for reading/writing and analytics.</span></span>

1. <span data-ttu-id="76be0-280">Utilizzare cluster HBase toohello tooconnect SSH utilizzando hello SSH e la password utente fornite toohello modello durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="76be0-280">Use SSH tooconnect toohello HBase cluster using hello SSH user and password you supplied toohello template during cluster creation.</span></span> <span data-ttu-id="76be0-281">Ad esempio, se la connessione utilizzando hello `ssh` comando, utilizzare la seguente sintassi hello:</span><span class="sxs-lookup"><span data-stu-id="76be0-281">For example, if connecting using hello `ssh` command, you would use hello following syntax:</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```
   
    <span data-ttu-id="76be0-282">Sostituire `sshuser` con nome utente di hello SSH forniti durante la creazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-282">Replace `sshuser` with hello SSH user name you provided when creating hello cluster.</span></span> <span data-ttu-id="76be0-283">Sostituire `clustername` con il nome del cluster HBase hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-283">Replace `clustername` with hello HBase cluster name.</span></span>

2. <span data-ttu-id="76be0-284">Dalla sessione SSH hello, avviare la shell di HBase hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-284">From hello SSH session, start hello HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="76be0-285">Una volta caricate shell hello, vedrai un `hbase(main):001:0>` prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="76be0-285">Once hello shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="76be0-286">Dalla shell di HBase hello, immettere hello toocreate comando dati del sensore una tabella toostore hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="76be0-286">From hello HBase shell, enter hello following command toocreate a table toostore hello sensor data:</span></span>
   
    ```hbase
    create 'SensorData', 'cf'
    ```

4. <span data-ttu-id="76be0-287">Verificare che la tabella hello è stata creata utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="76be0-287">Verify that hello table has been created by using hello following command:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="76be0-288">Vengono restituite informazioni toohello simile esempio seguente, che indica che sono disponibili 0 righe nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-288">This returns information similar toohello following example, indicating that there are 0 rows in hello table.</span></span>
   
        ROW                   COLUMN+CELL                                       0 row(s) in 0.1900 seconds

5. <span data-ttu-id="76be0-289">Immettere `exit` tooexit hello shell di HBase:</span><span class="sxs-lookup"><span data-stu-id="76be0-289">Enter `exit` tooexit hello HBase shell:</span></span>

## <a name="configure-hello-hbase-bolt"></a><span data-ttu-id="76be0-290">Configurare fulmine HBase hello</span><span class="sxs-lookup"><span data-stu-id="76be0-290">Configure hello HBase bolt</span></span>

<span data-ttu-id="76be0-291">tooHBase toowrite dal cluster Storm hello, è necessario fornire fulmine HBase hello con i dettagli di configurazione hello del cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="76be0-291">toowrite tooHBase from hello Storm cluster, you must provide hello HBase bolt with hello configuration details of your HBase cluster.</span></span>

1. <span data-ttu-id="76be0-292">Utilizzare uno dei seguenti quorum di esempi tooretrieve hello Zookeeper per il cluster HBase hello:</span><span class="sxs-lookup"><span data-stu-id="76be0-292">Use one of hello following examples tooretrieve hello Zookeeper quorum for your HBase cluster:</span></span>

    ```bash
    CLUSTERNAME='your_HDInsight_cluster_name'
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HBASE/components/HBASE_MASTER" | jq '.metrics.hbase.master.ZookeeperQuorum'
    ```

    > [!NOTE]
    > <span data-ttu-id="76be0-293">Sostituire `your_HDInsight_cluster_name` con nome hello del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="76be0-293">Replace `your_HDInsight_cluster_name` with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="76be0-294">Per ulteriori informazioni sull'installazione hello `jq` utilità, vedere [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="76be0-294">For more information on installing hello `jq` utility, see [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span></span>
    >
    > <span data-ttu-id="76be0-295">Quando richiesto, immettere la password di hello per account di accesso amministratore hello HDInsight.</span><span class="sxs-lookup"><span data-stu-id="76be0-295">When prompted, enter hello password for hello HDInsight admin login.</span></span>

    ```powershell
    $clusterName = 'your_HDInsight_cluster_name`
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HBASE/components/HBASE_MASTER" -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.metrics.hbase.master.ZookeeperQuorum
    ```

    > [!NOTE]
    > <span data-ttu-id="76be0-296">Sostituire ' your_HDInsight_cluster_name con nome hello del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="76be0-296">Replace \`your_HDInsight_cluster_name with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="76be0-297">Quando richiesto, immettere la password di hello per account di accesso amministratore hello HDInsight.</span><span class="sxs-lookup"><span data-stu-id="76be0-297">When prompted, enter hello password for hello HDInsight admin login.</span></span>
    >
    > <span data-ttu-id="76be0-298">Questo esempio richiede Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="76be0-298">This example requires Azure PowerShell.</span></span> <span data-ttu-id="76be0-299">Per altre informazioni sull'uso di Azure PowerShell, vedere [Getting started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6) (Introduzione ad Azure PowerShell)</span><span class="sxs-lookup"><span data-stu-id="76be0-299">For more information on using Azure PowerShell, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)</span></span>

    <span data-ttu-id="76be0-300">informazioni di Hello restituite da questi esempi sono simile toohello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="76be0-300">hello information returned by these examples is similar toohello following text:</span></span>

    `zk2-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk0-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk3-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181`

    <span data-ttu-id="76be0-301">Queste informazioni vengono utilizzate da toocommunicate Storm con cluster HBase hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-301">This information is used by Storm toocommunicate with hello HBase cluster.</span></span>

2. <span data-ttu-id="76be0-302">Modificare hello `dev.properties` file e aggiungere hello Zookeeper quorum informazioni toohello seguente riga:</span><span class="sxs-lookup"><span data-stu-id="76be0-302">Modify hello `dev.properties` file and add hello Zookeeper quorum information toohello following line:</span></span>

    ```yaml
    hbase.zookeeper.quorum: your_hbase_quorum
    ```

## <a name="build-package-and-deploy-hello-solution-toohdinsight"></a><span data-ttu-id="76be0-303">Pacchetto, compilare e distribuire hello soluzione tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="76be0-303">Build, package, and deploy hello solution tooHDInsight</span></span>

<span data-ttu-id="76be0-304">Nell'ambiente di sviluppo, utilizzare hello cluster storm passaggi toodeploy hello Storm topologia toohello seguente.</span><span class="sxs-lookup"><span data-stu-id="76be0-304">In your development environment, use hello following steps toodeploy hello Storm topology toohello storm cluster.</span></span>

1. <span data-ttu-id="76be0-305">Da hello `TemperatureMonitor` directory seguenti hello utilizzare comando tooperform una nuova compilazione e creare un pacchetto di file JAR dal progetto:</span><span class="sxs-lookup"><span data-stu-id="76be0-305">From hello `TemperatureMonitor` directory, use hello following command tooperform a new build and create a JAR package from your project:</span></span>
   
        mvn clean package
   
    <span data-ttu-id="76be0-306">Questo comando crea un file denominato `TemperatureMonitor-1.0-SNAPSHOT.jar in hello ` nella directory "target" del progetto.</span><span class="sxs-lookup"><span data-stu-id="76be0-306">This command creates a file named `TemperatureMonitor-1.0-SNAPSHOT.jar in hello `target\` directory of your project.</span></span>

2. <span data-ttu-id="76be0-307">Hello di utilizzare scp tooupload `TemperatureMonitor-1.0-SNAPSHOT.jar` e `dev.properties` cluster Storm tooyour di file.</span><span class="sxs-lookup"><span data-stu-id="76be0-307">Use scp tooupload hello `TemperatureMonitor-1.0-SNAPSHOT.jar` and `dev.properties` files tooyour Storm cluster.</span></span> <span data-ttu-id="76be0-308">In hello seguente esempio, sostituire `sshuser` con utente SSH hello specificato durante la creazione di cluster di hello e `clustername` con nome hello del cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="76be0-308">In hello following example, replace `sshuser` with hello SSH user you provided when creating hello cluster, and `clustername` with hello name of your Storm cluster.</span></span> <span data-ttu-id="76be0-309">Quando richiesto, immettere la password di hello per utente SSH hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-309">When prompted, enter hello password for hello SSH user.</span></span>
   
    ```bash
    scp target/TemperatureMonitor-1.0-SNAPSHOT.jar dev.properties sshuser@clustername-ssh.azurehdinsight.net:
    ```

   > [!NOTE]
   > <span data-ttu-id="76be0-310">Potrebbe richiedere alcuni minuti file hello tooupload.</span><span class="sxs-lookup"><span data-stu-id="76be0-310">It may take several minutes tooupload hello files.</span></span>

    <span data-ttu-id="76be0-311">Per ulteriori informazioni sull'utilizzo di hello `scp` e `ssh` i comandi con HDInsight, vedere [utilizzo di SSH con HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="76be0-311">For more information on using hello `scp` and `ssh` commands with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

3. <span data-ttu-id="76be0-312">Dopo aver hello file è stato caricato, connettersi cluster Storm toohello tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="76be0-312">Once hello file has been uploaded, connect toohello Storm cluster using SSH.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="76be0-313">Sostituire `sshuser` con nome utente di hello SSH.</span><span class="sxs-lookup"><span data-stu-id="76be0-313">Replace `sshuser` with hello SSH user name.</span></span> <span data-ttu-id="76be0-314">Sostituire `clustername` con il nome del cluster Storm hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-314">Replace `clustername` with hello Storm cluster name.</span></span>

4. <span data-ttu-id="76be0-315">toostart hello topologia, usare hello comando dalla sessione SSH hello seguente:</span><span class="sxs-lookup"><span data-stu-id="76be0-315">toostart hello topology, use hello following command from hello SSH session:</span></span>
   
    ```bash
    storm jar TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote --filter dev.properties -R /with-hbase.yaml
    ```

    * <span data-ttu-id="76be0-316">`--remote`Invia hello topologia toohello servizio Nimbus, che distribuisce i nodi del Supervisore toohello cluster hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-316">`--remote` submits hello topology toohello Nimbus service, which distributes it toohello supervisor nodes in hello cluster.</span></span>
    * <span data-ttu-id="76be0-317">`--filter`Usa hello `dev.properties` file toopopulate parametri nella definizione della topologia hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-317">`--filter` uses hello `dev.properties` file toopopulate parameters in hello topology definition.</span></span>
    * <span data-ttu-id="76be0-318">`-R /with-hbase.yaml`Usa hello `with-hbase.yaml` topologia inclusa nel pacchetto hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-318">`-R /with-hbase.yaml` uses hello `with-hbase.yaml` topology included in hello package.</span></span>

5. <span data-ttu-id="76be0-319">Dopo l'avvio della topologia di hello, aprire un sito Web toohello browser è stato pubblicato in Azure, quindi utilizzare hello `node app.js` comando toosend dati tooEvent Hub.</span><span class="sxs-lookup"><span data-stu-id="76be0-319">After hello topology has started, open a browser toohello website you published on Azure, then use hello `node app.js` command toosend data tooEvent Hub.</span></span> <span data-ttu-id="76be0-320">Informazioni di hello web dashboard aggiornamento toodisplay hello dovrebbe.</span><span class="sxs-lookup"><span data-stu-id="76be0-320">You should see hello web dashboard update toodisplay hello information.</span></span>
   
    ![dashboard](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

## <a name="view-hbase-data"></a><span data-ttu-id="76be0-322">Visualizzare i dati di HBase</span><span class="sxs-lookup"><span data-stu-id="76be0-322">View HBase data</span></span>

<span data-ttu-id="76be0-323">Utilizzare i seguenti passaggi tooconnect tooHBase hello e verificare che siano stati scritti dati hello toohello tabella:</span><span class="sxs-lookup"><span data-stu-id="76be0-323">Use hello following steps tooconnect tooHBase and verify that hello data has been written toohello table:</span></span>

1. <span data-ttu-id="76be0-324">Utilizzare cluster HBase di toohello tooconnect SSH.</span><span class="sxs-lookup"><span data-stu-id="76be0-324">Use SSH tooconnect toohello HBase cluster.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="76be0-325">Sostituire `sshuser` con nome utente di hello SSH.</span><span class="sxs-lookup"><span data-stu-id="76be0-325">Replace `sshuser` with hello SSH user name.</span></span> <span data-ttu-id="76be0-326">Sostituire `clustername` con il nome del cluster HBase hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-326">Replace `clustername` with hello HBase cluster name.</span></span>

2. <span data-ttu-id="76be0-327">Dalla sessione SSH hello, avviare la shell di HBase hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-327">From hello SSH session, start hello HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="76be0-328">Una volta caricate shell hello, vedrai un `hbase(main):001:0>` prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="76be0-328">Once hello shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="76be0-329">Visualizza le righe dalla tabella hello:</span><span class="sxs-lookup"><span data-stu-id="76be0-329">View rows from hello table:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="76be0-330">Questo comando restituisce informazioni toohello simile seguendo il testo, che indica che è dati nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-330">This command returns information similar toohello following text, indicating that there is data in hello table.</span></span>
   
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
   > <span data-ttu-id="76be0-331">Questa operazione di analisi restituisce un massimo di 10 righe dalla tabella hello.</span><span class="sxs-lookup"><span data-stu-id="76be0-331">This scan operation returns a maximum of 10 rows from hello table.</span></span>

## <a name="delete-your-clusters"></a><span data-ttu-id="76be0-332">Eliminare i cluster</span><span class="sxs-lookup"><span data-stu-id="76be0-332">Delete your clusters</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="76be0-333">toodelete hello cluster, archiviazione e app web in una sola volta, Elimina gruppo di risorse hello che li contiene.</span><span class="sxs-lookup"><span data-stu-id="76be0-333">toodelete hello clusters, storage, and web app at one time, delete hello resource group that contains them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76be0-334">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="76be0-334">Next steps</span></span>

<span data-ttu-id="76be0-335">Per altri esempi di topologie Storm con HDInsight, vedere [Topologie di esempio per Storm in HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="76be0-335">For more examples of Storm topologies with HDInsight, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md)</span></span>

<span data-ttu-id="76be0-336">Per ulteriori informazioni su Apache Storm, vedere hello [Apache Storm](https://storm.incubator.apache.org/) sito.</span><span class="sxs-lookup"><span data-stu-id="76be0-336">For more information about Apache Storm, see hello [Apache Storm](https://storm.incubator.apache.org/) site.</span></span>

<span data-ttu-id="76be0-337">Per ulteriori informazioni su HBase in HDInsight, vedere hello [HBase di HDInsight Panoramica](hdinsight-hbase-overview.md).</span><span class="sxs-lookup"><span data-stu-id="76be0-337">For more information about HBase on HDInsight, see hello [HBase with HDInsight Overview](hdinsight-hbase-overview.md).</span></span>

<span data-ttu-id="76be0-338">Per ulteriori informazioni su Socket.io, vedere hello [socket.io](http://socket.io/) sito.</span><span class="sxs-lookup"><span data-stu-id="76be0-338">For more information about Socket.io, see hello [socket.io](http://socket.io/) site.</span></span>

<span data-ttu-id="76be0-339">Per altre informazioni su D3.js, vedere [D3.js - Data Driven Documents](http://d3js.org/).</span><span class="sxs-lookup"><span data-stu-id="76be0-339">For more information about D3.js, see [D3.js - Data Driven Documents](http://d3js.org/).</span></span>

<span data-ttu-id="76be0-340">Per altre informazioni sulla creazione di topologie in Java, vedere [Sviluppo di topologie basate su Java per Apache Storm in HDInsight](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="76be0-340">For information about creating topologies in Java, see [Develop Java topologies for Apache Storm on HDInsight](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="76be0-341">Per altre informazioni sulla creazione di topologie in .NET, vedere [Sviluppare topologie C# per Apache Storm in HDInsight tramite Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="76be0-341">For information about creating topologies in .NET, see [Develop C# topologies for Apache Storm on HDInsight using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

[azure-portal]: https://portal.azure.com
