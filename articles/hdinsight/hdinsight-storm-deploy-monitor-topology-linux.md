---
title: Distribuire e gestire topologie Apache Storm in HDInsight basato su Linux | Documentazione Microsoft
description: Informazioni su come distribuire, monitorare e gestire le topologie Apache Storm mediante Storm Dashboard in HDInsight basato su Linux. Utilizzare gli strumenti Hadoop per Visual Studio
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
ms.openlocfilehash: b9e82463030807d2674594e73f762fe93515d423
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-hdinsight"></a><span data-ttu-id="04fc1-104">Distribuire e gestire topologie Apache Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="04fc1-104">Deploy and manage Apache Storm topologies on HDInsight</span></span>

<span data-ttu-id="04fc1-105">In questo documento sono illustrati i concetti di gestione e monitoraggio delle topologie Storm in esecuzione su Storm in cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="04fc1-105">In this document, learn the basics of managing and monitoring Storm topologies running on Storm on HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="04fc1-106">I passaggi descritti in questo articolo richiedono una versione di Storm basata su Linux nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="04fc1-106">The steps in this article require a Linux-based Storm on HDInsight cluster.</span></span> <span data-ttu-id="04fc1-107">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="04fc1-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="04fc1-108">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="04fc1-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 
>
> <span data-ttu-id="04fc1-109">Per informazioni sulla distribuzione e sul monitoraggio di topologie in HDInsight basato su Windows, vedere [Distribuire e gestire le topologie di Apache Storm in HDInsight basato su Windows](hdinsight-storm-deploy-monitor-topology.md)</span><span class="sxs-lookup"><span data-stu-id="04fc1-109">For information on deploying and monitoring topologies on Windows-based HDInsight, see [Deploy and manage Apache Storm topologies on Windows-based HDInsight](hdinsight-storm-deploy-monitor-topology.md)</span></span>


## <a name="prerequisites"></a><span data-ttu-id="04fc1-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="04fc1-110">Prerequisites</span></span>

* <span data-ttu-id="04fc1-111">**Storm basato su Linux in cluster HDInsight**: per i passaggi relativi alla creazione di un cluster, vedere [Introduzione ad Apache Storm in HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) .</span><span class="sxs-lookup"><span data-stu-id="04fc1-111">**A Linux-based Storm on HDInsight cluster**: see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) for steps on creating a cluster</span></span>

* <span data-ttu-id="04fc1-112">(Facoltativo) **Familiarità con SSH e SCP**: per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="04fc1-112">(Optional) **Familiarity with SSH and SCP**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="04fc1-113">(Facoltativo) **Visual Studio**: Azure SDK 2.5.1 o versione successiva e Data Lake Tools per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="04fc1-113">(Optional) **Visual Studio**: Azure SDK 2.5.1 or newer and the Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="04fc1-114">Per altre informazioni, vedere [Introduzione all'uso di Data Lake Tools per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="04fc1-114">For more information, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    <span data-ttu-id="04fc1-115">Una delle seguenti versioni di Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="04fc1-115">One of the following versions of Visual Studio:</span></span>

  * <span data-ttu-id="04fc1-116">Visual Studio 2012 con [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="04fc1-116">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

  * <span data-ttu-id="04fc1-117">Visual Studio 2013 con [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) o [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="04fc1-117">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>
  * [<span data-ttu-id="04fc1-118">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="04fc1-118">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/)

  * <span data-ttu-id="04fc1-119">Visual Studio 2015, qualsiasi edizione</span><span class="sxs-lookup"><span data-stu-id="04fc1-119">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="04fc1-120">Visual Studio 2017, qualsiasi edizione.</span><span class="sxs-lookup"><span data-stu-id="04fc1-120">Visual Studio 2017 (any edition).</span></span> <span data-ttu-id="04fc1-121">Data Lake Tools per Visual Studio 2017 viene installato come parte del carico di lavoro di Azure.</span><span class="sxs-lookup"><span data-stu-id="04fc1-121">Data Lake Tools for Visual Studio 2017 are installed as part of the Azure Workload.</span></span>

## <a name="submit-a-topology-visual-studio"></a><span data-ttu-id="04fc1-122">Inviare una topologia: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="04fc1-122">Submit a topology: Visual Studio</span></span>

<span data-ttu-id="04fc1-123">HDInsight Tools consente di inviare topologie C# o ibride al cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="04fc1-123">The HDInsight Tools can be used to submit C# or hybrid topologies to your Storm cluster.</span></span> <span data-ttu-id="04fc1-124">Nei seguenti passaggi viene usata un'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="04fc1-124">The following steps use a sample application.</span></span> <span data-ttu-id="04fc1-125">Per informazioni sulla creazione delle proprie tipologie, vedere [Sviluppare topologie C# per Apache Storm in HDInsight tramite Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="04fc1-125">For information about creating your own topologies by using the HDInsight Tools, see [Develop C# topologies using the HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

1. <span data-ttu-id="04fc1-126">Se la versione più recente di Data Lake Tools per Visual Studio non è ancora installata, vedere [Introduzione all'uso di Data Lake Tools per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="04fc1-126">If you have not already installed the latest version of the Data Lake tools for Visual Studio, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="04fc1-127">Data Lake Tools per Visual Studio veniva precedentemente chiamato HDInsight Tools per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="04fc1-127">The Data Lake Tools for Visual Studio were formerly called the HDInsight Tools for Visual Studio.</span></span>
    >
    > <span data-ttu-id="04fc1-128">Data Lake Tools per Visual Studio è incluso nel __carico di lavoro di Azure__ per Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="04fc1-128">Data Lake Tools for Visual Studio are included in the __Azure Workload__ for Visual Studio 2017.</span></span>

2. <span data-ttu-id="04fc1-129">Aprire Visual Studio e selezionare **File** > **Nuovo** > **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="04fc1-129">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="04fc1-130">Nella finestra di dialogo **Nuovo progetto** espandere **Installato** > **Modelli** e quindi selezionare **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="04fc1-130">In the **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="04fc1-131">Dall'elenco dei modelli selezionare **Storm Sample**.</span><span class="sxs-lookup"><span data-stu-id="04fc1-131">From the list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="04fc1-132">Nella parte inferiore della finestra di dialogo digitare un nome per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="04fc1-132">At the bottom of the dialog box, type a name for the application.</span></span>

    ![immagine](./media/hdinsight-storm-deploy-monitor-topology-linux/sample.png)

4. <span data-ttu-id="04fc1-134">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto e selezionare **Submit to Storm on HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="04fc1-134">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="04fc1-135">Se richiesto, immettere le credenziali di accesso per la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="04fc1-135">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="04fc1-136">Se si dispone di più di una sottoscrizione, accedere a quella che contiene il cluster Storm in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="04fc1-136">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="04fc1-137">Selezionare il cluster Storm in HDInsight dall'elenco a discesa **Storm Cluster** e quindi selezionare **Submit**.</span><span class="sxs-lookup"><span data-stu-id="04fc1-137">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="04fc1-138">È possibile verificare se l'invio è riuscito o meno usando la finestra **Output** .</span><span class="sxs-lookup"><span data-stu-id="04fc1-138">You can monitor whether the submission is successful by using the **Output** window.</span></span>

## <a name="submit-a-topology-ssh-and-the-storm-command"></a><span data-ttu-id="04fc1-139">Inviare una topologia: SSH e il comando Storm</span><span class="sxs-lookup"><span data-stu-id="04fc1-139">Submit a topology: SSH and the Storm command</span></span>

1. <span data-ttu-id="04fc1-140">Connettersi al cluster HDInsight usando SSH.</span><span class="sxs-lookup"><span data-stu-id="04fc1-140">Use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="04fc1-141">Sostituire **USERNAME** con il nome di accesso a SSH.</span><span class="sxs-lookup"><span data-stu-id="04fc1-141">Replace **USERNAME** the name of your SSH login.</span></span> <span data-ttu-id="04fc1-142">Sostituire **CLUSTERNAME** con il nome del cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="04fc1-142">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="04fc1-143">Per altre informazioni sull'uso di SSH per connettersi a HDInsight, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="04fc1-143">For more information on using SSH to connect to your HDInsight cluster, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="04fc1-144">Usare il comando seguente per avviare una topologia di esempio:</span><span class="sxs-lookup"><span data-stu-id="04fc1-144">Use the following command to start an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    <span data-ttu-id="04fc1-145">Questo comando consente di avviare la topologia di esempio WordCount nel cluster.</span><span class="sxs-lookup"><span data-stu-id="04fc1-145">This command starts the example WordCount topology on the cluster.</span></span> <span data-ttu-id="04fc1-146">Questa topologia genera in modo casuale le frasi e conteggia le occorrenze di ogni parola nelle frasi.</span><span class="sxs-lookup"><span data-stu-id="04fc1-146">This topology randomly generate sentences and count the occurrence of each word in the sentences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="04fc1-147">Durante l'invio di una topologia al cluster, è prima di tutto necessario copiare il file con estensione JAR contenente il cluster prima di usare il comando `storm`.</span><span class="sxs-lookup"><span data-stu-id="04fc1-147">When submitting topology to the cluster, you must first copy the jar file containing the cluster before using the `storm` command.</span></span> <span data-ttu-id="04fc1-148">Usare il comando `scp` per copiare il file nel cluster.</span><span class="sxs-lookup"><span data-stu-id="04fc1-148">To copy the file to the cluster, you can use the `scp` command.</span></span> <span data-ttu-id="04fc1-149">Ad esempio: `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="04fc1-149">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
   >
   > <span data-ttu-id="04fc1-150">L'esempio WordCount e altri esempi di avvio dell'utilità storm sono già inclusi nel cluster in `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="04fc1-150">The WordCount example, and other storm starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

## <a name="submit-a-topology-programmatically"></a><span data-ttu-id="04fc1-151">Inviare una topologia: a livello di programmazione</span><span class="sxs-lookup"><span data-stu-id="04fc1-151">Submit a topology: programmatically</span></span>

<span data-ttu-id="04fc1-152">È possibile distribuire a livello di codice una topologia in Storm su HDInsight comunicando con il servizio Nimbus ospitato nel cluster.</span><span class="sxs-lookup"><span data-stu-id="04fc1-152">You can programmatically deploy a topology to Storm on HDInsight by communicating with the Nimbus service hosted in your cluster.</span></span> <span data-ttu-id="04fc1-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) è disponibile un'applicazione Java di esempio che illustra come distribuire e avviare una topologia tramite il servizio Nimbus.</span><span class="sxs-lookup"><span data-stu-id="04fc1-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) provides an example Java application that demonstrates how to deploy and start a topology through the Nimbus service.</span></span>

## <a name="monitor-and-manage-visual-studio"></a><span data-ttu-id="04fc1-154">Monitorare e gestire: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="04fc1-154">Monitor and manage: Visual Studio</span></span>

<span data-ttu-id="04fc1-155">Dopo che la topologia è stata inviata correttamente con Visual Studio, verrà visualizza la vista **Topologie Storm** relativa al cluster.</span><span class="sxs-lookup"><span data-stu-id="04fc1-155">When a topology has been successfully submitted using Visual Studio, the **Storm Topologies** view for the cluster appears.</span></span> <span data-ttu-id="04fc1-156">Per visualizzare informazioni sulla topologia in esecuzione, selezionarla dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="04fc1-156">Select the topology from the list to view information about the running topology.</span></span>

![monitor Visual Studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

> [!NOTE]
> <span data-ttu-id="04fc1-158">È possibile visualizzare **Storm Topologies** anche da **Esplora server**, espandendo **Azure** > **HDInsight** e quindi facendo clic su un cluster Storm in HDInsight e selezionando **View Storm Topologies**.</span><span class="sxs-lookup"><span data-stu-id="04fc1-158">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

<span data-ttu-id="04fc1-159">Selezionare la forma degli spout o dei bolt per visualizzare informazioni su questi componenti.</span><span class="sxs-lookup"><span data-stu-id="04fc1-159">Select the shape for the spouts or bolts to view information about these components.</span></span> <span data-ttu-id="04fc1-160">Viene aperta una nuova finestra per ogni elemento selezionato.</span><span class="sxs-lookup"><span data-stu-id="04fc1-160">A new window opens for each item selected.</span></span>

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="04fc1-161">Disattivare e riattivare</span><span class="sxs-lookup"><span data-stu-id="04fc1-161">Deactivate and reactivate</span></span>

<span data-ttu-id="04fc1-162">La disattivazione di una topologia comporta la sua sospensione finché non viene terminata o riattivata.</span><span class="sxs-lookup"><span data-stu-id="04fc1-162">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="04fc1-163">Per eseguire queste operazioni, usare i pulsanti __Disattiva__ e __Riattiva__ nella parte superiore del __Topology Summary__ (Riepilogo topologia).</span><span class="sxs-lookup"><span data-stu-id="04fc1-163">To perform these operations, use the __Deactivate__ and __Reactivate__ buttons at the top of the __Topology Summary__.</span></span>

### <a name="rebalance"></a><span data-ttu-id="04fc1-164">Ribilanciare</span><span class="sxs-lookup"><span data-stu-id="04fc1-164">Rebalance</span></span>

<span data-ttu-id="04fc1-165">Il ribilanciamento di una topologia consente al sistema di analizzare il parallelismo della topologia.</span><span class="sxs-lookup"><span data-stu-id="04fc1-165">Rebalancing a topology allows the system to revise the parallelism of the topology.</span></span> <span data-ttu-id="04fc1-166">Ad esempio, se il cluster è stato ridimensionato per aggiungere altre note, il ribilanciamento consente a una topologia di visualizzare i nuovi nodi.</span><span class="sxs-lookup"><span data-stu-id="04fc1-166">For example, if you have resized the cluster to add more notes, rebalancing allows a topology to see the new nodes.</span></span>

<span data-ttu-id="04fc1-167">Per ribilanciare una topologia, usare il pulsante __Ribilancia__ nella parte superiore di __Topology Summary__ (Riepilogo topologia).</span><span class="sxs-lookup"><span data-stu-id="04fc1-167">To rebalance a topology, use the __Rebalance__ button at the top of the __Topology Summary__.</span></span>

> [!WARNING]
> <span data-ttu-id="04fc1-168">Il ribilanciamento di una topologia disattiva innanzitutto la topologia, ridistribuisce i processi di lavoro in modo uniforme nel cluster, quindi restituisce la topologia allo stato in cui si trovava prima che venisse eseguito il ribilanciamento.</span><span class="sxs-lookup"><span data-stu-id="04fc1-168">Rebalancing a topology first deactivates the topology, then redistributes workers evenly across the cluster, then finally returns the topology to the state it was in before rebalancing occurred.</span></span> <span data-ttu-id="04fc1-169">Se la topologia era attiva, tornerà a essere attiva di nuovo.</span><span class="sxs-lookup"><span data-stu-id="04fc1-169">So if the topology was active, it becomes active again.</span></span> <span data-ttu-id="04fc1-170">Se invece era disattivata, rimarrà disattivata.</span><span class="sxs-lookup"><span data-stu-id="04fc1-170">If it was deactivated, it remains deactivated.</span></span>

### <a name="kill-a-topology"></a><span data-ttu-id="04fc1-171">Terminare una topologia</span><span class="sxs-lookup"><span data-stu-id="04fc1-171">Kill a topology</span></span>

<span data-ttu-id="04fc1-172">Le topologie Storm continuano l'esecuzione fino a quando non vengono arrestate o fino a quando il cluster non viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="04fc1-172">Storm topologies continue running until they are stopped or the cluster is deleted.</span></span> <span data-ttu-id="04fc1-173">Per arrestare una topologia, usare il pulsante __Termina__ nella parte superiore di __Topology Summary__ (Riepilogo topologia).</span><span class="sxs-lookup"><span data-stu-id="04fc1-173">To stop a topology, use the __Kill__ button at the top of the __Topology Summary__.</span></span>

## <a name="monitor-and-manage-ssh-and-the-storm-command"></a><span data-ttu-id="04fc1-174">Monitorare e gestire: SSH e il comando Storm</span><span class="sxs-lookup"><span data-stu-id="04fc1-174">Monitor and manage: SSH and the Storm command</span></span>

<span data-ttu-id="04fc1-175">L'utilità `storm` consente di usare le topologie in esecuzione dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="04fc1-175">The `storm` utility allows you to work with running topologies from the command line.</span></span> <span data-ttu-id="04fc1-176">Per visualizzare l'elenco completo dei comandi, usare `storm -h` .</span><span class="sxs-lookup"><span data-stu-id="04fc1-176">Use `storm -h` for a full list of commands.</span></span>

### <a name="list-topologies"></a><span data-ttu-id="04fc1-177">Visualizzare l'elenco delle topologie</span><span class="sxs-lookup"><span data-stu-id="04fc1-177">List topologies</span></span>

<span data-ttu-id="04fc1-178">Usare il comando seguente per ottenere un elenco delle topologie in esecuzione:</span><span class="sxs-lookup"><span data-stu-id="04fc1-178">Use the following command to list all running topologies:</span></span>

    storm list

<span data-ttu-id="04fc1-179">Questo comando restituisce informazioni simili al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="04fc1-179">This command returns information similar to the following text:</span></span>

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="04fc1-180">Disattivare e riattivare</span><span class="sxs-lookup"><span data-stu-id="04fc1-180">Deactivate and reactivate</span></span>

<span data-ttu-id="04fc1-181">La disattivazione di una topologia comporta la sua sospensione finché non viene terminata o riattivata.</span><span class="sxs-lookup"><span data-stu-id="04fc1-181">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="04fc1-182">Per disattivare e riattivare, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="04fc1-182">Use the following command to deactivate and reactivate:</span></span>

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a><span data-ttu-id="04fc1-183">Terminare una topologia in esecuzione</span><span class="sxs-lookup"><span data-stu-id="04fc1-183">Kill a running topology</span></span>

<span data-ttu-id="04fc1-184">Una volta avviate, le topologie Storm continueranno a rimanere in esecuzione finché non vengono arrestate.</span><span class="sxs-lookup"><span data-stu-id="04fc1-184">Storm topologies, once started, continue running until stopped.</span></span> <span data-ttu-id="04fc1-185">Per arrestare una topologia, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="04fc1-185">To stop a topology, use the following command:</span></span>

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a><span data-ttu-id="04fc1-186">Ribilanciare</span><span class="sxs-lookup"><span data-stu-id="04fc1-186">Rebalance</span></span>

<span data-ttu-id="04fc1-187">Il ribilanciamento di una topologia consente al sistema di analizzare il parallelismo della topologia.</span><span class="sxs-lookup"><span data-stu-id="04fc1-187">Rebalancing a topology allows the system to revise the parallelism of the topology.</span></span> <span data-ttu-id="04fc1-188">Ad esempio, se il cluster è stato ridimensionato per aggiungere altre note, il ribilanciamento consente a una topologia di visualizzare i nuovi nodi.</span><span class="sxs-lookup"><span data-stu-id="04fc1-188">For example, if you have resized the cluster to add more notes, rebalancing allows a topology to see the new nodes.</span></span>

> [!WARNING]
> <span data-ttu-id="04fc1-189">Il ribilanciamento di una topologia disattiva innanzitutto la topologia, ridistribuisce i processi di lavoro in modo uniforme nel cluster, quindi restituisce la topologia allo stato in cui si trovava prima che venisse eseguito il ribilanciamento.</span><span class="sxs-lookup"><span data-stu-id="04fc1-189">Rebalancing a topology first deactivates the topology, then redistributes workers evenly across the cluster, then finally returns the topology to the state it was in before rebalancing occurred.</span></span> <span data-ttu-id="04fc1-190">Se la topologia era attiva, tornerà a essere attiva di nuovo.</span><span class="sxs-lookup"><span data-stu-id="04fc1-190">So if the topology was active, it becomes active again.</span></span> <span data-ttu-id="04fc1-191">Se invece era disattivata, rimarrà disattivata.</span><span class="sxs-lookup"><span data-stu-id="04fc1-191">If it was deactivated, it remains deactivated.</span></span>

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a><span data-ttu-id="04fc1-192">Monitorare e gestire: interfaccia utente di Storm</span><span class="sxs-lookup"><span data-stu-id="04fc1-192">Monitor and manage: Storm UI</span></span>

<span data-ttu-id="04fc1-193">L'interfaccia utente di Storm è inclusa nel cluster HDInsight e fornisce un'interfaccia Web da usare con le topologie in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="04fc1-193">The Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span> <span data-ttu-id="04fc1-194">Per visualizzare l'interfaccia utente di Storm, usare un Web browser per aprire **https://CLUSTERNAME.azurehdinsight.net/stormui**, dove **CLUSTERNAME** corrisponde al nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="04fc1-194">To view the Storm UI, use a web browser to open **https://CLUSTERNAME.azurehdinsight.net/stormui**, where **CLUSTERNAME** is the name of your cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="04fc1-195">Se viene richiesto di fornire un nome utente e una password, immettere l'amministratore del cluster e la password usati durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="04fc1-195">If asked to provide a user name and password, enter the cluster administrator (admin) and password that you used when creating the cluster.</span></span>

### <a name="main-page"></a><span data-ttu-id="04fc1-196">Pagina principale</span><span class="sxs-lookup"><span data-stu-id="04fc1-196">Main page</span></span>

<span data-ttu-id="04fc1-197">Nella pagina principale dell'interfaccia utente di Storm sono disponibili le informazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="04fc1-197">The main page of the Storm UI provides the following information:</span></span>

* <span data-ttu-id="04fc1-198">**Cluster summary**: informazioni di base sul cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="04fc1-198">**Cluster summary**: Basic information about the Storm cluster.</span></span>
* <span data-ttu-id="04fc1-199">**Topology summary**: elenco delle topologie in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="04fc1-199">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="04fc1-200">Usare i collegamenti disponibili in questa sezione per visualizzare ulteriori informazioni su topologie specifiche.</span><span class="sxs-lookup"><span data-stu-id="04fc1-200">Use the links in this section to view more information about specific topologies.</span></span>
* <span data-ttu-id="04fc1-201">**Supervisor summary**: informazioni su Storm Supervisor.</span><span class="sxs-lookup"><span data-stu-id="04fc1-201">**Supervisor summary**: Information about the Storm supervisor.</span></span>
* <span data-ttu-id="04fc1-202">**Nimbus configuration**: configurazione Nimbus per il cluster.</span><span class="sxs-lookup"><span data-stu-id="04fc1-202">**Nimbus configuration**: Nimbus configuration for the cluster.</span></span>

### <a name="topology-summary"></a><span data-ttu-id="04fc1-203">Topology summary</span><span class="sxs-lookup"><span data-stu-id="04fc1-203">Topology summary</span></span>

<span data-ttu-id="04fc1-204">Se si seleziona un collegamento nella sezione **Topology summary** , verranno visualizzate le informazioni seguenti sulla topologia.</span><span class="sxs-lookup"><span data-stu-id="04fc1-204">Selecting a link from the **Topology summary** section displays the following information about the topology:</span></span>

* <span data-ttu-id="04fc1-205">**Topology summary**: informazioni di base sulla topologia.</span><span class="sxs-lookup"><span data-stu-id="04fc1-205">**Topology summary**: Basic information about the topology.</span></span>
* <span data-ttu-id="04fc1-206">**Topology actions**: azioni di gestione che è possibile eseguire per la topologia.</span><span class="sxs-lookup"><span data-stu-id="04fc1-206">**Topology actions**: Management actions that you can perform for the topology.</span></span>

  * <span data-ttu-id="04fc1-207">**Activate**: riprende l'elaborazione di una topologia disattivata.</span><span class="sxs-lookup"><span data-stu-id="04fc1-207">**Activate**: Resumes processing of a deactivated topology.</span></span>
  * <span data-ttu-id="04fc1-208">**Deactivate**: sospende una topologia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="04fc1-208">**Deactivate**: Pauses a running topology.</span></span>
  * <span data-ttu-id="04fc1-209">**Rebalance**: regola il parallelismo della topologia.</span><span class="sxs-lookup"><span data-stu-id="04fc1-209">**Rebalance**: Adjusts the parallelism of the topology.</span></span> <span data-ttu-id="04fc1-210">È necessario ribilanciare le topologie in esecuzione dopo aver modificato il numero di nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="04fc1-210">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span></span> <span data-ttu-id="04fc1-211">Questa operazione consente alla topologia di regolare il parallelismo per compensare l'aumento o la diminuzione del numero di nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="04fc1-211">This operation allows the topology to adjust parallelism to compensate for the increased or decreased number of nodes in the cluster.</span></span>

    <span data-ttu-id="04fc1-212">Per altre informazioni, vedere l'articolo relativo al <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">parallelismo di una topologia Storm</a>.</span><span class="sxs-lookup"><span data-stu-id="04fc1-212">For more information, see <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Understanding the parallelism of a Storm topology</a>.</span></span>
  * <span data-ttu-id="04fc1-213">**Kill**: termina una topologia Storm dopo il timeout specificato.</span><span class="sxs-lookup"><span data-stu-id="04fc1-213">**Kill**: Terminates a Storm topology after the specified timeout.</span></span>
* <span data-ttu-id="04fc1-214">**Topology stats**: statistiche sulla topologia.</span><span class="sxs-lookup"><span data-stu-id="04fc1-214">**Topology stats**: Statistics about the topology.</span></span> <span data-ttu-id="04fc1-215">Usare i collegamenti disponibili nella colonna **Finestra** per impostare l'intervallo di tempo per le rimanenti voci della pagina.</span><span class="sxs-lookup"><span data-stu-id="04fc1-215">To set the timeframe for the remaining entries on the page, use the links in the **Window** column.</span></span>
* <span data-ttu-id="04fc1-216">**Spouts**: spout usati dalla topologia.</span><span class="sxs-lookup"><span data-stu-id="04fc1-216">**Spouts**: The spouts used by the topology.</span></span> <span data-ttu-id="04fc1-217">Usare i collegamenti disponibili in questa sezione per visualizzare ulteriori informazioni su spout specifici.</span><span class="sxs-lookup"><span data-stu-id="04fc1-217">Use the links in this section to view more information about specific spouts.</span></span>
* <span data-ttu-id="04fc1-218">**Bolts**: bolt usati nella topologia.</span><span class="sxs-lookup"><span data-stu-id="04fc1-218">**Bolts**: The bolts used by the topology.</span></span> <span data-ttu-id="04fc1-219">Usare i collegamenti disponibili in questa sezione per visualizzare ulteriori informazioni su bolt specifici.</span><span class="sxs-lookup"><span data-stu-id="04fc1-219">Use the links in this section to view more information about specific bolts.</span></span>
* <span data-ttu-id="04fc1-220">**Topology configuration**: configurazione della topologia selezionata.</span><span class="sxs-lookup"><span data-stu-id="04fc1-220">**Topology configuration**: The configuration of the selected topology.</span></span>

### <a name="spout-and-bolt-summary"></a><span data-ttu-id="04fc1-221">Riepilogo di spout e bolt</span><span class="sxs-lookup"><span data-stu-id="04fc1-221">Spout and Bolt summary</span></span>

<span data-ttu-id="04fc1-222">Se si seleziona un elemento nella sezione **Spouts** o **Bolts**, verranno visualizzate le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="04fc1-222">Selecting a spout from the **Spouts** or **Bolts** sections displays the following information about the selected item:</span></span>

* <span data-ttu-id="04fc1-223">**Component summary**: informazioni di base sullo spout o sul bolt.</span><span class="sxs-lookup"><span data-stu-id="04fc1-223">**Component summary**: Basic information about the spout or bolt.</span></span>
* <span data-ttu-id="04fc1-224">**Spout/Bolt stats**: statistiche relative allo spout o al bolt.</span><span class="sxs-lookup"><span data-stu-id="04fc1-224">**Spout/Bolt stats**: Statistics about the spout or bolt.</span></span> <span data-ttu-id="04fc1-225">Usare i collegamenti disponibili nella colonna **Finestra** per impostare l'intervallo di tempo per le rimanenti voci della pagina.</span><span class="sxs-lookup"><span data-stu-id="04fc1-225">To set the timeframe for the remaining entries on the page, use the links in the **Window** column.</span></span>
* <span data-ttu-id="04fc1-226">**Input stats** (solo bolt): informazioni sui flussi di input usati dal bolt.</span><span class="sxs-lookup"><span data-stu-id="04fc1-226">**Input stats** (bolt only): Information about the input streams consumed by the bolt.</span></span>
* <span data-ttu-id="04fc1-227">**Output stats**: informazioni sui flussi generati dallo spout o dal bolt.</span><span class="sxs-lookup"><span data-stu-id="04fc1-227">**Output stats**: Information about the streams emitted by this spout or bolt.</span></span>
* <span data-ttu-id="04fc1-228">**Executors**: informazioni sulle istanze dello spout o del bolt.</span><span class="sxs-lookup"><span data-stu-id="04fc1-228">**Executors**: Information about the instances of the spout or bolt.</span></span> <span data-ttu-id="04fc1-229">Selezionare la voce **Port** relativa a un esecutore specifico per visualizzare il log delle informazioni di diagnostica generate per questa istanza.</span><span class="sxs-lookup"><span data-stu-id="04fc1-229">Select the **Port** entry for a specific executor to view a log of diagnostic information produced for this instance.</span></span>
* <span data-ttu-id="04fc1-230">**Errors**: informazioni su eventuali errori dello spout o del bolt.</span><span class="sxs-lookup"><span data-stu-id="04fc1-230">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="monitor-and-manage-rest-api"></a><span data-ttu-id="04fc1-231">Monitorare e gestire: API REST</span><span class="sxs-lookup"><span data-stu-id="04fc1-231">Monitor and manage: REST API</span></span>

<span data-ttu-id="04fc1-232">L'interfaccia utente di Storm si basa sull'API REST. È pertanto possibile eseguire funzionalità di gestione e monitoraggio simili usando l'API REST.</span><span class="sxs-lookup"><span data-stu-id="04fc1-232">The Storm UI is built on top of the REST API, so you can perform similar management and monitoring functionality by using the REST API.</span></span> <span data-ttu-id="04fc1-233">L'API REST consente di creare strumenti personalizzati per la gestione e il monitoraggio di topologie Storm.</span><span class="sxs-lookup"><span data-stu-id="04fc1-233">You can use the REST API to create custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="04fc1-234">Per altre informazioni, vedere l'articolo relativo all'[API REST dell'interfaccia utente di Storm](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span><span class="sxs-lookup"><span data-stu-id="04fc1-234">For more information, see [Storm UI REST API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span></span> <span data-ttu-id="04fc1-235">Le seguenti informazioni sono specifiche per l'uso dell'API REST con Apache Storm in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="04fc1-235">The following information is specific to using the REST API with Apache Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="04fc1-236">L'API REST di Storm non è disponibile pubblicamente su Internet ed è necessario accedervi usando un tunnel SSH al nodo head del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="04fc1-236">The Storm REST API is not publicly available over the internet, and must be accessed using an SSH tunnel to the HDInsight cluster head node.</span></span> <span data-ttu-id="04fc1-237">Per informazioni sulla creazione e sull'uso di un tunnel SSH, vedere [Usare il tunneling SSH per accedere all'interfaccia Web di Ambari, ResourceManager, JobHistory, NameNode, Oozie e altre interfacce Web](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="04fc1-237">For information on creating and using an SSH tunnel, see [Use SSH Tunneling to access Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UIs](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

### <a name="base-uri"></a><span data-ttu-id="04fc1-238">URI di base</span><span class="sxs-lookup"><span data-stu-id="04fc1-238">Base URI</span></span>

<span data-ttu-id="04fc1-239">L'URI di base per l'API REST nei cluster HDInsight basati su Linux sono disponibili nel nodo head in **https://HEADNODEFQDN:8744/api/v1/**.</span><span class="sxs-lookup"><span data-stu-id="04fc1-239">The base URI for the REST API on Linux-based HDInsight clusters is available on the head node at **https://HEADNODEFQDN:8744/api/v1/**.</span></span> <span data-ttu-id="04fc1-240">Il nome di dominio del nodo head viene generato durante la creazione del cluster e non è statico.</span><span class="sxs-lookup"><span data-stu-id="04fc1-240">The domain name of the head node is generated during cluster creation and is not static.</span></span>

<span data-ttu-id="04fc1-241">È possibile trovare il nome di dominio completo (FQDN) per il nodo head del cluster in diversi modi:</span><span class="sxs-lookup"><span data-stu-id="04fc1-241">You can find the fully qualified domain name (FQDN) for the cluster head node in several different ways:</span></span>

* <span data-ttu-id="04fc1-242">**Da una sessione SSH**: usare il comando `headnode -f` da una sessione SSH al cluster.</span><span class="sxs-lookup"><span data-stu-id="04fc1-242">**From an SSH session**: Use the command `headnode -f` from an SSH session to the cluster.</span></span>
* <span data-ttu-id="04fc1-243">**Da Ambari Web**: selezionare **Services** (Servizi) nella parte superiore della pagina, quindi selezionare **Storm**.</span><span class="sxs-lookup"><span data-stu-id="04fc1-243">**From Ambari Web**: Select **Services** from the top of the page, then select **Storm**.</span></span> <span data-ttu-id="04fc1-244">Dalla scheda **Riepilogo** selezionare **Storm UI Server** (Server dell'interfaccia utente di Storm).</span><span class="sxs-lookup"><span data-stu-id="04fc1-244">From the **Summary** tab, select **Storm UI Server**.</span></span> <span data-ttu-id="04fc1-245">Il nome FQDN del nodo su cui sono in esecuzione l'interfaccia utente di Storm e le API REST sarà nella parte superiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="04fc1-245">The FQDN of the node that the Storm UI and REST API is running is at the top of the page.</span></span>
* <span data-ttu-id="04fc1-246">**Dall'API REST Ambari**: usare il comando `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` per recuperare informazioni sul nodo in cui sono in esecuzione l'interfaccia utente di Storm e l'API REST.</span><span class="sxs-lookup"><span data-stu-id="04fc1-246">**From Ambari REST API**: Use the command `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` to retrieve information about the node that the Storm UI and REST API are running on.</span></span> <span data-ttu-id="04fc1-247">Sostituire **PASSWORD** con la password di amministratore per il cluster.</span><span class="sxs-lookup"><span data-stu-id="04fc1-247">Replace **PASSWORD** with the admin password for the cluster.</span></span> <span data-ttu-id="04fc1-248">Sostituire **CLUSTERNAME** con il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="04fc1-248">Replace **CLUSTERNAME** with the cluster name.</span></span> <span data-ttu-id="04fc1-249">Nella risposta, la voce "host_name" contiene il nome di dominio completo del nodo.</span><span class="sxs-lookup"><span data-stu-id="04fc1-249">In the response, the "host_name" entry contains the FQDN of the node.</span></span>

### <a name="authentication"></a><span data-ttu-id="04fc1-250">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="04fc1-250">Authentication</span></span>

<span data-ttu-id="04fc1-251">Le richieste all'API REST devono usare l' **autenticazione di base**con il nome e la password amministratore del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="04fc1-251">Requests to the REST API must use **basic authentication**, so you use the HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="04fc1-252">Poiché l'autenticazione di base viene inviata in testo non crittografato, è necessario usare **sempre** HTTPS per proteggere le comunicazioni con il cluster.</span><span class="sxs-lookup"><span data-stu-id="04fc1-252">Because basic authentication is sent by using clear text, you should **always** use HTTPS to secure communications with the cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="04fc1-253">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="04fc1-253">Return values</span></span>

<span data-ttu-id="04fc1-254">Le informazioni restituite dall'API REST possono essere usate solo nel cluster o nei computer che si trovano nella stessa rete virtuale di Azure del cluster.</span><span class="sxs-lookup"><span data-stu-id="04fc1-254">Information that is returned from the REST API may only be usable from within the cluster or virtual machines on the same Azure Virtual Network as the cluster.</span></span> <span data-ttu-id="04fc1-255">Ad esempio, il nome di dominio completo (FQDN) restituito per i server Zookeeper non è accessibile da Internet.</span><span class="sxs-lookup"><span data-stu-id="04fc1-255">For example, the fully qualified domain name (FQDN) returned for Zookeeper servers is not be accessible from the Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04fc1-256">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="04fc1-256">Next Steps</span></span>

<span data-ttu-id="04fc1-257">A questo punto, dopo aver appreso come distribuire e monitorare le topologie usando Storm Dashboard, è possibile passare all'argomento [Sviluppare topologie basate su Java usando Maven](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="04fc1-257">Now that you've learned how to deploy and monitor topologies by using the Storm Dashboard, learn how to [Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="04fc1-258">Per un elenco di altre topologie di esempio, vedere [Esempi di topologie Storm per Apache Storm in HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="04fc1-258">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
