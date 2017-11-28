---
title: aaaDeploy e gestire le topologie di Apache Storm in HDInsight | Documenti Microsoft
description: Informazioni su come toodeploy, monitorare e gestire le topologie di Apache Storm tramite Dashboard Storm hello in HDInsight. Utilizzare gli strumenti Hadoop per Visual Studio
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
ms.openlocfilehash: 05f05fe8dd519fe99fb771d36bfc3d28168ca85f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a><span data-ttu-id="bc7c7-104">Distribuire e gestire topologie Apache Storm in HDInsight basato su Windows</span><span class="sxs-lookup"><span data-stu-id="bc7c7-104">Deploy and manage Apache Storm topologies on Windows-based HDInsight</span></span>

<span data-ttu-id="bc7c7-105">Hello Storm Dashboard consente tooeasily distribuire ed eseguire i cluster di HDInsight tooyour topologie Apache Storm tramite il web browser.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-105">hello Storm Dashboard allows you tooeasily deploy and run Apache Storm topologies tooyour HDInsight cluster by using your web browser.</span></span> <span data-ttu-id="bc7c7-106">È anche possibile utilizzare toomonitor dashboard hello e gestire topologie in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-106">You can also use hello dashboard toomonitor and manage running topologies.</span></span> <span data-ttu-id="bc7c7-107">Se si utilizza Visual Studio, hello HDInsight Tools per Visual Studio fornisce funzionalità simili in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-107">If you use Visual Studio, hello HDInsight Tools for Visual Studio provide similar features in Visual Studio.</span></span>

<span data-ttu-id="bc7c7-108">Hello Storm Dashboard e le funzionalità di Storm hello hello strumenti HDInsight si basano su hello Storm l'API REST che può essere utilizzato toocreate proprie soluzioni di monitoraggio e gestione.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-108">hello Storm Dashboard and hello Storm features in hello HDInsight Tools rely on hello Storm REST API, which can be used toocreate your own monitoring and management solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bc7c7-109">passaggi di Hello in questo documento richiedono un elevato numero di cluster HDInsight che usa Windows come sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-109">hello steps in this document require a Storm on HDInsight cluster that uses Windows as hello operating system.</span></span> <span data-ttu-id="bc7c7-110">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="bc7c7-111">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="bc7c7-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="bc7c7-112">Per informazioni sulla distribuzione e gestione di topologie Storm con un cluster HDInsight che usa Linux, vedere [Distribuzione e gestione di topologie Apache Storm in HDInsight basato su Linux](hdinsight-storm-deploy-monitor-topology-linux.md)</span><span class="sxs-lookup"><span data-stu-id="bc7c7-112">For information on deploying and managing Storm topologies with an HDInsight cluster that uses Linux, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc7c7-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bc7c7-113">Prerequisites</span></span>

* <span data-ttu-id="bc7c7-114">**Apache Storm in HDInsight**: per i passaggi relativi alla creazione di un cluster, vedere [Introduzione ad Apache Storm con HDInsight](hdinsight-apache-storm-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bc7c7-114">**Apache Storm on HDInsight** - see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started.md) for steps on creating a cluster.</span></span>

* <span data-ttu-id="bc7c7-115">Per hello **Dashboard Storm**: un browser web moderna che supporta HTML5.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-115">For hello **Storm Dashboard**: A modern web browser that supports HTML5.</span></span>

* <span data-ttu-id="bc7c7-116">Per **Visual Studio** -Azure SDK 2.5.1 o versione successiva e hello strumenti HDInsight per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-116">For **Visual Studio** - Azure SDK 2.5.1 or newer and hello HDInsight Tools for Visual Studio.</span></span> <span data-ttu-id="bc7c7-117">Vedere [iniziare a usare gli strumenti HDInsight per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall e configurare gli strumenti di HDInsight hello per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-117">See [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall and configure hello HDInsight tools for Visual Studio.</span></span>

    <span data-ttu-id="bc7c7-118">Una delle seguenti versioni di Visual Studio hello:</span><span class="sxs-lookup"><span data-stu-id="bc7c7-118">One of hello following versions of Visual Studio:</span></span>

  * <span data-ttu-id="bc7c7-119">Visual Studio 2012 con Update 4</span><span class="sxs-lookup"><span data-stu-id="bc7c7-119">Visual Studio 2012 with Update 4</span></span>

  * <span data-ttu-id="bc7c7-120">Visual Studio 2013 con Update 4 o Visual Studio 2013 Community</span><span class="sxs-lookup"><span data-stu-id="bc7c7-120">Visual Studio 2013 with Update 4 or Visual Studio 2013 Community</span></span>

  * <span data-ttu-id="bc7c7-121">Visual Studio 2015, qualsiasi edizione</span><span class="sxs-lookup"><span data-stu-id="bc7c7-121">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="bc7c7-122">Visual Studio 2017, qualsiasi edizione</span><span class="sxs-lookup"><span data-stu-id="bc7c7-122">Visual Studio 2017 (any edition)</span></span>

## <a name="storm-dashboard"></a><span data-ttu-id="bc7c7-123">Storm Dashboard</span><span class="sxs-lookup"><span data-stu-id="bc7c7-123">Storm Dashboard</span></span>

<span data-ttu-id="bc7c7-124">Hello Storm Dashboard è una pagina web disponibile sul cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-124">hello Storm Dashboard is a web page available on your Storm cluster.</span></span> <span data-ttu-id="bc7c7-125">URL di Hello è **https://&lt;clustername >.azurehdinsight.net/**, dove **clustername** è il nome di hello dell'elevato numero di cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-125">hello URL is **https://&lt;clustername>.azurehdinsight.net/**, where **clustername** is hello name of your Storm on HDInsight cluster.</span></span>

<span data-ttu-id="bc7c7-126">Dall'alto hello di hello Storm Dashboard, selezionare **inviare topologia**.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-126">From hello top of hello Storm Dashboard, select **Submit Topology**.</span></span> <span data-ttu-id="bc7c7-127">Seguire le istruzioni di hello su hello pagina toorun una topologia di esempio o tooupload ed eseguire una topologia in cui è stato creato.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-127">Follow hello instructions on hello page toorun a sample topology or tooupload and run a topology that you created.</span></span>

![Hello Invia pagina topologia][storm-dashboard-submit]

### <a name="storm-ui"></a><span data-ttu-id="bc7c7-129">Interfaccia utente di Storm</span><span class="sxs-lookup"><span data-stu-id="bc7c7-129">Storm UI</span></span>

<span data-ttu-id="bc7c7-130">Hello Storm Dashboard, selezionare hello **dell'interfaccia utente Storm** collegamento.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-130">From hello Storm Dashboard, select hello **Storm UI** link.</span></span> <span data-ttu-id="bc7c7-131">Consente di visualizzare informazioni sul cluster hello, tooany aggiunta in topologie di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-131">This displays information about hello cluster, in addition tooany running topologies.</span></span>

![interfaccia utente di storm Hello][storm-dashboard-ui]

> [!NOTE]
> <span data-ttu-id="bc7c7-133">Con alcune versioni di Internet Explorer, si potrebbe scoprire che hello che Storm UI non comporta l'aggiornamento dopo aver visitato innanzitutto il.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-133">With some versions of Internet Explorer, you may discover that hello Storm UI does not refresh after you have first visited it.</span></span> <span data-ttu-id="bc7c7-134">Ad esempio, potrebbe non visualizzate topologie nuovo hello è stato inviato o potrebbe mostrare una topologia come attivo quando precedente disattivazione.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-134">For example, it may not show hello new topologies you submitted, or it may show a topology as active when you previously deactivated it.</span></span> <span data-ttu-id="bc7c7-135">Microsoft è al corrente di questo problema e sta lavorando a una soluzione.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-135">Microsoft is aware of this issue and is working on a solution.</span></span>

#### <a name="main-page"></a><span data-ttu-id="bc7c7-136">Pagina principale</span><span class="sxs-lookup"><span data-stu-id="bc7c7-136">Main page</span></span>

<span data-ttu-id="bc7c7-137">pagina principale di Hello di hello Storm UI fornisce hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="bc7c7-137">hello main page of hello Storm UI provides hello following information:</span></span>

* <span data-ttu-id="bc7c7-138">**Riepilogo di cluster**: informazioni di base sui cluster Storm hello.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-138">**Cluster summary**: Basic information about hello Storm cluster.</span></span>

* <span data-ttu-id="bc7c7-139">**Topology summary**: elenco delle topologie in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-139">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="bc7c7-140">Utilizzare collegamenti hello in questa sezione di tooview ulteriori informazioni sulle topologie specifiche.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-140">Use hello links in this section tooview more information about specific topologies.</span></span>

* <span data-ttu-id="bc7c7-141">**Riepilogo Supervisore**: informazioni su Supervisore Storm hello.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-141">**Supervisor summary**: Information about hello Storm supervisor.</span></span>

* <span data-ttu-id="bc7c7-142">**Configurazione nimbus**: configurazione di Nimbus per cluster hello.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-142">**Nimbus configuration**: Nimbus configuration for hello cluster.</span></span>

#### <a name="topology-summary"></a><span data-ttu-id="bc7c7-143">Topology summary</span><span class="sxs-lookup"><span data-stu-id="bc7c7-143">Topology summary</span></span>

<span data-ttu-id="bc7c7-144">Quando si seleziona un collegamento da hello **riepilogo topologia** sezione sono visualizzate le seguenti informazioni sulla topologia di hello hello:</span><span class="sxs-lookup"><span data-stu-id="bc7c7-144">Selecting a link from hello **Topology summary** section displays hello following information about hello topology:</span></span>

* <span data-ttu-id="bc7c7-145">**Topologia riepilogo**: le informazioni di base relative alla topologia di hello.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-145">**Topology summary**: Basic information about hello topology.</span></span>

* <span data-ttu-id="bc7c7-146">**Azioni di topologia**: azioni di gestione che è possibile eseguire per la topologia hello.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-146">**Topology actions**: Management actions that you can perform for hello topology.</span></span>

  * <span data-ttu-id="bc7c7-147">**Activate**: riprende l'elaborazione di una topologia disattivata.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-147">**Activate**: Resumes processing of a deactivated topology.</span></span>

  * <span data-ttu-id="bc7c7-148">**Deactivate**: sospende una topologia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-148">**Deactivate**: Pauses a running topology.</span></span>

  * <span data-ttu-id="bc7c7-149">**Ribilanciare**: consente di regolare il parallelismo hello della topologia hello.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-149">**Rebalance**: Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="bc7c7-150">È necessario ribilanciare topologie in esecuzione dopo avere modificato il numero di hello di nodi nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-150">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="bc7c7-151">In questo modo hello topologia tooadjust parallelismo toocompensate per hello aumentato o diminuito di numero di nodi nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-151">This allows hello topology tooadjust parallelism toocompensate for hello increased or decreased number of nodes in hello cluster.</span></span>

      <span data-ttu-id="bc7c7-152">Per ulteriori informazioni, vedere [comprensione parallelismo hello di una topologia di Storm (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="bc7c7-152">For more information, see [Understanding hello parallelism of a Storm topology (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

  * <span data-ttu-id="bc7c7-153">**Kill**: termina una topologia di Storm dopo hello specificato timeout.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-153">**Kill**: Terminates a Storm topology after hello specified timeout.</span></span>

* <span data-ttu-id="bc7c7-154">**Statistiche di topologia**: le statistiche relative alla topologia di hello.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-154">**Topology stats**: Statistics about hello topology.</span></span> <span data-ttu-id="bc7c7-155">Usare collegamenti hello hello **finestra** intervallo di tempo di colonna tooset hello per le voci nella pagina hello rimanenti hello.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-155">Use hello links in hello **Window** column tooset hello timeframe for hello remaining entries on hello page.</span></span>

* <span data-ttu-id="bc7c7-156">**Spouts**: hello spouts utilizzato dalla topologia hello.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-156">**Spouts**: hello spouts used by hello topology.</span></span> <span data-ttu-id="bc7c7-157">Usare i collegamenti di hello in questa sezione di tooview ulteriori informazioni su spouts specifico.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-157">Use hello links in this section tooview more information about specific spouts.</span></span>

* <span data-ttu-id="bc7c7-158">**Bulloni**: hello bulloni utilizzati dalla topologia hello.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-158">**Bolts**: hello bolts used by hello topology.</span></span> <span data-ttu-id="bc7c7-159">Usare i collegamenti di hello in questa sezione di tooview ulteriori informazioni su bulloni specifici.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-159">Use hello links in this section tooview more information about specific bolts.</span></span>

* <span data-ttu-id="bc7c7-160">**Configurazione della topologia**: configurazione di hello della topologia hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-160">**Topology configuration**: hello configuration of hello selected topology.</span></span>

#### <a name="spout-and-bolt-summary"></a><span data-ttu-id="bc7c7-161">Riepilogo di spout e bolt</span><span class="sxs-lookup"><span data-stu-id="bc7c7-161">Spout and Bolt summary</span></span>

<span data-ttu-id="bc7c7-162">Selezionando un beccuccio hello **Spouts** o **bulloni** sezioni Visualizza le seguenti informazioni sull'elemento selezionato hello hello:</span><span class="sxs-lookup"><span data-stu-id="bc7c7-162">Selecting a spout from hello **Spouts** or **Bolts** sections displays hello following information about hello selected item:</span></span>

* <span data-ttu-id="bc7c7-163">**Riepilogo dei componenti**: informazioni di base beccuccio hello o fulmine.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-163">**Component summary**: Basic information about hello spout or bolt.</span></span>

* <span data-ttu-id="bc7c7-164">**Statistiche beccuccio/fulmine**: le statistiche relative hello spout o bullone.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-164">**Spout/Bolt stats**: Statistics about hello spout or bolt.</span></span> <span data-ttu-id="bc7c7-165">Usare collegamenti hello hello **finestra** intervallo di tempo di colonna tooset hello per le voci nella pagina hello rimanenti hello.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-165">Use hello links in hello **Window** column tooset hello timeframe for hello remaining entries on hello page.</span></span>

* <span data-ttu-id="bc7c7-166">**Statistiche di input** (solo bullone): informazioni su hello flussi utilizzati da fulmine hello di input.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-166">**Input stats** (bolt only): Information about hello input streams consumed by hello bolt.</span></span>

* <span data-ttu-id="bc7c7-167">**Output statistiche**: informazioni sui flussi di hello generato da questo spout o bullone.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-167">**Output stats**: Information about hello streams emitted by this spout or bolt.</span></span>

* <span data-ttu-id="bc7c7-168">**Executor**: informazioni sulle istanze di hello di beccuccio hello o fulmine.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-168">**Executors**: Information about hello instances of hello spout or bolt.</span></span> <span data-ttu-id="bc7c7-169">Seleziona hello **porta** voce per tooview un esecutore specifico prodotto un log delle informazioni di diagnostica per questa istanza.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-169">Select hello **Port** entry for a specific executor tooview a log of diagnostic information produced for this instance.</span></span>

* <span data-ttu-id="bc7c7-170">**Errors**: informazioni su eventuali errori dello spout o del bolt.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-170">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="hdinsight-tools-for-visual-studio"></a><span data-ttu-id="bc7c7-171">HDInsight Tools per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bc7c7-171">HDInsight Tools for Visual Studio</span></span>

<span data-ttu-id="bc7c7-172">gli strumenti di HDInsight Hello può essere utilizzato toosubmit c# o ibrida topologie tooyour cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-172">hello HDInsight Tools can be used toosubmit C# or hybrid topologies tooyour Storm cluster.</span></span> <span data-ttu-id="bc7c7-173">Hello alla procedura seguente usa un'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-173">hello following steps use a sample application.</span></span> <span data-ttu-id="bc7c7-174">Per informazioni sulla creazione di propri topologie utilizzando gli strumenti di HDInsight hello, vedere [c# sviluppare topologie in hello HDInsight Tools per Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="bc7c7-174">For information about creating your own topologies by using hello HDInsight Tools, see [Develop C# topologies using hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="bc7c7-175">Utilizzare hello seguendo i passaggi toodeploy tooyour un esempio Storm nel cluster HDInsight, quindi visualizzare e gestire la topologia di hello.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-175">Use hello following steps toodeploy a sample tooyour Storm on HDInsight cluster, then view and manage hello topology.</span></span>

1. <span data-ttu-id="bc7c7-176">Se non è già installato hello versione hello strumenti HDInsight per Visual Studio, vedere [iniziare a usare gli strumenti HDInsight per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bc7c7-176">If you have not already installed hello latest version of hello HDInsight Tools for Visual Studio, see [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="bc7c7-177">Aprire Visual Studio e selezionare **File** > **Nuovo** > **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-177">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="bc7c7-178">In hello **nuovo progetto** finestra di dialogo espandere **installato** > **modelli**, quindi selezionare **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-178">In hello **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="bc7c7-179">Selezionare nell'elenco dei modelli di hello **Storm esempio**.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-179">From hello list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="bc7c7-180">Nella parte inferiore di hello della finestra di dialogo hello, digitare un nome per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-180">At hello bottom of hello dialog box, type a name for hello application.</span></span>

    ![immagine](./media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. <span data-ttu-id="bc7c7-182">In **Esplora**, fare clic sul progetto hello e selezionare **inviare tooStorm in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-182">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bc7c7-183">Se richiesto, immettere le credenziali di accesso hello per la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-183">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="bc7c7-184">Se si dispone di più di una sottoscrizione, accedere toohello uno che contiene l'elevato numero di cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-184">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="bc7c7-185">Selezionare l'elevato numero di cluster HDInsight da hello **Cluster Storm** elenco a discesa e quindi selezionare **Invia**.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-185">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="bc7c7-186">È possibile controllare se l'invio di hello ha esito positivo tramite hello **Output** finestra.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-186">You can monitor whether hello submission is successful by using hello **Output** window.</span></span>

6. <span data-ttu-id="bc7c7-187">Quando la topologia hello è stata inviata correttamente, hello **Storm topologie** per cluster hello devono essere visualizzati.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-187">When hello topology has been successfully submitted, hello **Storm Topologies** for hello cluster should appear.</span></span> <span data-ttu-id="bc7c7-188">Selezionare la topologia hello hello elenco tooview informazioni hello in esecuzione sulla topologia.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-188">Select hello topology from hello list tooview information about hello running topology.</span></span>

    ![monitor Visual Studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > <span data-ttu-id="bc7c7-190">È possibile visualizzare **Storm Topologies** anche da **Esplora server**, espandendo **Azure** > **HDInsight** e quindi facendo clic su un cluster Storm in HDInsight e selezionando **View Storm Topologies**.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-190">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

    <span data-ttu-id="bc7c7-191">Selezionare la forma hello per hello spouts o bulloni tooview informazioni su questi componenti.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-191">Select hello shape for hello spouts or bolts tooview information about these components.</span></span> <span data-ttu-id="bc7c7-192">Viene aperta una nuova finestra per ogni elemento selezionato.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-192">A new window opens for each item selected.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bc7c7-193">nome Hello della topologia hello è il nome di classe hello della topologia hello (in questo caso, `HelloWord`,) con un timestamp aggiunto.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-193">hello name of hello topology is hello class name of hello topology (in this case, `HelloWord`,) with a timestamp appended.</span></span>

7. <span data-ttu-id="bc7c7-194">Da hello **topologia riepilogo** visualizzazione, selezionare **Kill** topologia hello toostop.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-194">From hello **Topology Summary** view, select **Kill** toostop hello topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bc7c7-195">Topologie di Storm continuano l'esecuzione fino a quando non vengono arrestati o hello cluster verrà eliminato.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-195">Storm topologies continue running until they are stopped or hello cluster is deleted.</span></span>


## <a name="rest-api"></a><span data-ttu-id="bc7c7-196">API REST</span><span class="sxs-lookup"><span data-stu-id="bc7c7-196">REST API</span></span>

<span data-ttu-id="bc7c7-197">Hello Storm UI si basa su hello l'API REST per effettuare la gestione e il monitoraggio delle funzionalità tramite l'API REST hello simili.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-197">hello Storm UI is built on top of hello REST API, so you can perform similar management and monitoring functionality by using hello REST API.</span></span> <span data-ttu-id="bc7c7-198">È possibile utilizzare strumenti personalizzati in toocreate hello API REST per la gestione e monitoraggio topologie Storm.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-198">You can use hello REST API toocreate custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="bc7c7-199">Per altre informazioni, vedere l'articolo relativo all'[API REST dell'interfaccia utente di Storm](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span><span class="sxs-lookup"><span data-stu-id="bc7c7-199">For more information, see [Storm UI REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span></span> <span data-ttu-id="bc7c7-200">Hello informazioni seguenti sono specifici toousing hello API REST con Apache Storm in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-200">hello following information is specific toousing hello REST API with Apache Storm on HDInsight.</span></span>

### <a name="base-uri"></a><span data-ttu-id="bc7c7-201">URI di base</span><span class="sxs-lookup"><span data-stu-id="bc7c7-201">Base URI</span></span>

<span data-ttu-id="bc7c7-202">URI di base per l'API REST di hello nei cluster HDInsight è Hello **https://&lt;clustername >.azurehdinsight.net/stormui/api/v1/**, dove **clustername** è il nome di hello dell'elevato numero di in Cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-202">hello base URI for hello REST API on HDInsight clusters is **https://&lt;clustername>.azurehdinsight.net/stormui/api/v1/**, where **clustername** is hello name of your Storm on HDInsight cluster.</span></span>

### <a name="authentication"></a><span data-ttu-id="bc7c7-203">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="bc7c7-203">Authentication</span></span>

<span data-ttu-id="bc7c7-204">Toohello richieste API REST è necessario utilizzare **l'autenticazione di base**, pertanto utilizzare nome amministratore del cluster HDInsight hello e una password.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-204">Requests toohello REST API must use **basic authentication**, so you use hello HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="bc7c7-205">Poiché l'autenticazione di base viene inviato con testo non crittografato, è necessario **sempre** utilizzare le comunicazioni HTTPS toosecure con cluster hello.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-205">Because basic authentication is sent by using clear text, you should **always** use HTTPS toosecure communications with hello cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="bc7c7-206">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="bc7c7-206">Return values</span></span>

<span data-ttu-id="bc7c7-207">Informazioni restituite da hello API REST possono solo essere usata da all'interno di cluster hello o hello di macchine virtuali nella stessa rete virtuale di Azure come cluster hello.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-207">Information that is returned from hello REST API may only be usable from within hello cluster or virtual machines on hello same Azure Virtual Network as hello cluster.</span></span> <span data-ttu-id="bc7c7-208">Nome di dominio completo hello (FQDN) restituito per i server Zookeeper sono ad esempio, non essere accessibile da Internet hello.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-208">For example, hello fully qualified domain name (FQDN) returned for Zookeeper servers are not be accessible from hello Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc7c7-209">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bc7c7-209">Next Steps</span></span>

<span data-ttu-id="bc7c7-210">Ora che si è appreso come topologie toodeploy e monitoraggio tramite hello Storm Dashboard, informazioni su come:</span><span class="sxs-lookup"><span data-stu-id="bc7c7-210">Now that you've learned how toodeploy and monitor topologies by using hello Storm Dashboard, learn how to:</span></span>

* [<span data-ttu-id="bc7c7-211">Sviluppare c# topologie in hello HDInsight Tools per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bc7c7-211">Develop C# topologies using hello HDInsight Tools for Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [<span data-ttu-id="bc7c7-212">Sviluppare topologie basate su Java per Apache Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="bc7c7-212">Develop Java-based topologies using Maven</span></span>](hdinsight-storm-develop-java-topology.md)

<span data-ttu-id="bc7c7-213">Per un elenco di altre topologie di esempio, vedere [Esempi di topologie Storm per Apache Storm in HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="bc7c7-213">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

[hdinsight-dashboard]: ./media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png
