---
title: aaaDeploy e gestire le topologie di Apache Storm in HDInsight basati su Linux | Documenti Microsoft
description: Informazioni su come toodeploy, monitorare e gestire le topologie di Apache Storm tramite Dashboard Storm hello in HDInsight basati su Linux. Utilizzare gli strumenti Hadoop per Visual Studio
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 35086e62-d6d8-4ccf-8cae-00073464a1e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 3a1edb773089cc596fea423710aa88cf83c7b841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-hdinsight"></a><span data-ttu-id="73e86-104">Distribuire e gestire topologie Apache Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="73e86-104">Deploy and manage Apache Storm topologies on HDInsight</span></span>

<span data-ttu-id="73e86-105">In questo documento, nozioni di base hello di gestione e monitoraggio topologie di Storm in esecuzione su Storm nei cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="73e86-105">In this document, learn hello basics of managing and monitoring Storm topologies running on Storm on HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="73e86-106">Hello passaggi in questo articolo richiedono un elevato numero di basati su Linux nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="73e86-106">hello steps in this article require a Linux-based Storm on HDInsight cluster.</span></span> <span data-ttu-id="73e86-107">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="73e86-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="73e86-108">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="73e86-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 
>
> <span data-ttu-id="73e86-109">Per informazioni sulla distribuzione e sul monitoraggio di topologie in HDInsight basato su Windows, vedere [Distribuire e gestire le topologie di Apache Storm in HDInsight basato su Windows](hdinsight-storm-deploy-monitor-topology.md)</span><span class="sxs-lookup"><span data-stu-id="73e86-109">For information on deploying and monitoring topologies on Windows-based HDInsight, see [Deploy and manage Apache Storm topologies on Windows-based HDInsight](hdinsight-storm-deploy-monitor-topology.md)</span></span>


## <a name="prerequisites"></a><span data-ttu-id="73e86-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="73e86-110">Prerequisites</span></span>

* <span data-ttu-id="73e86-111">**Storm basato su Linux in cluster HDInsight**: per i passaggi relativi alla creazione di un cluster, vedere [Introduzione ad Apache Storm in HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) .</span><span class="sxs-lookup"><span data-stu-id="73e86-111">**A Linux-based Storm on HDInsight cluster**: see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) for steps on creating a cluster</span></span>

* <span data-ttu-id="73e86-112">(Facoltativo) **Familiarità con SSH e SCP**: per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="73e86-112">(Optional) **Familiarity with SSH and SCP**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="73e86-113">(Facoltativo) **Visual Studio**: Azure SDK 2.5.1 o versione successiva e hello Data Lake Tools per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="73e86-113">(Optional) **Visual Studio**: Azure SDK 2.5.1 or newer and hello Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="73e86-114">Per altre informazioni, vedere [Introduzione all'uso di Data Lake Tools per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="73e86-114">For more information, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    <span data-ttu-id="73e86-115">Una delle seguenti versioni di Visual Studio hello:</span><span class="sxs-lookup"><span data-stu-id="73e86-115">One of hello following versions of Visual Studio:</span></span>

  * <span data-ttu-id="73e86-116">Visual Studio 2012 con [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="73e86-116">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

  * <span data-ttu-id="73e86-117">Visual Studio 2013 con [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) o [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="73e86-117">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>
  * [<span data-ttu-id="73e86-118">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="73e86-118">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/)

  * <span data-ttu-id="73e86-119">Visual Studio 2015, qualsiasi edizione</span><span class="sxs-lookup"><span data-stu-id="73e86-119">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="73e86-120">Visual Studio 2017, qualsiasi edizione.</span><span class="sxs-lookup"><span data-stu-id="73e86-120">Visual Studio 2017 (any edition).</span></span> <span data-ttu-id="73e86-121">Data Lake Tools per Visual Studio 2017 vengono installati come parte di hello del carico di lavoro di Azure.</span><span class="sxs-lookup"><span data-stu-id="73e86-121">Data Lake Tools for Visual Studio 2017 are installed as part of hello Azure Workload.</span></span>

## <a name="submit-a-topology-visual-studio"></a><span data-ttu-id="73e86-122">Inviare una topologia: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="73e86-122">Submit a topology: Visual Studio</span></span>

<span data-ttu-id="73e86-123">gli strumenti di HDInsight Hello può essere utilizzato toosubmit c# o ibrida topologie tooyour cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="73e86-123">hello HDInsight Tools can be used toosubmit C# or hybrid topologies tooyour Storm cluster.</span></span> <span data-ttu-id="73e86-124">Hello alla procedura seguente usa un'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="73e86-124">hello following steps use a sample application.</span></span> <span data-ttu-id="73e86-125">Per informazioni sulla creazione di propri topologie utilizzando gli strumenti di HDInsight hello, vedere [c# sviluppare topologie in hello HDInsight Tools per Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="73e86-125">For information about creating your own topologies by using hello HDInsight Tools, see [Develop C# topologies using hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

1. <span data-ttu-id="73e86-126">Se non è già installato più recente degli strumenti di Data Lake hello hello per Visual Studio, vedere [iniziare a usare Data Lake Tools per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="73e86-126">If you have not already installed hello latest version of hello Data Lake tools for Visual Studio, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="73e86-127">Hello Data Lake Tools per Visual Studio sono state in precedenza denominato hello HDInsight Tools per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="73e86-127">hello Data Lake Tools for Visual Studio were formerly called hello HDInsight Tools for Visual Studio.</span></span>
    >
    > <span data-ttu-id="73e86-128">Data Lake Tools per Visual Studio sono inclusi in hello __carico di lavoro di Azure__ per Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="73e86-128">Data Lake Tools for Visual Studio are included in hello __Azure Workload__ for Visual Studio 2017.</span></span>

2. <span data-ttu-id="73e86-129">Aprire Visual Studio e selezionare **File** > **Nuovo** > **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="73e86-129">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="73e86-130">In hello **nuovo progetto** finestra di dialogo espandere **installato** > **modelli**, quindi selezionare **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="73e86-130">In hello **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="73e86-131">Selezionare nell'elenco dei modelli di hello **Storm esempio**.</span><span class="sxs-lookup"><span data-stu-id="73e86-131">From hello list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="73e86-132">Nella parte inferiore di hello della finestra di dialogo hello, digitare un nome per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="73e86-132">At hello bottom of hello dialog box, type a name for hello application.</span></span>

    ![immagine](./media/hdinsight-storm-deploy-monitor-topology-linux/sample.png)

4. <span data-ttu-id="73e86-134">In **Esplora**, fare clic sul progetto hello e selezionare **inviare tooStorm in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="73e86-134">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="73e86-135">Se richiesto, immettere le credenziali di accesso hello per la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="73e86-135">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="73e86-136">Se si dispone di più di una sottoscrizione, accedere toohello uno che contiene l'elevato numero di cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="73e86-136">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="73e86-137">Selezionare l'elevato numero di cluster HDInsight da hello **Cluster Storm** elenco a discesa e quindi selezionare **Invia**.</span><span class="sxs-lookup"><span data-stu-id="73e86-137">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="73e86-138">È possibile controllare se l'invio di hello ha esito positivo tramite hello **Output** finestra.</span><span class="sxs-lookup"><span data-stu-id="73e86-138">You can monitor whether hello submission is successful by using hello **Output** window.</span></span>

## <a name="submit-a-topology-ssh-and-hello-storm-command"></a><span data-ttu-id="73e86-139">Inviare una topologia: SSH e hello Storm comando</span><span class="sxs-lookup"><span data-stu-id="73e86-139">Submit a topology: SSH and hello Storm command</span></span>

1. <span data-ttu-id="73e86-140">Utilizzare cluster di HDInsight toohello tooconnect SSH.</span><span class="sxs-lookup"><span data-stu-id="73e86-140">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="73e86-141">Sostituire **USERNAME** nome hello dell'accesso SSH.</span><span class="sxs-lookup"><span data-stu-id="73e86-141">Replace **USERNAME** hello name of your SSH login.</span></span> <span data-ttu-id="73e86-142">Sostituire **CLUSTERNAME** con il nome del cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="73e86-142">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="73e86-143">Per ulteriori informazioni sull'utilizzo di SSH tooconnect tooyour HDInsight cluster, vedere [utilizzo di SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="73e86-143">For more information on using SSH tooconnect tooyour HDInsight cluster, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="73e86-144">Utilizzare hello comando toostart una topologia di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="73e86-144">Use hello following command toostart an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    <span data-ttu-id="73e86-145">Questo comando avvia una topologia di hello esempio WordCount su cluster hello.</span><span class="sxs-lookup"><span data-stu-id="73e86-145">This command starts hello example WordCount topology on hello cluster.</span></span> <span data-ttu-id="73e86-146">Questa topologia generare in modo casuale frasi e occorrenza hello conteggio di ogni parola nella frase hello.</span><span class="sxs-lookup"><span data-stu-id="73e86-146">This topology randomly generate sentences and count hello occurrence of each word in hello sentences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="73e86-147">Quando si inviano cluster toohello topologia, è prima necessario copiare i file jar hello contenente cluster hello prima di utilizzare hello `storm` comando.</span><span class="sxs-lookup"><span data-stu-id="73e86-147">When submitting topology toohello cluster, you must first copy hello jar file containing hello cluster before using hello `storm` command.</span></span> <span data-ttu-id="73e86-148">toocopy hello toohello cluster di file è possibile utilizzare hello `scp` comando.</span><span class="sxs-lookup"><span data-stu-id="73e86-148">toocopy hello file toohello cluster, you can use hello `scp` command.</span></span> <span data-ttu-id="73e86-149">Ad esempio, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="73e86-149">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
   >
   > <span data-ttu-id="73e86-150">Esempio WordCount Hello e altri esempi di starter storm, sono già inclusi nel cluster in `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="73e86-150">hello WordCount example, and other storm starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

## <a name="submit-a-topology-programmatically"></a><span data-ttu-id="73e86-151">Inviare una topologia: a livello di programmazione</span><span class="sxs-lookup"><span data-stu-id="73e86-151">Submit a topology: programmatically</span></span>

<span data-ttu-id="73e86-152">A livello di codice, è possibile distribuire una topologia tooStorm in HDInsight mediante la comunicazione con hello servizio Nimbus ospitato nel cluster.</span><span class="sxs-lookup"><span data-stu-id="73e86-152">You can programmatically deploy a topology tooStorm on HDInsight by communicating with hello Nimbus service hosted in your cluster.</span></span> <span data-ttu-id="73e86-153">[https://github.com/Azure-Samples/hdinsight-Java-deploy-Storm-Topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) viene fornito un esempio di applicazione Java che illustra come toodeploy e avviare una topologia tramite il servizio Nimbus hello.</span><span class="sxs-lookup"><span data-stu-id="73e86-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) provides an example Java application that demonstrates how toodeploy and start a topology through hello Nimbus service.</span></span>

## <a name="monitor-and-manage-visual-studio"></a><span data-ttu-id="73e86-154">Monitorare e gestire: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="73e86-154">Monitor and manage: Visual Studio</span></span>

<span data-ttu-id="73e86-155">Quando una topologia è stata inviata tramite Visual Studio, hello **Storm topologie** visualizzare per il cluster hello viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="73e86-155">When a topology has been successfully submitted using Visual Studio, hello **Storm Topologies** view for hello cluster appears.</span></span> <span data-ttu-id="73e86-156">Selezionare la topologia hello hello elenco tooview informazioni hello in esecuzione sulla topologia.</span><span class="sxs-lookup"><span data-stu-id="73e86-156">Select hello topology from hello list tooview information about hello running topology.</span></span>

![monitor Visual Studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

> [!NOTE]
> <span data-ttu-id="73e86-158">È possibile visualizzare **Storm Topologies** anche da **Esplora server**, espandendo **Azure** > **HDInsight** e quindi facendo clic su un cluster Storm in HDInsight e selezionando **View Storm Topologies**.</span><span class="sxs-lookup"><span data-stu-id="73e86-158">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

<span data-ttu-id="73e86-159">Selezionare la forma hello per hello spouts o bulloni tooview informazioni su questi componenti.</span><span class="sxs-lookup"><span data-stu-id="73e86-159">Select hello shape for hello spouts or bolts tooview information about these components.</span></span> <span data-ttu-id="73e86-160">Viene aperta una nuova finestra per ogni elemento selezionato.</span><span class="sxs-lookup"><span data-stu-id="73e86-160">A new window opens for each item selected.</span></span>

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="73e86-161">Disattivare e riattivare</span><span class="sxs-lookup"><span data-stu-id="73e86-161">Deactivate and reactivate</span></span>

<span data-ttu-id="73e86-162">La disattivazione di una topologia comporta la sua sospensione finché non viene terminata o riattivata.</span><span class="sxs-lookup"><span data-stu-id="73e86-162">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="73e86-163">tooperform queste operazioni, utilizzare hello __disattiva__ e __riattivare__ pulsanti nella parte superiore di hello di hello __topologia riepilogo__.</span><span class="sxs-lookup"><span data-stu-id="73e86-163">tooperform these operations, use hello __Deactivate__ and __Reactivate__ buttons at hello top of hello __Topology Summary__.</span></span>

### <a name="rebalance"></a><span data-ttu-id="73e86-164">Ribilanciare</span><span class="sxs-lookup"><span data-stu-id="73e86-164">Rebalance</span></span>

<span data-ttu-id="73e86-165">Una topologia di ribilanciamento consente parallelismo di hello sistema toorevise hello della topologia hello.</span><span class="sxs-lookup"><span data-stu-id="73e86-165">Rebalancing a topology allows hello system toorevise hello parallelism of hello topology.</span></span> <span data-ttu-id="73e86-166">Ad esempio, se è stato ridimensionato hello cluster tooadd altre note, il ribilanciamento consente una topologia toosee hello nuovi nodi.</span><span class="sxs-lookup"><span data-stu-id="73e86-166">For example, if you have resized hello cluster tooadd more notes, rebalancing allows a topology toosee hello new nodes.</span></span>

<span data-ttu-id="73e86-167">toorebalance una topologia, utilizzare hello __ribilanciare__ pulsante nella parte superiore di hello di hello __topologia riepilogo__.</span><span class="sxs-lookup"><span data-stu-id="73e86-167">toorebalance a topology, use hello __Rebalance__ button at hello top of hello __Topology Summary__.</span></span>

> [!WARNING]
> <span data-ttu-id="73e86-168">Ribilanciamento innanzitutto una topologia Disattiva topologia hello, vengono ridistribuiti worker in modo uniforme tra cluster hello e quindi restituisce infine hello topologia toohello stato prima di ribilanciamento si è verificato.</span><span class="sxs-lookup"><span data-stu-id="73e86-168">Rebalancing a topology first deactivates hello topology, then redistributes workers evenly across hello cluster, then finally returns hello topology toohello state it was in before rebalancing occurred.</span></span> <span data-ttu-id="73e86-169">Pertanto, se la topologia hello era attiva, diventa nuovamente attiva.</span><span class="sxs-lookup"><span data-stu-id="73e86-169">So if hello topology was active, it becomes active again.</span></span> <span data-ttu-id="73e86-170">Se invece era disattivata, rimarrà disattivata.</span><span class="sxs-lookup"><span data-stu-id="73e86-170">If it was deactivated, it remains deactivated.</span></span>

### <a name="kill-a-topology"></a><span data-ttu-id="73e86-171">Terminare una topologia</span><span class="sxs-lookup"><span data-stu-id="73e86-171">Kill a topology</span></span>

<span data-ttu-id="73e86-172">Topologie di Storm continuano l'esecuzione fino a quando non vengono arrestati o hello cluster verrà eliminato.</span><span class="sxs-lookup"><span data-stu-id="73e86-172">Storm topologies continue running until they are stopped or hello cluster is deleted.</span></span> <span data-ttu-id="73e86-173">toostop una topologia, utilizzare hello __Kill__ pulsante nella parte superiore di hello di hello __topologia riepilogo__.</span><span class="sxs-lookup"><span data-stu-id="73e86-173">toostop a topology, use hello __Kill__ button at hello top of hello __Topology Summary__.</span></span>

## <a name="monitor-and-manage-ssh-and-hello-storm-command"></a><span data-ttu-id="73e86-174">Monitorare e gestire: SSH e hello Storm comando</span><span class="sxs-lookup"><span data-stu-id="73e86-174">Monitor and manage: SSH and hello Storm command</span></span>

<span data-ttu-id="73e86-175">Hello `storm` utilità consente toowork con esecuzione topologie dalla riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="73e86-175">hello `storm` utility allows you toowork with running topologies from hello command line.</span></span> <span data-ttu-id="73e86-176">Per visualizzare l'elenco completo dei comandi, usare `storm -h` .</span><span class="sxs-lookup"><span data-stu-id="73e86-176">Use `storm -h` for a full list of commands.</span></span>

### <a name="list-topologies"></a><span data-ttu-id="73e86-177">Visualizzare l'elenco delle topologie</span><span class="sxs-lookup"><span data-stu-id="73e86-177">List topologies</span></span>

<span data-ttu-id="73e86-178">Tutte le topologie in esecuzione, utilizzare hello toolist di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="73e86-178">Use hello following command toolist all running topologies:</span></span>

    storm list

<span data-ttu-id="73e86-179">Questo comando restituisce toohello di informazioni simili seguente testo:</span><span class="sxs-lookup"><span data-stu-id="73e86-179">This command returns information similar toohello following text:</span></span>

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="73e86-180">Disattivare e riattivare</span><span class="sxs-lookup"><span data-stu-id="73e86-180">Deactivate and reactivate</span></span>

<span data-ttu-id="73e86-181">La disattivazione di una topologia comporta la sua sospensione finché non viene terminata o riattivata.</span><span class="sxs-lookup"><span data-stu-id="73e86-181">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="73e86-182">Utilizzare hello successivo comando toodeactivate e riattivare:</span><span class="sxs-lookup"><span data-stu-id="73e86-182">Use hello following command toodeactivate and reactivate:</span></span>

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a><span data-ttu-id="73e86-183">Terminare una topologia in esecuzione</span><span class="sxs-lookup"><span data-stu-id="73e86-183">Kill a running topology</span></span>

<span data-ttu-id="73e86-184">Una volta avviate, le topologie Storm continueranno a rimanere in esecuzione finché non vengono arrestate.</span><span class="sxs-lookup"><span data-stu-id="73e86-184">Storm topologies, once started, continue running until stopped.</span></span> <span data-ttu-id="73e86-185">toostop una topologia, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="73e86-185">toostop a topology, use hello following command:</span></span>

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a><span data-ttu-id="73e86-186">Ribilanciare</span><span class="sxs-lookup"><span data-stu-id="73e86-186">Rebalance</span></span>

<span data-ttu-id="73e86-187">Una topologia di ribilanciamento consente parallelismo di hello sistema toorevise hello della topologia hello.</span><span class="sxs-lookup"><span data-stu-id="73e86-187">Rebalancing a topology allows hello system toorevise hello parallelism of hello topology.</span></span> <span data-ttu-id="73e86-188">Ad esempio, se è stato ridimensionato hello cluster tooadd altre note, il ribilanciamento consente una topologia toosee hello nuovi nodi.</span><span class="sxs-lookup"><span data-stu-id="73e86-188">For example, if you have resized hello cluster tooadd more notes, rebalancing allows a topology toosee hello new nodes.</span></span>

> [!WARNING]
> <span data-ttu-id="73e86-189">Ribilanciamento innanzitutto una topologia Disattiva topologia hello, vengono ridistribuiti worker in modo uniforme tra cluster hello e quindi restituisce infine hello topologia toohello stato prima di ribilanciamento si è verificato.</span><span class="sxs-lookup"><span data-stu-id="73e86-189">Rebalancing a topology first deactivates hello topology, then redistributes workers evenly across hello cluster, then finally returns hello topology toohello state it was in before rebalancing occurred.</span></span> <span data-ttu-id="73e86-190">Pertanto, se la topologia hello era attiva, diventa nuovamente attiva.</span><span class="sxs-lookup"><span data-stu-id="73e86-190">So if hello topology was active, it becomes active again.</span></span> <span data-ttu-id="73e86-191">Se invece era disattivata, rimarrà disattivata.</span><span class="sxs-lookup"><span data-stu-id="73e86-191">If it was deactivated, it remains deactivated.</span></span>

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a><span data-ttu-id="73e86-192">Monitorare e gestire: interfaccia utente di Storm</span><span class="sxs-lookup"><span data-stu-id="73e86-192">Monitor and manage: Storm UI</span></span>

<span data-ttu-id="73e86-193">Ciao Storm UI fornisce un'interfaccia web per l'utilizzo con l'esecuzione di topologie ed è incluso nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="73e86-193">hello Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span> <span data-ttu-id="73e86-194">hello tooview dell'interfaccia utente Storm, utilizzare un tooopen browser web **https://CLUSTERNAME.azurehdinsight.net/stormui**, dove **CLUSTERNAME** hello nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="73e86-194">tooview hello Storm UI, use a web browser tooopen **https://CLUSTERNAME.azurehdinsight.net/stormui**, where **CLUSTERNAME** is hello name of your cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="73e86-195">Se richiesto tooprovide un nome utente e una password, immettere Amministrazione cluster hello (amministratore) e la password utilizzati quando la creazione di cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="73e86-195">If asked tooprovide a user name and password, enter hello cluster administrator (admin) and password that you used when creating hello cluster.</span></span>

### <a name="main-page"></a><span data-ttu-id="73e86-196">Pagina principale</span><span class="sxs-lookup"><span data-stu-id="73e86-196">Main page</span></span>

<span data-ttu-id="73e86-197">pagina principale di Hello di hello Storm UI fornisce hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="73e86-197">hello main page of hello Storm UI provides hello following information:</span></span>

* <span data-ttu-id="73e86-198">**Riepilogo di cluster**: informazioni di base sui cluster Storm hello.</span><span class="sxs-lookup"><span data-stu-id="73e86-198">**Cluster summary**: Basic information about hello Storm cluster.</span></span>
* <span data-ttu-id="73e86-199">**Topology summary**: elenco delle topologie in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="73e86-199">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="73e86-200">Utilizzare collegamenti hello in questa sezione di tooview ulteriori informazioni sulle topologie specifiche.</span><span class="sxs-lookup"><span data-stu-id="73e86-200">Use hello links in this section tooview more information about specific topologies.</span></span>
* <span data-ttu-id="73e86-201">**Riepilogo Supervisore**: informazioni su Supervisore Storm hello.</span><span class="sxs-lookup"><span data-stu-id="73e86-201">**Supervisor summary**: Information about hello Storm supervisor.</span></span>
* <span data-ttu-id="73e86-202">**Configurazione nimbus**: configurazione di Nimbus per cluster hello.</span><span class="sxs-lookup"><span data-stu-id="73e86-202">**Nimbus configuration**: Nimbus configuration for hello cluster.</span></span>

### <a name="topology-summary"></a><span data-ttu-id="73e86-203">Topology summary</span><span class="sxs-lookup"><span data-stu-id="73e86-203">Topology summary</span></span>

<span data-ttu-id="73e86-204">Quando si seleziona un collegamento da hello **riepilogo topologia** sezione sono visualizzate le seguenti informazioni sulla topologia di hello hello:</span><span class="sxs-lookup"><span data-stu-id="73e86-204">Selecting a link from hello **Topology summary** section displays hello following information about hello topology:</span></span>

* <span data-ttu-id="73e86-205">**Topologia riepilogo**: le informazioni di base relative alla topologia di hello.</span><span class="sxs-lookup"><span data-stu-id="73e86-205">**Topology summary**: Basic information about hello topology.</span></span>
* <span data-ttu-id="73e86-206">**Azioni di topologia**: azioni di gestione che è possibile eseguire per la topologia hello.</span><span class="sxs-lookup"><span data-stu-id="73e86-206">**Topology actions**: Management actions that you can perform for hello topology.</span></span>

  * <span data-ttu-id="73e86-207">**Activate**: riprende l'elaborazione di una topologia disattivata.</span><span class="sxs-lookup"><span data-stu-id="73e86-207">**Activate**: Resumes processing of a deactivated topology.</span></span>
  * <span data-ttu-id="73e86-208">**Deactivate**: sospende una topologia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="73e86-208">**Deactivate**: Pauses a running topology.</span></span>
  * <span data-ttu-id="73e86-209">**Ribilanciare**: consente di regolare il parallelismo hello della topologia hello.</span><span class="sxs-lookup"><span data-stu-id="73e86-209">**Rebalance**: Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="73e86-210">È necessario ribilanciare topologie in esecuzione dopo avere modificato il numero di hello di nodi nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="73e86-210">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="73e86-211">Questa operazione consente hello topologia tooadjust parallelismo toocompensate per hello aumentato o diminuito di numero di nodi nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="73e86-211">This operation allows hello topology tooadjust parallelism toocompensate for hello increased or decreased number of nodes in hello cluster.</span></span>

    <span data-ttu-id="73e86-212">Per ulteriori informazioni, vedere <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">comprensione parallelismo hello di una topologia di Storm</a>.</span><span class="sxs-lookup"><span data-stu-id="73e86-212">For more information, see <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Understanding hello parallelism of a Storm topology</a>.</span></span>
  * <span data-ttu-id="73e86-213">**Kill**: termina una topologia di Storm dopo hello specificato timeout.</span><span class="sxs-lookup"><span data-stu-id="73e86-213">**Kill**: Terminates a Storm topology after hello specified timeout.</span></span>
* <span data-ttu-id="73e86-214">**Statistiche di topologia**: le statistiche relative alla topologia di hello.</span><span class="sxs-lookup"><span data-stu-id="73e86-214">**Topology stats**: Statistics about hello topology.</span></span> <span data-ttu-id="73e86-215">tooset hello periodo di tempo per hello rimanenti voci nella pagina di hello, utilizzare i collegamenti di hello hello **finestra** colonna.</span><span class="sxs-lookup"><span data-stu-id="73e86-215">tooset hello timeframe for hello remaining entries on hello page, use hello links in hello **Window** column.</span></span>
* <span data-ttu-id="73e86-216">**Spouts**: hello spouts utilizzato dalla topologia hello.</span><span class="sxs-lookup"><span data-stu-id="73e86-216">**Spouts**: hello spouts used by hello topology.</span></span> <span data-ttu-id="73e86-217">Usare i collegamenti di hello in questa sezione di tooview ulteriori informazioni su spouts specifico.</span><span class="sxs-lookup"><span data-stu-id="73e86-217">Use hello links in this section tooview more information about specific spouts.</span></span>
* <span data-ttu-id="73e86-218">**Bulloni**: hello bulloni utilizzati dalla topologia hello.</span><span class="sxs-lookup"><span data-stu-id="73e86-218">**Bolts**: hello bolts used by hello topology.</span></span> <span data-ttu-id="73e86-219">Usare i collegamenti di hello in questa sezione di tooview ulteriori informazioni su bulloni specifici.</span><span class="sxs-lookup"><span data-stu-id="73e86-219">Use hello links in this section tooview more information about specific bolts.</span></span>
* <span data-ttu-id="73e86-220">**Configurazione della topologia**: configurazione di hello della topologia hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="73e86-220">**Topology configuration**: hello configuration of hello selected topology.</span></span>

### <a name="spout-and-bolt-summary"></a><span data-ttu-id="73e86-221">Riepilogo di spout e bolt</span><span class="sxs-lookup"><span data-stu-id="73e86-221">Spout and Bolt summary</span></span>

<span data-ttu-id="73e86-222">Selezionando un beccuccio hello **Spouts** o **bulloni** sezioni Visualizza le seguenti informazioni sull'elemento selezionato hello hello:</span><span class="sxs-lookup"><span data-stu-id="73e86-222">Selecting a spout from hello **Spouts** or **Bolts** sections displays hello following information about hello selected item:</span></span>

* <span data-ttu-id="73e86-223">**Riepilogo dei componenti**: informazioni di base beccuccio hello o fulmine.</span><span class="sxs-lookup"><span data-stu-id="73e86-223">**Component summary**: Basic information about hello spout or bolt.</span></span>
* <span data-ttu-id="73e86-224">**Statistiche beccuccio/fulmine**: le statistiche relative hello spout o bullone.</span><span class="sxs-lookup"><span data-stu-id="73e86-224">**Spout/Bolt stats**: Statistics about hello spout or bolt.</span></span> <span data-ttu-id="73e86-225">tooset hello periodo di tempo per hello rimanenti voci nella pagina di hello, utilizzare i collegamenti di hello hello **finestra** colonna.</span><span class="sxs-lookup"><span data-stu-id="73e86-225">tooset hello timeframe for hello remaining entries on hello page, use hello links in hello **Window** column.</span></span>
* <span data-ttu-id="73e86-226">**Statistiche di input** (solo bullone): informazioni su hello flussi utilizzati da fulmine hello di input.</span><span class="sxs-lookup"><span data-stu-id="73e86-226">**Input stats** (bolt only): Information about hello input streams consumed by hello bolt.</span></span>
* <span data-ttu-id="73e86-227">**Output statistiche**: informazioni sui flussi di hello generato da questo spout o bullone.</span><span class="sxs-lookup"><span data-stu-id="73e86-227">**Output stats**: Information about hello streams emitted by this spout or bolt.</span></span>
* <span data-ttu-id="73e86-228">**Executor**: informazioni sulle istanze di hello di beccuccio hello o fulmine.</span><span class="sxs-lookup"><span data-stu-id="73e86-228">**Executors**: Information about hello instances of hello spout or bolt.</span></span> <span data-ttu-id="73e86-229">Seleziona hello **porta** voce per tooview un esecutore specifico prodotto un log delle informazioni di diagnostica per questa istanza.</span><span class="sxs-lookup"><span data-stu-id="73e86-229">Select hello **Port** entry for a specific executor tooview a log of diagnostic information produced for this instance.</span></span>
* <span data-ttu-id="73e86-230">**Errors**: informazioni su eventuali errori dello spout o del bolt.</span><span class="sxs-lookup"><span data-stu-id="73e86-230">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="monitor-and-manage-rest-api"></a><span data-ttu-id="73e86-231">Monitorare e gestire: API REST</span><span class="sxs-lookup"><span data-stu-id="73e86-231">Monitor and manage: REST API</span></span>

<span data-ttu-id="73e86-232">Hello Storm UI si basa su hello l'API REST per effettuare la gestione e il monitoraggio delle funzionalità tramite l'API REST hello simili.</span><span class="sxs-lookup"><span data-stu-id="73e86-232">hello Storm UI is built on top of hello REST API, so you can perform similar management and monitoring functionality by using hello REST API.</span></span> <span data-ttu-id="73e86-233">È possibile utilizzare strumenti personalizzati in toocreate hello API REST per la gestione e monitoraggio topologie Storm.</span><span class="sxs-lookup"><span data-stu-id="73e86-233">You can use hello REST API toocreate custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="73e86-234">Per altre informazioni, vedere l'articolo relativo all'[API REST dell'interfaccia utente di Storm](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span><span class="sxs-lookup"><span data-stu-id="73e86-234">For more information, see [Storm UI REST API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span></span> <span data-ttu-id="73e86-235">Hello informazioni seguenti sono specifici toousing hello API REST con Apache Storm in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="73e86-235">hello following information is specific toousing hello REST API with Apache Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="73e86-236">Hello Storm REST API non è disponibile pubblicamente su internet hello e deve essere accessibile tramite un SSH tunnel toohello HDInsight nodo head del cluster.</span><span class="sxs-lookup"><span data-stu-id="73e86-236">hello Storm REST API is not publicly available over hello internet, and must be accessed using an SSH tunnel toohello HDInsight cluster head node.</span></span> <span data-ttu-id="73e86-237">Per informazioni sulla creazione e utilizzo di un tunnel SSH, vedere [tooaccess usare SSH Tunneling Ambari web dell'interfaccia utente, ResourceManager, JobHistory, NameNode, Oozie e altre interfacce utente web](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="73e86-237">For information on creating and using an SSH tunnel, see [Use SSH Tunneling tooaccess Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UIs](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

### <a name="base-uri"></a><span data-ttu-id="73e86-238">URI di base</span><span class="sxs-lookup"><span data-stu-id="73e86-238">Base URI</span></span>

<span data-ttu-id="73e86-239">Hello URI di base per l'API REST di hello nei cluster HDInsight basati su Linux sono disponibili sul nodo head di hello in **https://HEADNODEFQDN:8744/api/v1/**.</span><span class="sxs-lookup"><span data-stu-id="73e86-239">hello base URI for hello REST API on Linux-based HDInsight clusters is available on hello head node at **https://HEADNODEFQDN:8744/api/v1/**.</span></span> <span data-ttu-id="73e86-240">nome di dominio Hello del nodo head hello viene generato durante la creazione del cluster e non è statico.</span><span class="sxs-lookup"><span data-stu-id="73e86-240">hello domain name of hello head node is generated during cluster creation and is not static.</span></span>

<span data-ttu-id="73e86-241">È possibile trovare il nome di dominio completo hello (FQDN) per nodo head del cluster hello in diversi modi:</span><span class="sxs-lookup"><span data-stu-id="73e86-241">You can find hello fully qualified domain name (FQDN) for hello cluster head node in several different ways:</span></span>

* <span data-ttu-id="73e86-242">**Da una sessione SSH**: utilizzare il comando hello `headnode -f` da un cluster di toohello sessione SSH.</span><span class="sxs-lookup"><span data-stu-id="73e86-242">**From an SSH session**: Use hello command `headnode -f` from an SSH session toohello cluster.</span></span>
* <span data-ttu-id="73e86-243">**Ambari Web**: selezionare **servizi** dalla parte superiore di hello della pagina di hello, quindi selezionare **Storm**.</span><span class="sxs-lookup"><span data-stu-id="73e86-243">**From Ambari Web**: Select **Services** from hello top of hello page, then select **Storm**.</span></span> <span data-ttu-id="73e86-244">Da hello **riepilogo** , selezionare **Server dell'interfaccia utente di Storm**.</span><span class="sxs-lookup"><span data-stu-id="73e86-244">From hello **Summary** tab, select **Storm UI Server**.</span></span> <span data-ttu-id="73e86-245">Hello FQDN hello del nodo di cui è in esecuzione dell'interfaccia utente Storm hello e l'API REST è nella parte superiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="73e86-245">hello FQDN of hello node that hello Storm UI and REST API is running is at hello top of hello page.</span></span>
* <span data-ttu-id="73e86-246">**Dall'API REST Ambari**: utilizzare il comando hello `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` eseguono tooretrieve informazioni nodo hello hello Storm UI e l'API REST.</span><span class="sxs-lookup"><span data-stu-id="73e86-246">**From Ambari REST API**: Use hello command `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` tooretrieve information about hello node that hello Storm UI and REST API are running on.</span></span> <span data-ttu-id="73e86-247">Sostituire **PASSWORD** con password di amministratore hello per cluster hello.</span><span class="sxs-lookup"><span data-stu-id="73e86-247">Replace **PASSWORD** with hello admin password for hello cluster.</span></span> <span data-ttu-id="73e86-248">Sostituire **CLUSTERNAME** con il nome del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="73e86-248">Replace **CLUSTERNAME** with hello cluster name.</span></span> <span data-ttu-id="73e86-249">In risposta hello, voce "host_name" hello contiene hello nome di dominio completo del nodo hello.</span><span class="sxs-lookup"><span data-stu-id="73e86-249">In hello response, hello "host_name" entry contains hello FQDN of hello node.</span></span>

### <a name="authentication"></a><span data-ttu-id="73e86-250">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="73e86-250">Authentication</span></span>

<span data-ttu-id="73e86-251">Toohello richieste API REST è necessario utilizzare **l'autenticazione di base**, pertanto utilizzare nome amministratore del cluster HDInsight hello e una password.</span><span class="sxs-lookup"><span data-stu-id="73e86-251">Requests toohello REST API must use **basic authentication**, so you use hello HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="73e86-252">Poiché l'autenticazione di base viene inviato con testo non crittografato, è necessario **sempre** utilizzare le comunicazioni HTTPS toosecure con cluster hello.</span><span class="sxs-lookup"><span data-stu-id="73e86-252">Because basic authentication is sent by using clear text, you should **always** use HTTPS toosecure communications with hello cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="73e86-253">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="73e86-253">Return values</span></span>

<span data-ttu-id="73e86-254">Informazioni restituite da hello API REST possono solo essere usata da all'interno di cluster hello o hello di macchine virtuali nella stessa rete virtuale di Azure come cluster hello.</span><span class="sxs-lookup"><span data-stu-id="73e86-254">Information that is returned from hello REST API may only be usable from within hello cluster or virtual machines on hello same Azure Virtual Network as hello cluster.</span></span> <span data-ttu-id="73e86-255">Nome di dominio completo hello (FQDN) restituito per i server Zookeeper è ad esempio, non essere accessibile da Internet hello.</span><span class="sxs-lookup"><span data-stu-id="73e86-255">For example, hello fully qualified domain name (FQDN) returned for Zookeeper servers is not be accessible from hello Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73e86-256">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="73e86-256">Next Steps</span></span>

<span data-ttu-id="73e86-257">Ora che si è appreso come topologie toodeploy e monitoraggio tramite hello Storm Dashboard, informazioni su come troppo[topologie basate sul linguaggio di sviluppo utilizzando Maven](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="73e86-257">Now that you've learned how toodeploy and monitor topologies by using hello Storm Dashboard, learn how too[Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="73e86-258">Per un elenco di altre topologie di esempio, vedere [Esempi di topologie Storm per Apache Storm in HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="73e86-258">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
