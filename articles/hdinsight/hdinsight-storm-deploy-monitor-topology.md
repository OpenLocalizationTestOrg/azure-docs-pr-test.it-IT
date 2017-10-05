---
title: Distribuire e gestire topologie Apache Storm in HDInsight | Documentazione Microsoft
description: Informazioni su come distribuire, monitorare e gestire le topologie Apache Storm mediante Storm Dashboard in HDInsight. Utilizzare gli strumenti Hadoop per Visual Studio
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5e542072-f014-42aa-82d6-2694a76df520
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 34072574f83b51280e60e2f8766c6c5d5a33c307
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a><span data-ttu-id="9fa6f-104">Distribuire e gestire topologie Apache Storm in HDInsight basato su Windows</span><span class="sxs-lookup"><span data-stu-id="9fa6f-104">Deploy and manage Apache Storm topologies on Windows-based HDInsight</span></span>

<span data-ttu-id="9fa6f-105">Storm Dashboard consente di distribuire e gestire facilmente topologie Apache Storm nel cluster mediante il Web browser in uso.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-105">The Storm Dashboard allows you to easily deploy and run Apache Storm topologies to your HDInsight cluster by using your web browser.</span></span> <span data-ttu-id="9fa6f-106">È possibile usare il dashboard anche per monitorare e gestire topologie in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-106">You can also use the dashboard to monitor and manage running topologies.</span></span> <span data-ttu-id="9fa6f-107">Se si usa Visual Studio, HDInsight Tools per Visual Studio fornisce funzionalità simili in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-107">If you use Visual Studio, the HDInsight Tools for Visual Studio provide similar features in Visual Studio.</span></span>

<span data-ttu-id="9fa6f-108">Storm Dashboard e le funzionalità Storm di HDInsight Tools si basano sull'API REST Storm, che consente di creare soluzioni di monitoraggio e gestione.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-108">The Storm Dashboard and the Storm features in the HDInsight Tools rely on the Storm REST API, which can be used to create your own monitoring and management solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fa6f-109">I passaggi descritti in questo documento richiedono un cluster Storm in HDInsight che usa il sistema operativo Windows.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-109">The steps in this document require a Storm on HDInsight cluster that uses Windows as the operating system.</span></span> <span data-ttu-id="9fa6f-110">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9fa6f-111">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="9fa6f-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="9fa6f-112">Per informazioni sulla distribuzione e gestione di topologie Storm con un cluster HDInsight che usa Linux, vedere [Distribuzione e gestione di topologie Apache Storm in HDInsight basato su Linux](hdinsight-storm-deploy-monitor-topology-linux.md)</span><span class="sxs-lookup"><span data-stu-id="9fa6f-112">For information on deploying and managing Storm topologies with an HDInsight cluster that uses Linux, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9fa6f-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9fa6f-113">Prerequisites</span></span>

* <span data-ttu-id="9fa6f-114">**Apache Storm in HDInsight**: per i passaggi relativi alla creazione di un cluster, vedere [Introduzione ad Apache Storm con HDInsight](hdinsight-apache-storm-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9fa6f-114">**Apache Storm on HDInsight** - see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started.md) for steps on creating a cluster.</span></span>

* <span data-ttu-id="9fa6f-115">Per **Storm Dashboard**: un Web browser di ultima generazione che supporta HTML5.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-115">For the **Storm Dashboard**: A modern web browser that supports HTML5.</span></span>

* <span data-ttu-id="9fa6f-116">Per **Visual Studio** : Azure SDK 2.5.1 o versione successiva e HDInsight Tools per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-116">For **Visual Studio** - Azure SDK 2.5.1 or newer and the HDInsight Tools for Visual Studio.</span></span> <span data-ttu-id="9fa6f-117">Per installare e configurare gli strumenti HDInsight per Visual Studio, vedere [Introduzione all'uso di HDInsight Tools per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9fa6f-117">See [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) to install and configure the HDInsight tools for Visual Studio.</span></span>

    <span data-ttu-id="9fa6f-118">Una delle seguenti versioni di Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="9fa6f-118">One of the following versions of Visual Studio:</span></span>

  * <span data-ttu-id="9fa6f-119">Visual Studio 2012 con Update 4</span><span class="sxs-lookup"><span data-stu-id="9fa6f-119">Visual Studio 2012 with Update 4</span></span>

  * <span data-ttu-id="9fa6f-120">Visual Studio 2013 con Update 4 o Visual Studio 2013 Community</span><span class="sxs-lookup"><span data-stu-id="9fa6f-120">Visual Studio 2013 with Update 4 or Visual Studio 2013 Community</span></span>

  * <span data-ttu-id="9fa6f-121">Visual Studio 2015, qualsiasi edizione</span><span class="sxs-lookup"><span data-stu-id="9fa6f-121">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="9fa6f-122">Visual Studio 2017, qualsiasi edizione</span><span class="sxs-lookup"><span data-stu-id="9fa6f-122">Visual Studio 2017 (any edition)</span></span>

## <a name="storm-dashboard"></a><span data-ttu-id="9fa6f-123">Storm Dashboard</span><span class="sxs-lookup"><span data-stu-id="9fa6f-123">Storm Dashboard</span></span>

<span data-ttu-id="9fa6f-124">Dashboard di Storm è una pagina Web disponibile nel cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-124">The Storm Dashboard is a web page available on your Storm cluster.</span></span> <span data-ttu-id="9fa6f-125">L'URL è **https://&lt;NomeCluster>.azurehdinsight.net/**, dove **NomeCluster** è il nome del cluster Storm in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-125">The URL is **https://&lt;clustername>.azurehdinsight.net/**, where **clustername** is the name of your Storm on HDInsight cluster.</span></span>

<span data-ttu-id="9fa6f-126">Nella parte superiore di Storm Dashboard selezionare **Submit Topology**.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-126">From the top of the Storm Dashboard, select **Submit Topology**.</span></span> <span data-ttu-id="9fa6f-127">Seguire le istruzioni visualizzate nella pagina per eseguire una topologia di esempio o per caricare ed eseguire una topologia creata.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-127">Follow the instructions on the page to run a sample topology or to upload and run a topology that you created.</span></span>

![pagina Submit Topology][storm-dashboard-submit]

### <a name="storm-ui"></a><span data-ttu-id="9fa6f-129">Interfaccia utente di Storm</span><span class="sxs-lookup"><span data-stu-id="9fa6f-129">Storm UI</span></span>

<span data-ttu-id="9fa6f-130">In Storm Dashboard selezionare il collegamento **Storm UI** .</span><span class="sxs-lookup"><span data-stu-id="9fa6f-130">From the Storm Dashboard, select the **Storm UI** link.</span></span> <span data-ttu-id="9fa6f-131">Vengono visualizzate informazioni sul cluster, nonché l'elenco delle topologie in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-131">This displays information about the cluster, in addition to any running topologies.</span></span>

![interfaccia utente Storm][storm-dashboard-ui]

> [!NOTE]
> <span data-ttu-id="9fa6f-133">Con alcune versioni di Internet Explorer, potrebbe risultare che l'interfaccia utente di Storm non viene aggiornata dopo il primo utilizzo.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-133">With some versions of Internet Explorer, you may discover that the Storm UI does not refresh after you have first visited it.</span></span> <span data-ttu-id="9fa6f-134">Ad esempio, potrebbero non essere visibili nuove topologie inviate oppure potrebbe risultare ancora attiva la visualizzazione di una topologia precedentemente disattivata.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-134">For example, it may not show the new topologies you submitted, or it may show a topology as active when you previously deactivated it.</span></span> <span data-ttu-id="9fa6f-135">Microsoft è al corrente di questo problema e sta lavorando a una soluzione.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-135">Microsoft is aware of this issue and is working on a solution.</span></span>

#### <a name="main-page"></a><span data-ttu-id="9fa6f-136">Pagina principale</span><span class="sxs-lookup"><span data-stu-id="9fa6f-136">Main page</span></span>

<span data-ttu-id="9fa6f-137">Nella pagina principale dell'interfaccia utente di Storm sono disponibili le informazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-137">The main page of the Storm UI provides the following information:</span></span>

* <span data-ttu-id="9fa6f-138">**Cluster summary**: informazioni di base sul cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-138">**Cluster summary**: Basic information about the Storm cluster.</span></span>

* <span data-ttu-id="9fa6f-139">**Topology summary**: elenco delle topologie in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-139">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="9fa6f-140">Usare i collegamenti disponibili in questa sezione per visualizzare ulteriori informazioni su topologie specifiche.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-140">Use the links in this section to view more information about specific topologies.</span></span>

* <span data-ttu-id="9fa6f-141">**Supervisor summary**: informazioni su Storm Supervisor.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-141">**Supervisor summary**: Information about the Storm supervisor.</span></span>

* <span data-ttu-id="9fa6f-142">**Nimbus configuration**: configurazione Nimbus per il cluster.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-142">**Nimbus configuration**: Nimbus configuration for the cluster.</span></span>

#### <a name="topology-summary"></a><span data-ttu-id="9fa6f-143">Topology summary</span><span class="sxs-lookup"><span data-stu-id="9fa6f-143">Topology summary</span></span>

<span data-ttu-id="9fa6f-144">Se si seleziona un collegamento nella sezione **Topology summary** , verranno visualizzate le informazioni seguenti sulla topologia.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-144">Selecting a link from the **Topology summary** section displays the following information about the topology:</span></span>

* <span data-ttu-id="9fa6f-145">**Topology summary**: informazioni di base sulla topologia.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-145">**Topology summary**: Basic information about the topology.</span></span>

* <span data-ttu-id="9fa6f-146">**Topology actions**: azioni di gestione che è possibile eseguire per la topologia.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-146">**Topology actions**: Management actions that you can perform for the topology.</span></span>

  * <span data-ttu-id="9fa6f-147">**Activate**: riprende l'elaborazione di una topologia disattivata.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-147">**Activate**: Resumes processing of a deactivated topology.</span></span>

  * <span data-ttu-id="9fa6f-148">**Deactivate**: sospende una topologia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-148">**Deactivate**: Pauses a running topology.</span></span>

  * <span data-ttu-id="9fa6f-149">**Rebalance**: regola il parallelismo della topologia.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-149">**Rebalance**: Adjusts the parallelism of the topology.</span></span> <span data-ttu-id="9fa6f-150">È necessario ribilanciare le topologie in esecuzione dopo aver modificato il numero di nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-150">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span></span> <span data-ttu-id="9fa6f-151">Questo consente alla topologia di regolare il parallelismo per compensare l'aumento o la diminuzione del numero di nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-151">This allows the topology to adjust parallelism to compensate for the increased or decreased number of nodes in the cluster.</span></span>

      <span data-ttu-id="9fa6f-152">Per altre informazioni, vedere [Understanding the parallelism of a Storm topology (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) (Informazioni sul parallelismo di una topologia Storm).</span><span class="sxs-lookup"><span data-stu-id="9fa6f-152">For more information, see [Understanding the parallelism of a Storm topology (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

  * <span data-ttu-id="9fa6f-153">**Kill**: termina una topologia Storm dopo il timeout specificato.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-153">**Kill**: Terminates a Storm topology after the specified timeout.</span></span>

* <span data-ttu-id="9fa6f-154">**Topology stats**: statistiche sulla topologia.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-154">**Topology stats**: Statistics about the topology.</span></span> <span data-ttu-id="9fa6f-155">Usare i collegamenti disponibili nella colonna **Window** per impostare l'intervallo di tempo per le rimanenti voci della pagina.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-155">Use the links in the **Window** column to set the timeframe for the remaining entries on the page.</span></span>

* <span data-ttu-id="9fa6f-156">**Spouts**: spout usati dalla topologia.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-156">**Spouts**: The spouts used by the topology.</span></span> <span data-ttu-id="9fa6f-157">Usare i collegamenti disponibili in questa sezione per visualizzare ulteriori informazioni su spout specifici.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-157">Use the links in this section to view more information about specific spouts.</span></span>

* <span data-ttu-id="9fa6f-158">**Bolts**: bolt usati nella topologia.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-158">**Bolts**: The bolts used by the topology.</span></span> <span data-ttu-id="9fa6f-159">Usare i collegamenti disponibili in questa sezione per visualizzare ulteriori informazioni su bolt specifici.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-159">Use the links in this section to view more information about specific bolts.</span></span>

* <span data-ttu-id="9fa6f-160">**Topology configuration**: configurazione della topologia selezionata.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-160">**Topology configuration**: The configuration of the selected topology.</span></span>

#### <a name="spout-and-bolt-summary"></a><span data-ttu-id="9fa6f-161">Riepilogo di spout e bolt</span><span class="sxs-lookup"><span data-stu-id="9fa6f-161">Spout and Bolt summary</span></span>

<span data-ttu-id="9fa6f-162">Se si seleziona un elemento nella sezione **Spouts** o **Bolts**, verranno visualizzate le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="9fa6f-162">Selecting a spout from the **Spouts** or **Bolts** sections displays the following information about the selected item:</span></span>

* <span data-ttu-id="9fa6f-163">**Component summary**: informazioni di base sullo spout o sul bolt.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-163">**Component summary**: Basic information about the spout or bolt.</span></span>

* <span data-ttu-id="9fa6f-164">**Spout/Bolt stats**: statistiche relative allo spout o al bolt.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-164">**Spout/Bolt stats**: Statistics about the spout or bolt.</span></span> <span data-ttu-id="9fa6f-165">Usare i collegamenti disponibili nella colonna **Window** per impostare l'intervallo di tempo per le rimanenti voci della pagina.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-165">Use the links in the **Window** column to set the timeframe for the remaining entries on the page.</span></span>

* <span data-ttu-id="9fa6f-166">**Input stats** (solo bolt): informazioni sui flussi di input usati dal bolt.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-166">**Input stats** (bolt only): Information about the input streams consumed by the bolt.</span></span>

* <span data-ttu-id="9fa6f-167">**Output stats**: informazioni sui flussi generati dallo spout o dal bolt.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-167">**Output stats**: Information about the streams emitted by this spout or bolt.</span></span>

* <span data-ttu-id="9fa6f-168">**Executors**: informazioni sulle istanze dello spout o del bolt.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-168">**Executors**: Information about the instances of the spout or bolt.</span></span> <span data-ttu-id="9fa6f-169">Selezionare la voce **Port** relativa a un esecutore specifico per visualizzare il log delle informazioni di diagnostica generate per questa istanza.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-169">Select the **Port** entry for a specific executor to view a log of diagnostic information produced for this instance.</span></span>

* <span data-ttu-id="9fa6f-170">**Errors**: informazioni su eventuali errori dello spout o del bolt.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-170">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="hdinsight-tools-for-visual-studio"></a><span data-ttu-id="9fa6f-171">HDInsight Tools per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9fa6f-171">HDInsight Tools for Visual Studio</span></span>

<span data-ttu-id="9fa6f-172">HDInsight Tools consente di inviare topologie C# o ibride al cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-172">The HDInsight Tools can be used to submit C# or hybrid topologies to your Storm cluster.</span></span> <span data-ttu-id="9fa6f-173">Nei seguenti passaggi viene usata un'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-173">The following steps use a sample application.</span></span> <span data-ttu-id="9fa6f-174">Per informazioni sulla creazione delle proprie tipologie, vedere [Sviluppare topologie C# per Apache Storm in HDInsight tramite Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="9fa6f-174">For information about creating your own topologies by using the HDInsight Tools, see [Develop C# topologies using the HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="9fa6f-175">Eseguire i passaggi seguenti per distribuire una topologia di esempio nel cluster Storm in HDInsight e quindi visualizzare e gestire tale topologia.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-175">Use the following steps to deploy a sample to your Storm on HDInsight cluster, then view and manage the topology.</span></span>

1. <span data-ttu-id="9fa6f-176">Se la versione più recente di HDInsight Tools per Visual Studio non è ancora installata, vedere [Introduzione all'uso di HDInsight Tools per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9fa6f-176">If you have not already installed the latest version of the HDInsight Tools for Visual Studio, see [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="9fa6f-177">Aprire Visual Studio e selezionare **File** > **Nuovo** > **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-177">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="9fa6f-178">Nella finestra di dialogo **Nuovo progetto** espandere **Installato** > **Modelli** e quindi selezionare **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-178">In the **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="9fa6f-179">Dall'elenco dei modelli selezionare **Storm Sample**.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-179">From the list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="9fa6f-180">Nella parte inferiore della finestra di dialogo digitare un nome per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-180">At the bottom of the dialog box, type a name for the application.</span></span>

    ![immagine](./media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. <span data-ttu-id="9fa6f-182">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto e selezionare **Submit to Storm on HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-182">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9fa6f-183">Se richiesto, immettere le credenziali di accesso per la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-183">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="9fa6f-184">Se si dispone di più di una sottoscrizione, accedere a quella che contiene il cluster Storm in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-184">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="9fa6f-185">Selezionare il cluster Storm in HDInsight dall'elenco a discesa **Storm Cluster** e quindi selezionare **Submit**.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-185">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="9fa6f-186">È possibile verificare se l'invio è riuscito o meno usando la finestra **Output** .</span><span class="sxs-lookup"><span data-stu-id="9fa6f-186">You can monitor whether the submission is successful by using the **Output** window.</span></span>

6. <span data-ttu-id="9fa6f-187">Dopo che la topologia è stata inviata correttamente, verrà visualizzato l'elenco **Storm Topologies** relativo al cluster.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-187">When the topology has been successfully submitted, the **Storm Topologies** for the cluster should appear.</span></span> <span data-ttu-id="9fa6f-188">Per visualizzare informazioni sulla topologia in esecuzione, selezionarla dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-188">Select the topology from the list to view information about the running topology.</span></span>

    ![monitor Visual Studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > <span data-ttu-id="9fa6f-190">È possibile visualizzare **Storm Topologies** anche da **Esplora server**, espandendo **Azure** > **HDInsight** e quindi facendo clic su un cluster Storm in HDInsight e selezionando **View Storm Topologies**.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-190">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

    <span data-ttu-id="9fa6f-191">Selezionare la forma degli spout o dei bolt per visualizzare informazioni su questi componenti.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-191">Select the shape for the spouts or bolts to view information about these components.</span></span> <span data-ttu-id="9fa6f-192">Viene aperta una nuova finestra per ogni elemento selezionato.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-192">A new window opens for each item selected.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9fa6f-193">Il nome della topologia è il nome della classe della topologia, in questo caso `HelloWord`, a cui è stato aggiunto un timestamp.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-193">The name of the topology is the class name of the topology (in this case, `HelloWord`,) with a timestamp appended.</span></span>

7. <span data-ttu-id="9fa6f-194">Nella visualizzazione **Topology Summary** selezionare **Kill** per arrestare la topologia.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-194">From the **Topology Summary** view, select **Kill** to stop the topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9fa6f-195">Le topologie Storm continuano l'esecuzione fino a quando non vengono arrestate o fino a quando il cluster non viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-195">Storm topologies continue running until they are stopped or the cluster is deleted.</span></span>


## <a name="rest-api"></a><span data-ttu-id="9fa6f-196">API REST</span><span class="sxs-lookup"><span data-stu-id="9fa6f-196">REST API</span></span>

<span data-ttu-id="9fa6f-197">L'interfaccia utente di Storm si basa sull'API REST. È pertanto possibile eseguire funzionalità di gestione e monitoraggio simili usando l'API REST.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-197">The Storm UI is built on top of the REST API, so you can perform similar management and monitoring functionality by using the REST API.</span></span> <span data-ttu-id="9fa6f-198">L'API REST consente di creare strumenti personalizzati per la gestione e il monitoraggio di topologie Storm.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-198">You can use the REST API to create custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="9fa6f-199">Per altre informazioni, vedere l'articolo relativo all'[API REST dell'interfaccia utente di Storm](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span><span class="sxs-lookup"><span data-stu-id="9fa6f-199">For more information, see [Storm UI REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span></span> <span data-ttu-id="9fa6f-200">Le seguenti informazioni sono specifiche per l'uso dell'API REST con Apache Storm in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-200">The following information is specific to using the REST API with Apache Storm on HDInsight.</span></span>

### <a name="base-uri"></a><span data-ttu-id="9fa6f-201">URI di base</span><span class="sxs-lookup"><span data-stu-id="9fa6f-201">Base URI</span></span>

<span data-ttu-id="9fa6f-202">L'URI di base per l'API REST nei cluster HDInsight è **https://&lt;NomeCluster>.azurehdinsight.net/stormui/api/v1/**, dove **NomeCluster** è il nome del cluster Storm in HDInsight in uso.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-202">The base URI for the REST API on HDInsight clusters is **https://&lt;clustername>.azurehdinsight.net/stormui/api/v1/**, where **clustername** is the name of your Storm on HDInsight cluster.</span></span>

### <a name="authentication"></a><span data-ttu-id="9fa6f-203">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="9fa6f-203">Authentication</span></span>

<span data-ttu-id="9fa6f-204">Le richieste all'API REST devono usare l' **autenticazione di base**con il nome e la password amministratore del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-204">Requests to the REST API must use **basic authentication**, so you use the HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="9fa6f-205">Poiché l'autenticazione di base viene inviata in testo non crittografato, è necessario usare **sempre** HTTPS per proteggere le comunicazioni con il cluster.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-205">Because basic authentication is sent by using clear text, you should **always** use HTTPS to secure communications with the cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fa6f-206">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9fa6f-206">Return values</span></span>

<span data-ttu-id="9fa6f-207">Le informazioni restituite dall'API REST possono essere usate solo nel cluster o nei computer che si trovano nella stessa rete virtuale di Azure del cluster.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-207">Information that is returned from the REST API may only be usable from within the cluster or virtual machines on the same Azure Virtual Network as the cluster.</span></span> <span data-ttu-id="9fa6f-208">Ad esempio, il nome di dominio completo (FQDN) restituito per i server Zookeeper non è accessibile da Internet.</span><span class="sxs-lookup"><span data-stu-id="9fa6f-208">For example, the fully qualified domain name (FQDN) returned for Zookeeper servers are not be accessible from the Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fa6f-209">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9fa6f-209">Next Steps</span></span>

<span data-ttu-id="9fa6f-210">A questo punto, dopo aver appreso come distribuire e monitorare le topologie usando Storm Dashboard, è possibile passare agli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="9fa6f-210">Now that you've learned how to deploy and monitor topologies by using the Storm Dashboard, learn how to:</span></span>

* [<span data-ttu-id="9fa6f-211">Sviluppare topologie C# per Apache Storm in HDInsight tramite Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9fa6f-211">Develop C# topologies using the HDInsight Tools for Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [<span data-ttu-id="9fa6f-212">Sviluppare topologie basate su Java per Apache Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="9fa6f-212">Develop Java-based topologies using Maven</span></span>](hdinsight-storm-develop-java-topology.md)

<span data-ttu-id="9fa6f-213">Per un elenco di altre topologie di esempio, vedere [Esempi di topologie Storm per Apache Storm in HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="9fa6f-213">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

[hdinsight-dashboard]: ./media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png
