---
title: eventi aaaCorrelate nel tempo con Storm e HBase in HDInsight
description: Informazioni su come toocorrelate eventi che arrivano in momenti diversi tramite Storm e HBase in HDInsight.
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
ms.openlocfilehash: f915eef77bbda5b02bfd02ad0b5a4923ff2f4f26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="correlate-events-that-arrive-at-different-times-using-storm-and-hbase"></a><span data-ttu-id="037e9-103">Correlare eventi che arrivano in momenti diversi tramite Storm e HBase</span><span class="sxs-lookup"><span data-stu-id="037e9-103">Correlate events that arrive at different times using Storm and HBase</span></span>

<span data-ttu-id="037e9-104">Utilizzando un archivio dati permanente con Apache Storm, è possibile correlare le voci di dati che arrivano in momenti diversi.</span><span class="sxs-lookup"><span data-stu-id="037e9-104">By using a persistent data store with Apache Storm, you can correlate data entries that arrive at different times.</span></span> <span data-ttu-id="037e9-105">Ad esempio, collegamento eventi di accesso e disconnessione per un toocalculate sessione utente come sessione hello di lunga durata.</span><span class="sxs-lookup"><span data-stu-id="037e9-105">For example, linking login and logout events for a user session toocalculate how long hello session lasted.</span></span>

<span data-ttu-id="037e9-106">Nel presente documento, si apprenderà come toocreate una topologia c# tempesta di base che tiene traccia di eventi di accesso e disconnessione per le sessioni utente e viene calcolata hello durata della sessione hello.</span><span class="sxs-lookup"><span data-stu-id="037e9-106">In this document, you learn how toocreate a basic C# Storm topology that tracks login and logout events for user sessions, and calculates hello duration of hello session.</span></span> <span data-ttu-id="037e9-107">topologia di Hello utilizza HBase come archivio dati persistente.</span><span class="sxs-lookup"><span data-stu-id="037e9-107">hello topology uses HBase as a persistent data store.</span></span> <span data-ttu-id="037e9-108">HBase consente inoltre query batch tooperform nella raccolta di informazioni aggiuntive hello dati cronologici tooproduce.</span><span class="sxs-lookup"><span data-stu-id="037e9-108">HBase also allows you tooperform batch queries on hello historical data tooproduce additional insights.</span></span> <span data-ttu-id="037e9-109">ad esempio il numero di sessioni utente avviate o terminate in un determinato periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="037e9-109">For example, how many user sessions were started or ended during a specific time period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="037e9-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="037e9-110">Prerequisites</span></span>

* <span data-ttu-id="037e9-111">Visual Studio e hello gli strumenti HDInsight per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="037e9-111">Visual Studio and hello HDInsight tools for Visual Studio.</span></span> <span data-ttu-id="037e9-112">Per ulteriori informazioni, vedere [iniziare a usare gli strumenti di HDInsight hello per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="037e9-112">For more information, see [Get started using hello HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="037e9-113">Cluster Apache Storm in HDInsight, basato su Windows.</span><span class="sxs-lookup"><span data-stu-id="037e9-113">Apache Storm on HDInsight cluster (Windows-based).</span></span>

  > [!WARNING]
  > <span data-ttu-id="037e9-114">Mentre SCP.NET topologie sono supportate nei cluster basati su Linux Storm creato dopo il 10/28/2016, hello HBase SDK per il pacchetto .NET disponibile a partire da 28/10/2016 non funziona correttamente in HDInsight basati su Linux</span><span class="sxs-lookup"><span data-stu-id="037e9-114">While SCP.NET topologies are supported on Linux-based Storm clusters created after 10/28/2016, hello HBase SDK for .NET package available as of 10/28/2016 does not work correctly on Linux-based HDInsight</span></span>

* <span data-ttu-id="037e9-115">Cluster Apache HBase in HDInsight, basato su Linux o su Windows.</span><span class="sxs-lookup"><span data-stu-id="037e9-115">Apache HBase on HDInsight cluster (Linux or Windows-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="037e9-116">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="037e9-116">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="037e9-117">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="037e9-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="037e9-118">[Java](https://java.com) 1.7 o versione successiva nell'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="037e9-118">[Java](https://java.com) 1.7 or greater on your development environment.</span></span> <span data-ttu-id="037e9-119">Java è topologia hello toopackage utilizzato quando è cluster HDInsight toohello inviato.</span><span class="sxs-lookup"><span data-stu-id="037e9-119">Java is used toopackage hello topology when it is submitted toohello HDInsight cluster.</span></span>

  * <span data-ttu-id="037e9-120">Hello **JAVA_HOME** directory di toohello punto deve variabile di ambiente contenente Java.</span><span class="sxs-lookup"><span data-stu-id="037e9-120">hello **JAVA_HOME** environment variable must point toohello directory that contains Java.</span></span>
  * <span data-ttu-id="037e9-121">Hello **%JAVA_HOME%/bin** directory deve trovarsi nel percorso hello</span><span class="sxs-lookup"><span data-stu-id="037e9-121">hello **%JAVA_HOME%/bin** directory must be in hello path</span></span>

## <a name="architecture"></a><span data-ttu-id="037e9-122">Architettura</span><span class="sxs-lookup"><span data-stu-id="037e9-122">Architecture</span></span>

![Diagramma di flusso di dati hello attraverso topologia hello](./media/hdinsight-storm-correlation-topology/correlationtopology.png)

<span data-ttu-id="037e9-124">Correlazione di eventi, è necessario un identificatore comune per l'origine evento hello.</span><span class="sxs-lookup"><span data-stu-id="037e9-124">Correlating events requires a common identifier for hello event source.</span></span> <span data-ttu-id="037e9-125">Ad esempio, un ID utente, ID di sessione o altro dato che è un) univoci e b) incluso in tutti i dati inviati tooStorm.</span><span class="sxs-lookup"><span data-stu-id="037e9-125">For example, a user ID, session ID, or other piece of data that is a) unique and b) included in all data sent tooStorm.</span></span> <span data-ttu-id="037e9-126">Questo esempio viene utilizzato un toorepresent valore GUID un ID sessione.</span><span class="sxs-lookup"><span data-stu-id="037e9-126">This example uses a GUID value toorepresent a session ID.</span></span>

<span data-ttu-id="037e9-127">Questo esempio è costituito da due cluster di HDInsight:</span><span class="sxs-lookup"><span data-stu-id="037e9-127">This example consists of two HDInsight clusters:</span></span>

* <span data-ttu-id="037e9-128">HBase: archivio dati permanente per i dati cronologici</span><span class="sxs-lookup"><span data-stu-id="037e9-128">HBase: persistent data store for historical data</span></span>
* <span data-ttu-id="037e9-129">Storm: utilizzare i dati in arrivo tooingest</span><span class="sxs-lookup"><span data-stu-id="037e9-129">Storm: used tooingest incoming data</span></span>

<span data-ttu-id="037e9-130">dati Hello viene generati in modo casuale dalla topologia Storm hello ed è costituito da hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="037e9-130">hello data is randomly generated by hello Storm topology, and consists of hello following items:</span></span>

* <span data-ttu-id="037e9-131">ID di sessione: un GUID che identifica in modo univoco ogni sessione</span><span class="sxs-lookup"><span data-stu-id="037e9-131">Session ID: a GUID that uniquely identifies each session</span></span>
* <span data-ttu-id="037e9-132">Evento: un evento START o END.</span><span class="sxs-lookup"><span data-stu-id="037e9-132">Event: a START or END event.</span></span> <span data-ttu-id="037e9-133">Per questo esempio, l'evento START si verifica sempre prima dell'evento END</span><span class="sxs-lookup"><span data-stu-id="037e9-133">For this example, START always occurs before END</span></span>
* <span data-ttu-id="037e9-134">Ora: hello ora di hello evento.</span><span class="sxs-lookup"><span data-stu-id="037e9-134">Time: hello time of hello event.</span></span>

<span data-ttu-id="037e9-135">Questi dati vengono elaborati e archiviati in HBase.</span><span class="sxs-lookup"><span data-stu-id="037e9-135">This data is processed and stored in HBase.</span></span>

### <a name="storm-topology"></a><span data-ttu-id="037e9-136">Topologia Storm</span><span class="sxs-lookup"><span data-stu-id="037e9-136">Storm topology</span></span>

<span data-ttu-id="037e9-137">Quando si avvia una sessione, un **avviare** evento viene ricevuto dalla topologia hello e registrato tooHBase.</span><span class="sxs-lookup"><span data-stu-id="037e9-137">When a session starts, a **START** event is received by hello topology and logged tooHBase.</span></span> <span data-ttu-id="037e9-138">Quando un **fine** viene ricevuto l'evento, la topologia hello recupera hello **avviare** evento e calcola il tempo di hello tra gli eventi di hello due.</span><span class="sxs-lookup"><span data-stu-id="037e9-138">When an **END** event is received, hello topology retrieves hello **START** event and calculates hello time between hello two events.</span></span> <span data-ttu-id="037e9-139">Questo **durata** valore verrà quindi archiviato in HBase insieme hello **fine** informazioni sull'evento.</span><span class="sxs-lookup"><span data-stu-id="037e9-139">This **Duration** value is then stored in HBase along with hello **END** event information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="037e9-140">Durante questa topologia illustra modello di base hello, una soluzione di produzione sarà necessario progettazione tootake per hello seguenti scenari:</span><span class="sxs-lookup"><span data-stu-id="037e9-140">While this topology demonstrates hello basic pattern, a production solution would need tootake design for hello following scenarios:</span></span>
>
> * <span data-ttu-id="037e9-141">Eventi che arrivano nell'ordine errato</span><span class="sxs-lookup"><span data-stu-id="037e9-141">Events arriving out of order</span></span>
> * <span data-ttu-id="037e9-142">Eventi duplicati</span><span class="sxs-lookup"><span data-stu-id="037e9-142">Duplicate events</span></span>
> * <span data-ttu-id="037e9-143">Eventi eliminati</span><span class="sxs-lookup"><span data-stu-id="037e9-143">Dropped events</span></span>

<span data-ttu-id="037e9-144">topologia di esempio Hello è costituita da hello seguenti componenti:</span><span class="sxs-lookup"><span data-stu-id="037e9-144">hello sample topology is composed of hello following components:</span></span>

* <span data-ttu-id="037e9-145">Session.cs: simula una sessione utente tramite la creazione di un ID di sessione casuale, inizio hello tempo e la durata della sessione hanno una durata.</span><span class="sxs-lookup"><span data-stu-id="037e9-145">Session.cs: simulates a user session by creating a random session ID, start time, and how long hello session lasts.</span></span>

* <span data-ttu-id="037e9-146">Spout.cs: crea 100 sessioni, genera un evento di inizio, hello casuale timeout in attesa per ogni sessione e quindi genera un evento di fine.</span><span class="sxs-lookup"><span data-stu-id="037e9-146">Spout.cs: creates 100 sessions, emits a START event, waits hello random timeout for each session, and then emits an END event.</span></span> <span data-ttu-id="037e9-147">Quindi ricicli terminata sessioni toogenerate nuovi.</span><span class="sxs-lookup"><span data-stu-id="037e9-147">Then recycles ended sessions toogenerate new ones.</span></span>

* <span data-ttu-id="037e9-148">HBaseLookupBolt.cs: Usa toolook ID di sessione hello le informazioni di sessione da HBase.</span><span class="sxs-lookup"><span data-stu-id="037e9-148">HBaseLookupBolt.cs: uses hello session ID toolook up session information from HBase.</span></span> <span data-ttu-id="037e9-149">Quando viene elaborato un evento di fine, trova hello corrispondente evento di inizio e hello durata della sessione hello viene calcolata.</span><span class="sxs-lookup"><span data-stu-id="037e9-149">When an END event is processed, it finds hello corresponding START event and calculates hello duration of hello session.</span></span>

* <span data-ttu-id="037e9-150">HBaseBolt.cs: archivia le informazioni in HBase.</span><span class="sxs-lookup"><span data-stu-id="037e9-150">HBaseBolt.cs: Stores information into HBase.</span></span>

* <span data-ttu-id="037e9-151">TypeHelper.cs: Consente con conversione del tipo durante la lettura / scrittura tooHBase.</span><span class="sxs-lookup"><span data-stu-id="037e9-151">TypeHelper.cs: Helps with type conversion when reading from/writing tooHBase.</span></span>

### <a name="hbase-schema"></a><span data-ttu-id="037e9-152">Schema HBase</span><span class="sxs-lookup"><span data-stu-id="037e9-152">HBase schema</span></span>

<span data-ttu-id="037e9-153">In HBase, hello vengono archiviati in una tabella con hello/impostazioni di schema seguente:</span><span class="sxs-lookup"><span data-stu-id="037e9-153">In HBase, hello data is stored in a table with hello following schema/settings:</span></span>

* <span data-ttu-id="037e9-154">Chiave di riga: hello ID sessione è usato come chiave hello per le righe in questa tabella.</span><span class="sxs-lookup"><span data-stu-id="037e9-154">Row key: hello session ID is used as hello key for rows in this table.</span></span>

* <span data-ttu-id="037e9-155">Famiglia di colonna: nome della famiglia hello è 'cf'.</span><span class="sxs-lookup"><span data-stu-id="037e9-155">Column family: hello family name is 'cf'.</span></span> <span data-ttu-id="037e9-156">Le colonne memorizzate in questo gruppo sono le seguenti:</span><span class="sxs-lookup"><span data-stu-id="037e9-156">Columns stored in this family are:</span></span>

  * <span data-ttu-id="037e9-157">event: START o END.</span><span class="sxs-lookup"><span data-stu-id="037e9-157">event: START or END.</span></span>

  * <span data-ttu-id="037e9-158">ora: si è verificato il tempo di hello in millisecondi che hello evento.</span><span class="sxs-lookup"><span data-stu-id="037e9-158">time: hello time in milliseconds that hello event occurred.</span></span>

  * <span data-ttu-id="037e9-159">durata: hello di lunghezza compresa tra eventi di inizio e di fine.</span><span class="sxs-lookup"><span data-stu-id="037e9-159">duration: hello length between START and END event.</span></span>

* <span data-ttu-id="037e9-160">Le versioni: famiglia 'cf' hello è impostata tooretain 5 versioni di ogni riga.</span><span class="sxs-lookup"><span data-stu-id="037e9-160">VERSIONS: hello 'cf' family is set tooretain 5 versions of each row.</span></span>

  > [!NOTE]
  > <span data-ttu-id="037e9-161">Le versioni sono un registro dei valori precedentemente memorizzati per una chiave di riga specifica.</span><span class="sxs-lookup"><span data-stu-id="037e9-161">Versions are a log of previous values stored for a specific row key.</span></span> <span data-ttu-id="037e9-162">Per impostazione predefinita, HBase restituisce solo il valore di hello per la versione più recente di hello di una riga.</span><span class="sxs-lookup"><span data-stu-id="037e9-162">By default, HBase only returns hello value for hello most recent version of a row.</span></span> <span data-ttu-id="037e9-163">In questo caso, hello stessa riga viene utilizzata per tutti gli eventi (inizio, fine) ogni versione di una riga viene identificato dal valore di timestamp hello.</span><span class="sxs-lookup"><span data-stu-id="037e9-163">In this case, hello same row is used for all events (START, END.) each version of a row is identified by hello timestamp value.</span></span> <span data-ttu-id="037e9-164">Le versioni forniscono una visualizzazione cronologica degli eventi registrati per un ID specifico.</span><span class="sxs-lookup"><span data-stu-id="037e9-164">Versions provide a historical view of events logged for a specific ID.</span></span>

## <a name="download-hello-project"></a><span data-ttu-id="037e9-165">Scaricare il progetto hello</span><span class="sxs-lookup"><span data-stu-id="037e9-165">Download hello project</span></span>

<span data-ttu-id="037e9-166">progetto di esempio Hello può essere scaricato da [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span><span class="sxs-lookup"><span data-stu-id="037e9-166">hello sample project can be downloaded from [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span></span>

<span data-ttu-id="037e9-167">Questo download contiene hello c# progetti seguenti:</span><span class="sxs-lookup"><span data-stu-id="037e9-167">This download contains hello following C# projects:</span></span>

* <span data-ttu-id="037e9-168">CorrelationTopology: topologia Storm di C# che casualmente genera eventi di inizio e di fine per le sessioni utente.</span><span class="sxs-lookup"><span data-stu-id="037e9-168">CorrelationTopology: C# Storm topology that randomly emits start and end events for user sessions.</span></span> <span data-ttu-id="037e9-169">La durata di ogni sessione è compresa tra 1 e 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="037e9-169">Each session lasts between 1 and 5 minutes.</span></span>

* <span data-ttu-id="037e9-170">SessionInfo: Applicazione console c# che crea una tabella HBase hello e fornisce query di esempio tooreturn informazioni sui dati di sessione.</span><span class="sxs-lookup"><span data-stu-id="037e9-170">SessionInfo: C# console application that creates hello HBase table, and provides example queries tooreturn information about stored session data.</span></span>

## <a name="create-hello-table"></a><span data-ttu-id="037e9-171">Creare la tabella hello</span><span class="sxs-lookup"><span data-stu-id="037e9-171">Create hello table</span></span>

1. <span data-ttu-id="037e9-172">Aprire hello **SessionInfo** progetto in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="037e9-172">Open hello **SessionInfo** project in Visual Studio.</span></span>

2. <span data-ttu-id="037e9-173">In **Esplora**, hello rapida **SessionInfo** del progetto e selezionare **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="037e9-173">In **Solution Explorer**, right-click hello **SessionInfo** project and select **Properties**.</span></span>

    ![Schermata del menu con le proprietà selezionate](./media/hdinsight-storm-correlation-topology/selectproperties.png)

3. <span data-ttu-id="037e9-175">Selezionare **impostazioni**, quindi hello set seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="037e9-175">Select **Settings**, then set hello following values:</span></span>

   * <span data-ttu-id="037e9-176">HBaseClusterURL: cluster di HBase tooyour URL hello.</span><span class="sxs-lookup"><span data-stu-id="037e9-176">HBaseClusterURL: hello URL tooyour HBase cluster.</span></span> <span data-ttu-id="037e9-177">Ad esempio, https://myhbasecluster.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="037e9-177">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="037e9-178">HBaseClusterUserName: account utente di amministrazione/HTTP hello per il cluster</span><span class="sxs-lookup"><span data-stu-id="037e9-178">HBaseClusterUserName: hello admin/HTTP user account for your cluster</span></span>

   * <span data-ttu-id="037e9-179">HBaseClusterPassword: password di hello per l'account utente di amministrazione/HTTP hello</span><span class="sxs-lookup"><span data-stu-id="037e9-179">HBaseClusterPassword: hello password for hello admin/HTTP user account</span></span>

   * <span data-ttu-id="037e9-180">HBaseTableName: nome di hello hello tabella toouse con questo esempio</span><span class="sxs-lookup"><span data-stu-id="037e9-180">HBaseTableName: hello name of hello table toouse with this example</span></span>

   * <span data-ttu-id="037e9-181">HBaseTableColumnFamily: nome della famiglia colonna hello</span><span class="sxs-lookup"><span data-stu-id="037e9-181">HBaseTableColumnFamily: hello column family name</span></span>

     ![Finestra di dialogo delle impostazioni di connessione](./media/hdinsight-storm-correlation-topology/settings.png)

4. <span data-ttu-id="037e9-183">Eseguire la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="037e9-183">Run hello solution.</span></span> <span data-ttu-id="037e9-184">Quando richiesto, selezionare una tabella di hello toocreate chiave "c" hello sul cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="037e9-184">When prompted, select hello 'c' key toocreate hello table on your HBase cluster.</span></span>

## <a name="build-and-deploy-hello-storm-topology"></a><span data-ttu-id="037e9-185">Compilare e distribuire una topologia di Storm hello</span><span class="sxs-lookup"><span data-stu-id="037e9-185">Build and deploy hello Storm topology</span></span>

1. <span data-ttu-id="037e9-186">Aprire hello **CorrelationTopology** soluzione in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="037e9-186">Open hello **CorrelationTopology** solution in Visual Studio.</span></span>

2. <span data-ttu-id="037e9-187">In **Esplora**, hello rapida **CorrelationTopology** del progetto e scegliere Proprietà.</span><span class="sxs-lookup"><span data-stu-id="037e9-187">In **Solution Explorer**, right-click hello **CorrelationTopology** project and select properties.</span></span>

3. <span data-ttu-id="037e9-188">Nella finestra Proprietà hello selezionare **impostazioni** e immettere i valori di configurazione hello per questo progetto.</span><span class="sxs-lookup"><span data-stu-id="037e9-188">In hello properties window, select **Settings** and enter hello configuration values for this project.</span></span> <span data-ttu-id="037e9-189">primi 5 Hello sono hello stessi valori utilizzati per hello **SessionInfo** progetto:</span><span class="sxs-lookup"><span data-stu-id="037e9-189">hello first 5 are hello same values used by hello **SessionInfo** project:</span></span>

   * <span data-ttu-id="037e9-190">HBaseClusterURL: cluster di HBase tooyour URL hello.</span><span class="sxs-lookup"><span data-stu-id="037e9-190">HBaseClusterURL: hello URL tooyour HBase cluster.</span></span> <span data-ttu-id="037e9-191">Ad esempio, https://myhbasecluster.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="037e9-191">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="037e9-192">HBaseClusterUserName: hello admin/HTTP account utente per il cluster.</span><span class="sxs-lookup"><span data-stu-id="037e9-192">HBaseClusterUserName: hello admin/HTTP user account for your cluster.</span></span>

   * <span data-ttu-id="037e9-193">HBaseClusterPassword: password di hello per l'account utente di amministrazione/HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="037e9-193">HBaseClusterPassword: hello password for hello admin/HTTP user account.</span></span>

   * <span data-ttu-id="037e9-194">HBaseTableName: hello Nome hello tabella toouse con questo esempio.</span><span class="sxs-lookup"><span data-stu-id="037e9-194">HBaseTableName: hello name of hello table toouse with this example.</span></span> <span data-ttu-id="037e9-195">Questo valore è hello stesso nome di tabella utilizzato nel progetto SessionInfo hello.</span><span class="sxs-lookup"><span data-stu-id="037e9-195">This value is hello same table name as used in hello SessionInfo project.</span></span>

   * <span data-ttu-id="037e9-196">HBaseTableColumnFamily: nome della famiglia hello colonna.</span><span class="sxs-lookup"><span data-stu-id="037e9-196">HBaseTableColumnFamily: hello column family name.</span></span> <span data-ttu-id="037e9-197">Questo valore è hello stesso nome della famiglia di colonna utilizzato nel progetto SessionInfo hello.</span><span class="sxs-lookup"><span data-stu-id="037e9-197">This value is hello same column family name as used in hello SessionInfo project.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="037e9-198">Non modificare hello HBaseTableColumnNames, come valori predefiniti di hello sono nomi hello utilizzati dal **SessionInfo** tooretrieve dati.</span><span class="sxs-lookup"><span data-stu-id="037e9-198">Do not change hello HBaseTableColumnNames, as hello defaults are hello names used by **SessionInfo** tooretrieve data.</span></span>

4. <span data-ttu-id="037e9-199">Salvare le proprietà di hello, quindi compilare il progetto hello.</span><span class="sxs-lookup"><span data-stu-id="037e9-199">Save hello properties, then build hello project.</span></span>

5. <span data-ttu-id="037e9-200">In **Esplora**, fare clic sul progetto hello e selezionare **inviare tooStorm in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="037e9-200">In **Solution Explorer**, right-click hello project and select **Submit tooStorm on HDInsight**.</span></span> <span data-ttu-id="037e9-201">Se richiesto, immettere le credenziali di hello per la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="037e9-201">If prompted, enter hello credentials for your Azure subscription.</span></span>

   ![Immagine di hello inviare la voce di menu toostorm](./media/hdinsight-storm-correlation-topology/submittostorm.png)

6. <span data-ttu-id="037e9-203">In hello **inviare topologia** finestra di dialogo, cluster Storm hello selezionare desiderato toodeploy questa topologia.</span><span class="sxs-lookup"><span data-stu-id="037e9-203">In hello **Submit Topology** dialog, select hello Storm cluster you want toodeploy this topology to.</span></span>

   > [!NOTE]
   > <span data-ttu-id="037e9-204">Hello prima volta che si invia una topologia, potrebbe richiedere alcuni secondi nome hello tooretrieve dei cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="037e9-204">hello first time you submit a topology, it may take a few seconds tooretrieve hello name of your HDInsight clusters.</span></span>

7. <span data-ttu-id="037e9-205">Dopo aver caricato e inviato toohello cluster topologia hello, hello **vista topologia Storm** aprirà e visualizzerà hello in esecuzione sulla topologia.</span><span class="sxs-lookup"><span data-stu-id="037e9-205">Once hello topology has been uploaded and submitted toohello cluster, hello **Storm Topology View** opens and displays hello running topology.</span></span> <span data-ttu-id="037e9-206">dati hello toorefresh, seleziona hello **CorrelationTopology** e utilizzare il pulsante di aggiornamento hello hello in alto a destra della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="037e9-206">toorefresh hello data, select hello **CorrelationTopology** and use hello refresh button at hello top right of hello page.</span></span>

   ![Immagine di vista della topologia hello](./media/hdinsight-storm-correlation-topology/topologyview.png)

   <span data-ttu-id="037e9-208">Quando inizia la topologia di hello la generazione di dati, hello valore hello **emessa** colonna viene incrementato.</span><span class="sxs-lookup"><span data-stu-id="037e9-208">When hello topology begins generating data, hello value in hello **Emitted** column increments.</span></span>

   > [!NOTE]
   > <span data-ttu-id="037e9-209">Se hello **vista topologia Storm** non viene aperto automaticamente, usare hello seguendo i passaggi tooopen:</span><span class="sxs-lookup"><span data-stu-id="037e9-209">If hello **Storm Topology View** does not open automatically, use hello following steps tooopen it:</span></span>
   >
   > 1. <span data-ttu-id="037e9-210">Da **Esplora soluzioni** espandere **Azure**, quindi **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="037e9-210">In **Solution Explorer**, expand **Azure**, and then expand **HDInsight**.</span></span>
   > 2. <span data-ttu-id="037e9-211">È in esecuzione nel cluster che hello topologia Storm di hello pulsante destro del mouse e quindi selezionare **visualizzazione Storm topologie**</span><span class="sxs-lookup"><span data-stu-id="037e9-211">Right-click hello Storm cluster that hello topology is running on, and then select **View Storm Topologies**</span></span>

## <a name="query-hello-data"></a><span data-ttu-id="037e9-212">Eseguire query sui dati hello</span><span class="sxs-lookup"><span data-stu-id="037e9-212">Query hello data</span></span>

<span data-ttu-id="037e9-213">Una volta dati sono stato emesso, utilizzare hello passaggi tooquery hello dati seguenti.</span><span class="sxs-lookup"><span data-stu-id="037e9-213">Once data has been emitted, use hello following steps tooquery hello data.</span></span>

1. <span data-ttu-id="037e9-214">Restituire toohello **SessionInfo** progetto.</span><span class="sxs-lookup"><span data-stu-id="037e9-214">Return toohello **SessionInfo** project.</span></span> <span data-ttu-id="037e9-215">Se non in esecuzione, avviare una nuova istanza.</span><span class="sxs-lookup"><span data-stu-id="037e9-215">If not running, start a new instance of it.</span></span>

2. <span data-ttu-id="037e9-216">Quando richiesto, selezionare **s** toosearch per eventi di avvio.</span><span class="sxs-lookup"><span data-stu-id="037e9-216">When prompted, select **s** toosearch for START event.</span></span> <span data-ttu-id="037e9-217">Si tooenter richiesta un inizio e fine ora toodefine un intervallo di tempo, vengono restituiti solo gli eventi tra questi due volte.</span><span class="sxs-lookup"><span data-stu-id="037e9-217">You are prompted tooenter a start and end time toodefine a time range - only events between these two times are returned.</span></span>

    <span data-ttu-id="037e9-218">Seguente hello utilizzare formato quando si immette inizio hello e di fine: hh: mm e 'M'' o 'pm'.</span><span class="sxs-lookup"><span data-stu-id="037e9-218">Use hello following format when entering hello start and end times: HH:MM and 'am' or 'pm'.</span></span> <span data-ttu-id="037e9-219">Ad esempio, 11:20 pm.</span><span class="sxs-lookup"><span data-stu-id="037e9-219">For example, 11:20pm.</span></span>

    <span data-ttu-id="037e9-220">gli eventi tooreturn registrato, viene utilizzato da un'ora di inizio prima hello Storm topologia è stata distribuita e un'ora di fine dell'ora.</span><span class="sxs-lookup"><span data-stu-id="037e9-220">tooreturn logged events, use a start time from before hello Storm topology was deployed, and an end time of now.</span></span> <span data-ttu-id="037e9-221">Restituisce i dati Hello contengano toohello di voci simili seguente testo:</span><span class="sxs-lookup"><span data-stu-id="037e9-221">hello return data contains entries similar toohello following text:</span></span>

        Session e6992b3e-79be-4991-afcf-5cb47dd1c81c started at 6/5/2015 6:10:15 PM. Timestamp = 1433527820737

<span data-ttu-id="037e9-222">Ricerca di hello works gli eventi di fine stesso come eventi di avvio.</span><span class="sxs-lookup"><span data-stu-id="037e9-222">Searching for END events works hello same as START events.</span></span> <span data-ttu-id="037e9-223">Tuttavia, gli eventi di fine vengono generati in modo casuale compreso tra 1 e 5 minuti dopo l'evento di inizio hello.</span><span class="sxs-lookup"><span data-stu-id="037e9-223">However, END events are generated randomly between 1 and 5 minutes after hello START event.</span></span> <span data-ttu-id="037e9-224">È possibile tootry qualche tempo intervalli toofind hello gli eventi di fine.</span><span class="sxs-lookup"><span data-stu-id="037e9-224">You may have tootry a few time ranges toofind hello END events.</span></span> <span data-ttu-id="037e9-225">Inoltre, gli eventi di fine contengano durata hello della sessione hello - differenza hello hello evento ora inizio e fine evento.</span><span class="sxs-lookup"><span data-stu-id="037e9-225">END events also contain hello duration of hello session - hello difference between hello START event time and END event time.</span></span> <span data-ttu-id="037e9-226">Di seguito è riportato un esempio di dati per gli eventi END:</span><span class="sxs-lookup"><span data-stu-id="037e9-226">Here is an example of data for END events:</span></span>

    Session fc9fa8e6-6892-4073-93b3-a587040d892e lasted 2 minutes, and ended at 6/5/2015 6:12:15 PM

> [!NOTE]
> <span data-ttu-id="037e9-227">Anche se si immette i valori di ora hello sono nell'ora locale, ora hello restituito dalla query hello è in UTC.</span><span class="sxs-lookup"><span data-stu-id="037e9-227">While hello time values you enter are in local time, hello time returned from hello query is in UTC.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="037e9-228">Arrestare la topologia hello</span><span class="sxs-lookup"><span data-stu-id="037e9-228">Stop hello topology</span></span>

<span data-ttu-id="037e9-229">Quando si è pronti toostop topologia di hello, restituire toohello **CorrelationTopology** progetto in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="037e9-229">When you are ready toostop hello topology, return toohello **CorrelationTopology** project in Visual Studio.</span></span> <span data-ttu-id="037e9-230">In hello **vista topologia Storm**, selezionare la topologia hello e quindi usare hello **Kill** pulsante nella parte superiore di hello della vista della topologia hello.</span><span class="sxs-lookup"><span data-stu-id="037e9-230">In hello **Storm Topology View**, select hello topology and then use hello **Kill** button at hello top of hello topology view.</span></span>

## <a name="delete-your-cluster"></a><span data-ttu-id="037e9-231">Eliminare il cluster</span><span class="sxs-lookup"><span data-stu-id="037e9-231">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="037e9-232">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="037e9-232">Next steps</span></span>

<span data-ttu-id="037e9-233">Per altri esempi di Storm, vedere [Topologie di esempio per Storm in HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="037e9-233">For more Storm examples, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
