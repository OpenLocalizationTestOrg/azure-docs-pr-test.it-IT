---
title: Correlare gli eventi nel tempo con Storm e HBase in HDInsight
description: Informazioni su come correlare gli eventi che giungono in momenti diversi tramite Storm e HBase in HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 17d11479-2d02-4790-8d29-05fb38351479
ms.service: hdinsight
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 06630096383601e48e8f69f8553314cee42f5f3e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="correlate-events-that-arrive-at-different-times-using-storm-and-hbase"></a><span data-ttu-id="6632e-103">Correlare eventi che arrivano in momenti diversi tramite Storm e HBase</span><span class="sxs-lookup"><span data-stu-id="6632e-103">Correlate events that arrive at different times using Storm and HBase</span></span>

<span data-ttu-id="6632e-104">Utilizzando un archivio dati permanente con Apache Storm, è possibile correlare le voci di dati che arrivano in momenti diversi.</span><span class="sxs-lookup"><span data-stu-id="6632e-104">By using a persistent data store with Apache Storm, you can correlate data entries that arrive at different times.</span></span> <span data-ttu-id="6632e-105">Ad esempio, il collegamento degli eventi di accesso e disconnessione di una sessione utente per calcolare il tempo di esecuzione della sessione.</span><span class="sxs-lookup"><span data-stu-id="6632e-105">For example, linking login and logout events for a user session to calculate how long the session lasted.</span></span>

<span data-ttu-id="6632e-106">Questo documento descrive come creare una topologia di Storm C# di base che tenga traccia degli eventi di accesso e disconnessione per le sessioni utente e che calcoli la durata della sessione.</span><span class="sxs-lookup"><span data-stu-id="6632e-106">In this document, you learn how to create a basic C# Storm topology that tracks login and logout events for user sessions, and calculates the duration of the session.</span></span> <span data-ttu-id="6632e-107">La topologia utilizza HBase come archivio dati permanente.</span><span class="sxs-lookup"><span data-stu-id="6632e-107">The topology uses HBase as a persistent data store.</span></span> <span data-ttu-id="6632e-108">HBase consente inoltre di eseguire query in batch sui dati cronologici per ottenere informazioni aggiuntive,</span><span class="sxs-lookup"><span data-stu-id="6632e-108">HBase also allows you to perform batch queries on the historical data to produce additional insights.</span></span> <span data-ttu-id="6632e-109">ad esempio il numero di sessioni utente avviate o terminate in un determinato periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="6632e-109">For example, how many user sessions were started or ended during a specific time period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6632e-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6632e-110">Prerequisites</span></span>

* <span data-ttu-id="6632e-111">Visual Studio e gli strumenti di HDInsight per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6632e-111">Visual Studio and the HDInsight tools for Visual Studio.</span></span> <span data-ttu-id="6632e-112">Per altre informazioni, vedere [Introduzione all'uso di strumenti di HDInsight per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6632e-112">For more information, see [Get started using the HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="6632e-113">Cluster Apache Storm in HDInsight, basato su Windows.</span><span class="sxs-lookup"><span data-stu-id="6632e-113">Apache Storm on HDInsight cluster (Windows-based).</span></span>

  > [!WARNING]
  > <span data-ttu-id="6632e-114">Anche se le topologie SCP.NET sono supportate nei cluster Storm basati su Linux creati dopo il 28/10/2016, il pacchetto HBase SDK per .NET disponibile dal 28/10/2016 non funziona correttamente in HDInsight basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="6632e-114">While SCP.NET topologies are supported on Linux-based Storm clusters created after 10/28/2016, the HBase SDK for .NET package available as of 10/28/2016 does not work correctly on Linux-based HDInsight</span></span>

* <span data-ttu-id="6632e-115">Cluster Apache HBase in HDInsight, basato su Linux o su Windows.</span><span class="sxs-lookup"><span data-stu-id="6632e-115">Apache HBase on HDInsight cluster (Linux or Windows-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="6632e-116">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="6632e-116">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6632e-117">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="6632e-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="6632e-118">[Java](https://java.com) 1.7 o versione successiva nell'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="6632e-118">[Java](https://java.com) 1.7 or greater on your development environment.</span></span> <span data-ttu-id="6632e-119">Java viene usato per creare il pacchetto della topologia per l'invio al cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6632e-119">Java is used to package the topology when it is submitted to the HDInsight cluster.</span></span>

  * <span data-ttu-id="6632e-120">La variabile di ambiente **JAVA_HOME** deve puntare alla directory contenente Java.</span><span class="sxs-lookup"><span data-stu-id="6632e-120">The **JAVA_HOME** environment variable must point to the directory that contains Java.</span></span>
  * <span data-ttu-id="6632e-121">La directory **%JAVA_HOME%/bin** deve essere inclusa nel percorso.</span><span class="sxs-lookup"><span data-stu-id="6632e-121">The **%JAVA_HOME%/bin** directory must be in the path</span></span>

## <a name="architecture"></a><span data-ttu-id="6632e-122">Architettura</span><span class="sxs-lookup"><span data-stu-id="6632e-122">Architecture</span></span>

![Diagramma del flusso di dati tramite la topologia](./media/hdinsight-storm-correlation-topology/correlationtopology.png)

<span data-ttu-id="6632e-124">La correlazione di eventi richiede un identificatore comune per l'origine dell'evento.</span><span class="sxs-lookup"><span data-stu-id="6632e-124">Correlating events requires a common identifier for the event source.</span></span> <span data-ttu-id="6632e-125">Ad esempio, un ID utente, un ID di sessione o altro dato che sia a) univoco e b) incluso in tutti i dati inviati a Storm.</span><span class="sxs-lookup"><span data-stu-id="6632e-125">For example, a user ID, session ID, or other piece of data that is a) unique and b) included in all data sent to Storm.</span></span> <span data-ttu-id="6632e-126">In questo esempio viene utilizzato un valore GUID per rappresentare un ID sessione.</span><span class="sxs-lookup"><span data-stu-id="6632e-126">This example uses a GUID value to represent a session ID.</span></span>

<span data-ttu-id="6632e-127">Questo esempio è costituito da due cluster di HDInsight:</span><span class="sxs-lookup"><span data-stu-id="6632e-127">This example consists of two HDInsight clusters:</span></span>

* <span data-ttu-id="6632e-128">HBase: archivio dati permanente per i dati cronologici</span><span class="sxs-lookup"><span data-stu-id="6632e-128">HBase: persistent data store for historical data</span></span>
* <span data-ttu-id="6632e-129">Storm: utilizzato per inserire i dati in ingresso</span><span class="sxs-lookup"><span data-stu-id="6632e-129">Storm: used to ingest incoming data</span></span>

<span data-ttu-id="6632e-130">I dati vengono generati casualmente dalla topologia di Storm e sono costituiti dai seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="6632e-130">The data is randomly generated by the Storm topology, and consists of the following items:</span></span>

* <span data-ttu-id="6632e-131">ID di sessione: un GUID che identifica in modo univoco ogni sessione</span><span class="sxs-lookup"><span data-stu-id="6632e-131">Session ID: a GUID that uniquely identifies each session</span></span>
* <span data-ttu-id="6632e-132">Evento: un evento START o END.</span><span class="sxs-lookup"><span data-stu-id="6632e-132">Event: a START or END event.</span></span> <span data-ttu-id="6632e-133">Per questo esempio, l'evento START si verifica sempre prima dell'evento END</span><span class="sxs-lookup"><span data-stu-id="6632e-133">For this example, START always occurs before END</span></span>
* <span data-ttu-id="6632e-134">Ora: l'ora dell'evento.</span><span class="sxs-lookup"><span data-stu-id="6632e-134">Time: the time of the event.</span></span>

<span data-ttu-id="6632e-135">Questi dati vengono elaborati e archiviati in HBase.</span><span class="sxs-lookup"><span data-stu-id="6632e-135">This data is processed and stored in HBase.</span></span>

### <a name="storm-topology"></a><span data-ttu-id="6632e-136">Topologia Storm</span><span class="sxs-lookup"><span data-stu-id="6632e-136">Storm topology</span></span>

<span data-ttu-id="6632e-137">Quando si avvia una sessione, un evento **START** viene ricevuto dalla topologia e registrato in HBase.</span><span class="sxs-lookup"><span data-stu-id="6632e-137">When a session starts, a **START** event is received by the topology and logged to HBase.</span></span> <span data-ttu-id="6632e-138">Quando viene ricevuto un evento **END**, la topologia recupera l'evento **START** e calcola il tempo tra i due eventi.</span><span class="sxs-lookup"><span data-stu-id="6632e-138">When an **END** event is received, the topology retrieves the **START** event and calculates the time between the two events.</span></span> <span data-ttu-id="6632e-139">Questo valore relativo alla **durata** viene quindi archiviato in HBase con le informazioni sull'evento **END**.</span><span class="sxs-lookup"><span data-stu-id="6632e-139">This **Duration** value is then stored in HBase along with the **END** event information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6632e-140">Mentre con questa topologia viene illustrato il modello di base, per una soluzione di produzione potrebbe essere necessaria la progettazione per gli scenari seguenti:</span><span class="sxs-lookup"><span data-stu-id="6632e-140">While this topology demonstrates the basic pattern, a production solution would need to take design for the following scenarios:</span></span>
>
> * <span data-ttu-id="6632e-141">Eventi che arrivano nell'ordine errato</span><span class="sxs-lookup"><span data-stu-id="6632e-141">Events arriving out of order</span></span>
> * <span data-ttu-id="6632e-142">Eventi duplicati</span><span class="sxs-lookup"><span data-stu-id="6632e-142">Duplicate events</span></span>
> * <span data-ttu-id="6632e-143">Eventi eliminati</span><span class="sxs-lookup"><span data-stu-id="6632e-143">Dropped events</span></span>

<span data-ttu-id="6632e-144">La topologia di esempio è costituita dai seguenti componenti:</span><span class="sxs-lookup"><span data-stu-id="6632e-144">The sample topology is composed of the following components:</span></span>

* <span data-ttu-id="6632e-145">Session.cs: simula una sessione utente tramite la creazione di un ID di sessione casuale, l'ora di inizio e la durata della sessione.</span><span class="sxs-lookup"><span data-stu-id="6632e-145">Session.cs: simulates a user session by creating a random session ID, start time, and how long the session lasts.</span></span>

* <span data-ttu-id="6632e-146">Spout.cs: crea 100 sessioni, genera un evento START, attende il timeout casuale per ogni sessione e quindi genera un evento END.</span><span class="sxs-lookup"><span data-stu-id="6632e-146">Spout.cs: creates 100 sessions, emits a START event, waits the random timeout for each session, and then emits an END event.</span></span> <span data-ttu-id="6632e-147">Successivamente, ricicla le sessioni terminate per generarne di nuove.</span><span class="sxs-lookup"><span data-stu-id="6632e-147">Then recycles ended sessions to generate new ones.</span></span>

* <span data-ttu-id="6632e-148">HBaseLookupBolt.cs: utilizza l'ID di sessione per cercare le informazioni di sessione da HBase.</span><span class="sxs-lookup"><span data-stu-id="6632e-148">HBaseLookupBolt.cs: uses the session ID to look up session information from HBase.</span></span> <span data-ttu-id="6632e-149">Quando viene elaborato un evento END, consente di trovare l'evento START corrispondente e calcola la durata della sessione.</span><span class="sxs-lookup"><span data-stu-id="6632e-149">When an END event is processed, it finds the corresponding START event and calculates the duration of the session.</span></span>

* <span data-ttu-id="6632e-150">HBaseBolt.cs: archivia le informazioni in HBase.</span><span class="sxs-lookup"><span data-stu-id="6632e-150">HBaseBolt.cs: Stores information into HBase.</span></span>

* <span data-ttu-id="6632e-151">TypeHelper.cs: consente la conversione di tipo durante la lettura/scrittura in HBase.</span><span class="sxs-lookup"><span data-stu-id="6632e-151">TypeHelper.cs: Helps with type conversion when reading from/writing to HBase.</span></span>

### <a name="hbase-schema"></a><span data-ttu-id="6632e-152">Schema HBase</span><span class="sxs-lookup"><span data-stu-id="6632e-152">HBase schema</span></span>

<span data-ttu-id="6632e-153">In HBase, i dati vengono archiviati in una tabella con lo schema e le impostazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="6632e-153">In HBase, the data is stored in a table with the following schema/settings:</span></span>

* <span data-ttu-id="6632e-154">Chiave di riga: la sessione ID viene utilizzato come chiave per le righe in questa tabella.</span><span class="sxs-lookup"><span data-stu-id="6632e-154">Row key: the session ID is used as the key for rows in this table.</span></span>

* <span data-ttu-id="6632e-155">Famiglia di colonne: il nome di famiglia è 'cf'.</span><span class="sxs-lookup"><span data-stu-id="6632e-155">Column family: the family name is 'cf'.</span></span> <span data-ttu-id="6632e-156">Le colonne memorizzate in questo gruppo sono le seguenti:</span><span class="sxs-lookup"><span data-stu-id="6632e-156">Columns stored in this family are:</span></span>

  * <span data-ttu-id="6632e-157">event: START o END.</span><span class="sxs-lookup"><span data-stu-id="6632e-157">event: START or END.</span></span>

  * <span data-ttu-id="6632e-158">time: il tempo in millisecondi in cui si è verificato l'evento.</span><span class="sxs-lookup"><span data-stu-id="6632e-158">time: the time in milliseconds that the event occurred.</span></span>

  * <span data-ttu-id="6632e-159">duration: la lunghezza del periodo di tempo che intercorre tra gli eventi START ed END.</span><span class="sxs-lookup"><span data-stu-id="6632e-159">duration: the length between START and END event.</span></span>

* <span data-ttu-id="6632e-160">VERSIONS: la famiglia 'cf' è impostata per conservare 5 versioni di ogni riga.</span><span class="sxs-lookup"><span data-stu-id="6632e-160">VERSIONS: the 'cf' family is set to retain 5 versions of each row.</span></span>

  > [!NOTE]
  > <span data-ttu-id="6632e-161">Le versioni sono un registro dei valori precedentemente memorizzati per una chiave di riga specifica.</span><span class="sxs-lookup"><span data-stu-id="6632e-161">Versions are a log of previous values stored for a specific row key.</span></span> <span data-ttu-id="6632e-162">Per impostazione predefinita, HBase restituisce solo il valore relativo alla versione più recente di una riga.</span><span class="sxs-lookup"><span data-stu-id="6632e-162">By default, HBase only returns the value for the most recent version of a row.</span></span> <span data-ttu-id="6632e-163">In questo caso, la stessa riga viene utilizzata per tutti gli eventi (START, END) ogni versione di una riga viene identificata dal valore di timestamp.</span><span class="sxs-lookup"><span data-stu-id="6632e-163">In this case, the same row is used for all events (START, END.) each version of a row is identified by the timestamp value.</span></span> <span data-ttu-id="6632e-164">Le versioni forniscono una visualizzazione cronologica degli eventi registrati per un ID specifico.</span><span class="sxs-lookup"><span data-stu-id="6632e-164">Versions provide a historical view of events logged for a specific ID.</span></span>

## <a name="download-the-project"></a><span data-ttu-id="6632e-165">Scaricare il progetto</span><span class="sxs-lookup"><span data-stu-id="6632e-165">Download the project</span></span>

<span data-ttu-id="6632e-166">Il progetto di esempio può essere scaricato da [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span><span class="sxs-lookup"><span data-stu-id="6632e-166">The sample project can be downloaded from [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span></span>

<span data-ttu-id="6632e-167">Il download contiene i seguenti progetti C#:</span><span class="sxs-lookup"><span data-stu-id="6632e-167">This download contains the following C# projects:</span></span>

* <span data-ttu-id="6632e-168">CorrelationTopology: topologia Storm di C# che casualmente genera eventi di inizio e di fine per le sessioni utente.</span><span class="sxs-lookup"><span data-stu-id="6632e-168">CorrelationTopology: C# Storm topology that randomly emits start and end events for user sessions.</span></span> <span data-ttu-id="6632e-169">La durata di ogni sessione è compresa tra 1 e 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="6632e-169">Each session lasts between 1 and 5 minutes.</span></span>

* <span data-ttu-id="6632e-170">SessionInfo: applicazione console C# che crea la tabella HBase e fornisce query di esempio per restituire informazioni sui dati della sessione archiviati.</span><span class="sxs-lookup"><span data-stu-id="6632e-170">SessionInfo: C# console application that creates the HBase table, and provides example queries to return information about stored session data.</span></span>

## <a name="create-the-table"></a><span data-ttu-id="6632e-171">Creare la tabella</span><span class="sxs-lookup"><span data-stu-id="6632e-171">Create the table</span></span>

1. <span data-ttu-id="6632e-172">Aprire il progetto **SessionInfo** in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6632e-172">Open the **SessionInfo** project in Visual Studio.</span></span>

2. <span data-ttu-id="6632e-173">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto **SessionInfo**, quindi scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="6632e-173">In **Solution Explorer**, right-click the **SessionInfo** project and select **Properties**.</span></span>

    ![Schermata del menu con le proprietà selezionate](./media/hdinsight-storm-correlation-topology/selectproperties.png)

3. <span data-ttu-id="6632e-175">Selezionare **Impostazioni**, quindi impostare i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="6632e-175">Select **Settings**, then set the following values:</span></span>

   * <span data-ttu-id="6632e-176">HBaseClusterURL: l'URL del cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="6632e-176">HBaseClusterURL: the URL to your HBase cluster.</span></span> <span data-ttu-id="6632e-177">Ad esempio, https://myhbasecluster.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="6632e-177">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="6632e-178">HBaseClusterUserName: l'account amministratore/utente HTTP per il cluster</span><span class="sxs-lookup"><span data-stu-id="6632e-178">HBaseClusterUserName: the admin/HTTP user account for your cluster</span></span>

   * <span data-ttu-id="6632e-179">HBaseClusterPassword: la password per l'account amministratore/utente HTTP</span><span class="sxs-lookup"><span data-stu-id="6632e-179">HBaseClusterPassword: the password for the admin/HTTP user account</span></span>

   * <span data-ttu-id="6632e-180">HBaseTableName: il nome della tabella da utilizzare in questo esempio</span><span class="sxs-lookup"><span data-stu-id="6632e-180">HBaseTableName: the name of the table to use with this example</span></span>

   * <span data-ttu-id="6632e-181">HBaseTableColumnFamily: il nome di famiglia di colonne</span><span class="sxs-lookup"><span data-stu-id="6632e-181">HBaseTableColumnFamily: The column family name</span></span>

     ![Finestra di dialogo delle impostazioni di connessione](./media/hdinsight-storm-correlation-topology/settings.png)

4. <span data-ttu-id="6632e-183">Eseguire la soluzione.</span><span class="sxs-lookup"><span data-stu-id="6632e-183">Run the solution.</span></span> <span data-ttu-id="6632e-184">Quando richiesto, selezionare il tasto 'C' per creare la tabella nel cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="6632e-184">When prompted, select the 'c' key to create the table on your HBase cluster.</span></span>

## <a name="build-and-deploy-the-storm-topology"></a><span data-ttu-id="6632e-185">Compilare e distribuire la topologia di Storm</span><span class="sxs-lookup"><span data-stu-id="6632e-185">Build and deploy the Storm topology</span></span>

1. <span data-ttu-id="6632e-186">Aprire la soluzione **CorrelationTopology** in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6632e-186">Open the **CorrelationTopology** solution in Visual Studio.</span></span>

2. <span data-ttu-id="6632e-187">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **CorrelationTopology** e quindi scegliere Proprietà.</span><span class="sxs-lookup"><span data-stu-id="6632e-187">In **Solution Explorer**, right-click the **CorrelationTopology** project and select properties.</span></span>

3. <span data-ttu-id="6632e-188">Nella finestra Proprietà selezionare **Impostazioni** e immettere i valori di configurazione per questo progetto.</span><span class="sxs-lookup"><span data-stu-id="6632e-188">In the properties window, select **Settings** and enter the configuration values for this project.</span></span> <span data-ttu-id="6632e-189">I primi cinque sono gli stessi valori usati dal progetto **SessionInfo**:</span><span class="sxs-lookup"><span data-stu-id="6632e-189">The first 5 are the same values used by the **SessionInfo** project:</span></span>

   * <span data-ttu-id="6632e-190">HBaseClusterURL: l'URL del cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="6632e-190">HBaseClusterURL: the URL to your HBase cluster.</span></span> <span data-ttu-id="6632e-191">Ad esempio, https://myhbasecluster.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="6632e-191">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="6632e-192">HBaseClusterUserName: l'account amministratore/utente HTTP per il cluster.</span><span class="sxs-lookup"><span data-stu-id="6632e-192">HBaseClusterUserName: the admin/HTTP user account for your cluster.</span></span>

   * <span data-ttu-id="6632e-193">HBaseClusterPassword: la password per l'account amministratore/utente HTTP.</span><span class="sxs-lookup"><span data-stu-id="6632e-193">HBaseClusterPassword: the password for the admin/HTTP user account.</span></span>

   * <span data-ttu-id="6632e-194">HBaseTableName: il nome della tabella da utilizzare in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="6632e-194">HBaseTableName: the name of the table to use with this example.</span></span> <span data-ttu-id="6632e-195">Questo valore deve corrispondere al nome di tabella usato nel progetto SessionInfo.</span><span class="sxs-lookup"><span data-stu-id="6632e-195">This value is the same table name as used in the SessionInfo project.</span></span>

   * <span data-ttu-id="6632e-196">HBaseTableColumnFamily: il nome di famiglia di colonne.</span><span class="sxs-lookup"><span data-stu-id="6632e-196">HBaseTableColumnFamily: The column family name.</span></span> <span data-ttu-id="6632e-197">Questo valore deve corrispondere al nome di famiglia di colonne usato nel progetto SessionInfo.</span><span class="sxs-lookup"><span data-stu-id="6632e-197">This value is the same column family name as used in the SessionInfo project.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="6632e-198">Non modificare HBaseTableColumnNames, poiché i valori predefiniti sono i nomi utilizzati da **SessionInfo** per recuperare i dati.</span><span class="sxs-lookup"><span data-stu-id="6632e-198">Do not change the HBaseTableColumnNames, as the defaults are the names used by **SessionInfo** to retrieve data.</span></span>

4. <span data-ttu-id="6632e-199">Salvare le proprietà, quindi compilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="6632e-199">Save the properties, then build the project.</span></span>

5. <span data-ttu-id="6632e-200">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto e scegliere **Submit to Storm on HDInsight** (Invia a Storm in HDInsight).</span><span class="sxs-lookup"><span data-stu-id="6632e-200">In **Solution Explorer**, right-click the project and select **Submit to Storm on HDInsight**.</span></span> <span data-ttu-id="6632e-201">Se richiesto, immettere le credenziali per la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6632e-201">If prompted, enter the credentials for your Azure subscription.</span></span>

   ![Immagine della voce di menu Submit to Storm](./media/hdinsight-storm-correlation-topology/submittostorm.png)

6. <span data-ttu-id="6632e-203">Nella finestra di dialogo **Submit Topology** (Invia topologia) selezionare il cluster Storm in cui distribuire questa topologia.</span><span class="sxs-lookup"><span data-stu-id="6632e-203">In the **Submit Topology** dialog, select the Storm cluster you want to deploy this topology to.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6632e-204">La prima volta che si invia una topologia potrebbe richiedere alcuni secondi per recuperare il nome dei cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6632e-204">The first time you submit a topology, it may take a few seconds to retrieve the name of your HDInsight clusters.</span></span>

7. <span data-ttu-id="6632e-205">Dopo che la topologia è stata caricata e inviata al cluster, la finestra **Storm Topology View** (Visualizzazione topologia Storm) si apre e visualizza la topologia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="6632e-205">Once the topology has been uploaded and submitted to the cluster, the **Storm Topology View** opens and displays the running topology.</span></span> <span data-ttu-id="6632e-206">Per aggiornare i dati, selezionare **CorrelationTopology** e usare il pulsante di aggiornamento nella parte superiore destra della pagina.</span><span class="sxs-lookup"><span data-stu-id="6632e-206">To refresh the data, select the **CorrelationTopology** and use the refresh button at the top right of the page.</span></span>

   ![Immagine della visualizzazione topologia](./media/hdinsight-storm-correlation-topology/topologyview.png)

   <span data-ttu-id="6632e-208">Quando la topologia inizia la generazione di dati, il valore nella colonna **Emitted** (Emesso) aumenta.</span><span class="sxs-lookup"><span data-stu-id="6632e-208">When the topology begins generating data, the value in the **Emitted** column increments.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6632e-209">Se la finestra **Storm Topology View** non veniva visualizzato automaticamente, utilizzare i passaggi seguenti per aprirlo:</span><span class="sxs-lookup"><span data-stu-id="6632e-209">If the **Storm Topology View** does not open automatically, use the following steps to open it:</span></span>
   >
   > 1. <span data-ttu-id="6632e-210">Da **Esplora soluzioni** espandere **Azure**, quindi **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="6632e-210">In **Solution Explorer**, expand **Azure**, and then expand **HDInsight**.</span></span>
   > 2. <span data-ttu-id="6632e-211">Fare clic con il pulsante destro del mouse sul cluster di Storm su cui è in esecuzione la topologia e quindi scegliere **View Storm Topologies** (Visualizza topologie Storm).</span><span class="sxs-lookup"><span data-stu-id="6632e-211">Right-click the Storm cluster that the topology is running on, and then select **View Storm Topologies**</span></span>

## <a name="query-the-data"></a><span data-ttu-id="6632e-212">Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="6632e-212">Query the data</span></span>

<span data-ttu-id="6632e-213">Una volta generati i dati, utilizzare la procedura seguente per eseguire query sui dati.</span><span class="sxs-lookup"><span data-stu-id="6632e-213">Once data has been emitted, use the following steps to query the data.</span></span>

1. <span data-ttu-id="6632e-214">Tornare al progetto **SessionInfo** .</span><span class="sxs-lookup"><span data-stu-id="6632e-214">Return to the **SessionInfo** project.</span></span> <span data-ttu-id="6632e-215">Se non in esecuzione, avviare una nuova istanza.</span><span class="sxs-lookup"><span data-stu-id="6632e-215">If not running, start a new instance of it.</span></span>

2. <span data-ttu-id="6632e-216">Quando richiesto, selezionare **S** per la ricerca dell'evento START.</span><span class="sxs-lookup"><span data-stu-id="6632e-216">When prompted, select **s** to search for START event.</span></span> <span data-ttu-id="6632e-217">Viene richiesto di immettere un'ora di inizio e fine per definire un intervallo di tempo; vengono restituiti solo gli eventi che si sono verificati all'interno di questo intervallo.</span><span class="sxs-lookup"><span data-stu-id="6632e-217">You are prompted to enter a start and end time to define a time range - only events between these two times are returned.</span></span>

    <span data-ttu-id="6632e-218">Utilizzare i seguenti formati quando si immette l'ora di inizio e fine: HH:MM e 'M'' e 'am' o 'pm'.</span><span class="sxs-lookup"><span data-stu-id="6632e-218">Use the following format when entering the start and end times: HH:MM and 'am' or 'pm'.</span></span> <span data-ttu-id="6632e-219">Ad esempio, 11:20 pm.</span><span class="sxs-lookup"><span data-stu-id="6632e-219">For example, 11:20pm.</span></span>

    <span data-ttu-id="6632e-220">Per tornare agli eventi registrati, usare una data di inizio precedente alla distribuzione della topologia Storm e un'ora di fine corrispondente all'ora attuale.</span><span class="sxs-lookup"><span data-stu-id="6632e-220">To return logged events, use a start time from before the Storm topology was deployed, and an end time of now.</span></span> <span data-ttu-id="6632e-221">I dati restituiti contengano voci simili al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="6632e-221">The return data contains entries similar to the following text:</span></span>

        Session e6992b3e-79be-4991-afcf-5cb47dd1c81c started at 6/5/2015 6:10:15 PM. Timestamp = 1433527820737

<span data-ttu-id="6632e-222">La ricerca degli eventi END funziona come gli eventi START.</span><span class="sxs-lookup"><span data-stu-id="6632e-222">Searching for END events works the same as START events.</span></span> <span data-ttu-id="6632e-223">Tuttavia, gli eventi END vengono generati in modo casuale in un tempo compreso tra 1 e 5 minuti dopo l'evento START.</span><span class="sxs-lookup"><span data-stu-id="6632e-223">However, END events are generated randomly between 1 and 5 minutes after the START event.</span></span> <span data-ttu-id="6632e-224">Può essere necessario provare alcuni intervalli di tempo per trovare gli eventi END.</span><span class="sxs-lookup"><span data-stu-id="6632e-224">You may have to try a few time ranges to find the END events.</span></span> <span data-ttu-id="6632e-225">Gli eventi END contengono anche la durata della sessione, ovvero la differenza tra l'ora dell'evento START e l'ora dell'evento END.</span><span class="sxs-lookup"><span data-stu-id="6632e-225">END events also contain the duration of the session - the difference between the START event time and END event time.</span></span> <span data-ttu-id="6632e-226">Di seguito è riportato un esempio di dati per gli eventi END:</span><span class="sxs-lookup"><span data-stu-id="6632e-226">Here is an example of data for END events:</span></span>

    Session fc9fa8e6-6892-4073-93b3-a587040d892e lasted 2 minutes, and ended at 6/5/2015 6:12:15 PM

> [!NOTE]
> <span data-ttu-id="6632e-227">Sebbene i valori orari immessi siano indicati nell'ora locale, l'ora restituita dalla query è in UTC.</span><span class="sxs-lookup"><span data-stu-id="6632e-227">While the time values you enter are in local time, the time returned from the query is in UTC.</span></span>

## <a name="stop-the-topology"></a><span data-ttu-id="6632e-228">Arrestare la topologia</span><span class="sxs-lookup"><span data-stu-id="6632e-228">Stop the topology</span></span>

<span data-ttu-id="6632e-229">Quando si è pronti per arrestare la topologia, tornare al progetto **CorrelationTopology** in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6632e-229">When you are ready to stop the topology, return to the **CorrelationTopology** project in Visual Studio.</span></span> <span data-ttu-id="6632e-230">Nella finestra **Storm Topology View** selezionare la topologia quindi utilizzare il pulsante **Kill** nella parte superiore della visualizzazione topologia.</span><span class="sxs-lookup"><span data-stu-id="6632e-230">In the **Storm Topology View**, select the topology and then use the **Kill** button at the top of the topology view.</span></span>

## <a name="delete-your-cluster"></a><span data-ttu-id="6632e-231">Eliminare il cluster</span><span class="sxs-lookup"><span data-stu-id="6632e-231">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="6632e-232">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6632e-232">Next steps</span></span>

<span data-ttu-id="6632e-233">Per altri esempi di Storm, vedere [Topologie di esempio per Storm in HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="6632e-233">For more Storm examples, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
