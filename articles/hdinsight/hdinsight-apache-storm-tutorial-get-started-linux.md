---
title: esempi di aaaStorm starter su Apache Storm in HDInsight - Azure | Documenti Microsoft
description: Informazioni su come toodo analitica di dati ed elaborare i dati in tempo reale usando Apache Storm hello esempi storm starter in HDInsight.
keywords: storm starter, esempio di apache storm
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: d710dcac-35d1-4c27-a8d6-acaf8146b485
ms.service: hdinsight
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: bb6d6549e67ca5b557f0692f98c89692a87267b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
#<a name="get-started-with-apache-storm-on-hdinsight-using-hello-storm-starter-examples"></a><span data-ttu-id="69d29-104">Introduzione a Apache Storm in HDInsight utilizzando hello storm starter esempi</span><span class="sxs-lookup"><span data-stu-id="69d29-104">Get started with Apache Storm on HDInsight using hello storm-starter examples</span></span>

<span data-ttu-id="69d29-105">Informazioni su come toouse Apache Storm HDInsight con hello esempi storm starter.</span><span class="sxs-lookup"><span data-stu-id="69d29-105">Learn how toouse Apache Storm in HDInsight using hello storm-starter examples.</span></span>

<span data-ttu-id="69d29-106">Apache Storm è un sistema di calcolo in tempo reale scalabile, a tolleranza di errore e distribuito per l'elaborazione di flussi di dati.</span><span class="sxs-lookup"><span data-stu-id="69d29-106">Apache Storm is a scalable, fault-tolerant, distributed, real-time computation system for processing streams of data.</span></span> <span data-ttu-id="69d29-107">Con Storm in Azure HDInsight è possibile creare un cluster Storm basato sul cloud che esegue analisi di Big Data in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="69d29-107">With Storm on Azure HDInsight, you can create a cloud-based Storm cluster that performs big data analytics in real time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="69d29-108">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="69d29-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="69d29-109">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="69d29-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="69d29-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="69d29-110">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="69d29-111">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="69d29-111">**An Azure subscription**.</span></span> <span data-ttu-id="69d29-112">Vedere [Ottenere una versione di prova gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="69d29-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="69d29-113">**Familiarità con SSH e SCP**.</span><span class="sxs-lookup"><span data-stu-id="69d29-113">**Familiarity with SSH and SCP**.</span></span> <span data-ttu-id="69d29-114">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="69d29-114">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-a-storm-cluster"></a><span data-ttu-id="69d29-115">Creare un cluster di Storm</span><span class="sxs-lookup"><span data-stu-id="69d29-115">Create a Storm cluster</span></span>

<span data-ttu-id="69d29-116">Utilizzare hello seguire toocreate passi un elevato numero di cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="69d29-116">Use hello following steps toocreate a Storm on HDInsight cluster:</span></span>

1. <span data-ttu-id="69d29-117">Da hello [portale di Azure](https://portal.azure.com)selezionare **+ nuovo**, **Intelligence + Analitica**, quindi selezionare **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="69d29-117">From hello [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>

    ![Creazione di un cluster HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. <span data-ttu-id="69d29-119">Da hello **nozioni di base** pannello immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="69d29-119">From hello **Basics** blade, enter hello following information:</span></span>

    * <span data-ttu-id="69d29-120">**Nome del cluster**: nome hello del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="69d29-120">**Cluster Name**: hello name of hello HDInsight cluster.</span></span>
    * <span data-ttu-id="69d29-121">**Sottoscrizione**: selezionare hello toouse di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="69d29-121">**Subscription**: Select hello subscription toouse.</span></span>
    * <span data-ttu-id="69d29-122">**Nome utente account di accesso del cluster** e **password dell'account di accesso Cluster**: accesso hello quando si accede a cluster hello tramite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="69d29-122">**Cluster login username** and **Cluster login password**: hello login when accessing hello cluster over HTTPS.</span></span> <span data-ttu-id="69d29-123">Usare questi servizi tooaccess credenziali, ad esempio hello dell'interfaccia utente Web Ambari o l'API REST.</span><span class="sxs-lookup"><span data-stu-id="69d29-123">You use these credentials tooaccess services such as hello Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="69d29-124">**Secure Shell (SSH) username**: hello account di accesso quando si accede a cluster hello su SSH.</span><span class="sxs-lookup"><span data-stu-id="69d29-124">**Secure Shell (SSH) username**: hello login used when accessing hello cluster over SSH.</span></span> <span data-ttu-id="69d29-125">Per impostazione predefinita la password di hello è hello come password di accesso cluster hello.</span><span class="sxs-lookup"><span data-stu-id="69d29-125">By default hello password is hello same as hello cluster login password.</span></span>
    * <span data-ttu-id="69d29-126">**Gruppo di risorse**: hello gruppo toocreate hello cluster della risorsa in.</span><span class="sxs-lookup"><span data-stu-id="69d29-126">**Resource Group**: hello resource group toocreate hello cluster in.</span></span>
    * <span data-ttu-id="69d29-127">**Percorso**: hello Azure area toocreate hello cluster.</span><span class="sxs-lookup"><span data-stu-id="69d29-127">**Location**: hello Azure region toocreate hello cluster in.</span></span>

    ![Selezionare la sottoscrizione](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. <span data-ttu-id="69d29-129">Selezionare **Cluster tipo**, e quindi set hello seguendo i valori hello **configurazione Cluster** pannello:</span><span class="sxs-lookup"><span data-stu-id="69d29-129">Select **Cluster type**, and then set hello following values on hello **Cluster configuration** blade:</span></span>

    * <span data-ttu-id="69d29-130">**Tipo di cluster**: Storm</span><span class="sxs-lookup"><span data-stu-id="69d29-130">**Cluster Type**: Storm</span></span>

    * <span data-ttu-id="69d29-131">**Sistema operativo**: Linux</span><span class="sxs-lookup"><span data-stu-id="69d29-131">**Operating system**: Linux</span></span>

    * <span data-ttu-id="69d29-132">**Versione**: Storm 1.1.0 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="69d29-132">**Version**: Storm 1.1.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="69d29-133">**Livello cluster**: Standard</span><span class="sxs-lookup"><span data-stu-id="69d29-133">**Cluster Tier**: Standard</span></span>

    <span data-ttu-id="69d29-134">Infine, utilizzare hello **selezionare** pulsante toosave impostazioni.</span><span class="sxs-lookup"><span data-stu-id="69d29-134">Finally, use hello **Select** button toosave settings.</span></span>

    ![Selezionare il tipo di cluster](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="69d29-136">Dopo aver selezionato il tipo di cluster hello, utilizzare hello __selezionare__ tooset hello cluster tipo di pulsante.</span><span class="sxs-lookup"><span data-stu-id="69d29-136">After selecting hello cluster type, use hello __Select__ button tooset hello cluster type.</span></span> <span data-ttu-id="69d29-137">Successivamente, utilizzare hello __Avanti__ configurazione di base toofinish pulsante.</span><span class="sxs-lookup"><span data-stu-id="69d29-137">Next, use hello __Next__ button toofinish basic configuration.</span></span>

5. <span data-ttu-id="69d29-138">Da hello **archiviazione** pannello selezionare o creare un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="69d29-138">From hello **Storage** blade, select or create a Storage account.</span></span> <span data-ttu-id="69d29-139">Per i passaggi hello in questo documento, lasciare hello altri campi in questo pannello valori predefiniti di hello.</span><span class="sxs-lookup"><span data-stu-id="69d29-139">For hello steps in this document, leave hello other fields on this blade at hello default values.</span></span> <span data-ttu-id="69d29-140">Hello utilizzare __Avanti__ configurazione dell'archiviazione toosave pulsante.</span><span class="sxs-lookup"><span data-stu-id="69d29-140">Use hello __Next__ button toosave storage configuration.</span></span>

    ![Configurare le impostazioni di account di archiviazione hello per HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. <span data-ttu-id="69d29-142">Da hello **riepilogo** pannello, verificare la configurazione per il cluster hello hello.</span><span class="sxs-lookup"><span data-stu-id="69d29-142">From hello **Summary** blade, review hello configuration for hello cluster.</span></span> <span data-ttu-id="69d29-143">Hello utilizzare __modifica__ collegamenti toochange eventuali impostazioni non sono corrette.</span><span class="sxs-lookup"><span data-stu-id="69d29-143">Use hello __Edit__ links toochange any settings that are incorrect.</span></span> <span data-ttu-id="69d29-144">Infine, utilizzare the__Create__ pulsante toocreate hello cluster.</span><span class="sxs-lookup"><span data-stu-id="69d29-144">Finally, use the__Create__ button toocreate hello cluster.</span></span>

    ![Riepilogo della configurazione del cluster](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > <span data-ttu-id="69d29-146">Può richiedere di cluster hello toocreate di too20 minuti.</span><span class="sxs-lookup"><span data-stu-id="69d29-146">It can take up too20 minutes toocreate hello cluster.</span></span>

## <a name="run-a-storm-starter-sample-on-hdinsight"></a><span data-ttu-id="69d29-147">Eseguire un esempio di Storm Starter in HDInsight</span><span class="sxs-lookup"><span data-stu-id="69d29-147">Run a storm-starter sample on HDInsight</span></span>

1. <span data-ttu-id="69d29-148">Connettere il cluster di HDInsight toohello tramite SSH:</span><span class="sxs-lookup"><span data-stu-id="69d29-148">Connect toohello HDInsight cluster using SSH:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="69d29-149">Se si utilizza un toosecure password account utente SSH, si è tooenter richiesto è.</span><span class="sxs-lookup"><span data-stu-id="69d29-149">If you used a password toosecure your SSH user account, you are prompted tooenter it.</span></span> <span data-ttu-id="69d29-150">Se si utilizza una chiave pubblica, è necessario utilizzare hello `-i` toospecify parametro hello chiave privata corrispondente.</span><span class="sxs-lookup"><span data-stu-id="69d29-150">If you used a public key, you may need use hello `-i` parameter toospecify hello matching private key.</span></span> <span data-ttu-id="69d29-151">ad esempio `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="69d29-151">For example, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

    <span data-ttu-id="69d29-152">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="69d29-152">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="69d29-153">Utilizzare hello comando toostart una topologia di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="69d29-153">Use hello following command toostart an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    > [!NOTE]
    > <span data-ttu-id="69d29-154">Nelle versioni precedenti di HDInsight, nome della classe hello della topologia hello è `storm.starter.WordCountTopology` anziché `org.apache.storm.starter.WordCountTopology`.</span><span class="sxs-lookup"><span data-stu-id="69d29-154">On previous versions of HDInsight, hello class name of hello topology is `storm.starter.WordCountTopology` instead of `org.apache.storm.starter.WordCountTopology`.</span></span>

    <span data-ttu-id="69d29-155">Questo comando avvia una topologia di hello esempio WordCount su cluster hello, con un nome descrittivo 'wordcount'.</span><span class="sxs-lookup"><span data-stu-id="69d29-155">This command starts hello example WordCount topology on hello cluster, with a friendly name of 'wordcount'.</span></span> <span data-ttu-id="69d29-156">In modo casuale genera frasi e occorrenza hello conteggio di ogni parola nella frase hello.</span><span class="sxs-lookup"><span data-stu-id="69d29-156">It randomly generates sentences and count hello occurrence of each word in hello sentences.</span></span>

    > [!NOTE]
    > <span data-ttu-id="69d29-157">Quando si inviano cluster toohello topologie, è prima necessario copiare i file jar hello contenente cluster hello prima di utilizzare hello `storm` comando.</span><span class="sxs-lookup"><span data-stu-id="69d29-157">When submitting your own topologies toohello cluster, you must first copy hello jar file containing hello cluster before using hello `storm` command.</span></span> <span data-ttu-id="69d29-158">Hello utilizzare `scp` file hello toocopy di comando.</span><span class="sxs-lookup"><span data-stu-id="69d29-158">Use hello `scp` command toocopy hello file.</span></span> <span data-ttu-id="69d29-159">Ad esempio, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="69d29-159">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
    >
    > <span data-ttu-id="69d29-160">Esempio WordCount Hello e altri esempi di storm starter, sono già inclusi nel cluster in `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="69d29-160">hello WordCount example, and other storm-starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

<span data-ttu-id="69d29-161">Se si è interessati in visualizzazione origine hello per esempi di hello storm starter, è possibile trovare codice hello [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span><span class="sxs-lookup"><span data-stu-id="69d29-161">If you are interested in viewing hello source for hello storm-starter examples, you can find hello code at [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span></span> <span data-ttu-id="69d29-162">Questo collegamento riguarda Storm 1.1, che viene offerto con HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="69d29-162">This link is for Storm 1.1.x, which is provided with HDInsight 3.6.</span></span> <span data-ttu-id="69d29-163">Per altre versioni di Storm, utilizzare hello __ramo__ pulsante nella parte superiore di hello di hello pagina tooselect una versione diversa di Storm.</span><span class="sxs-lookup"><span data-stu-id="69d29-163">For other versions of Storm, use hello __Branch__ button at hello top of hello page tooselect a different Storm version.</span></span>

## <a name="monitor-hello-topology"></a><span data-ttu-id="69d29-164">Monitoraggio hello topologia</span><span class="sxs-lookup"><span data-stu-id="69d29-164">Monitor hello topology</span></span>

<span data-ttu-id="69d29-165">Ciao Storm UI fornisce un'interfaccia web per l'utilizzo con l'esecuzione di topologie ed è incluso nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="69d29-165">hello Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span>

<span data-ttu-id="69d29-166">Utilizzare hello seguente topologia di hello toomonitor passaggi utilizzando hello UI Storm:</span><span class="sxs-lookup"><span data-stu-id="69d29-166">Use hello following steps toomonitor hello topology using hello Storm UI:</span></span>

1. <span data-ttu-id="69d29-167">hello toodisplay dell'interfaccia utente Storm, aprire un toohttps://CLUSTERNAME.azurehdinsight.net/stormui browser web.</span><span class="sxs-lookup"><span data-stu-id="69d29-167">toodisplay hello Storm UI, open a web browser toohttps://CLUSTERNAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="69d29-168">Sostituire **CLUSTERNAME** con nome hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="69d29-168">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="69d29-169">Se richiesto tooprovide un nome utente e una password, immettere Amministrazione cluster hello (amministratore) e la password utilizzati quando la creazione di cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="69d29-169">If asked tooprovide a user name and password, enter hello cluster administrator (admin) and password that you used when creating hello cluster.</span></span>

2. <span data-ttu-id="69d29-170">In **riepilogo topologia**selezionare hello **wordcount** voce hello **nome** colonna.</span><span class="sxs-lookup"><span data-stu-id="69d29-170">Under **Topology summary**, select hello **wordcount** entry in hello **Name** column.</span></span> <span data-ttu-id="69d29-171">Informazioni sulla topologia di hello.</span><span class="sxs-lookup"><span data-stu-id="69d29-171">Information about hello topology is displayed.</span></span>

    ![Dashboard di Storm con informazioni sulla topologia di Storm Starter WordCount.](./media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

    <span data-ttu-id="69d29-173">In questa pagina vengono hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="69d29-173">This page provides hello following information:</span></span>

    * <span data-ttu-id="69d29-174">**Statistiche di topologia** -informazioni di base sulle prestazioni di topologia hello, organizzati in intervalli di tempo.</span><span class="sxs-lookup"><span data-stu-id="69d29-174">**Topology stats** - Basic information on hello topology performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="69d29-175">Se si seleziona un intervallo di tempo specifico tempo finestra modifiche hello per le informazioni visualizzate in altre sezioni della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="69d29-175">Selecting a specific time window changes hello time window for information displayed in other sections of hello page.</span></span>

    * <span data-ttu-id="69d29-176">**Spouts** -spouts, inclusi l'ultimo errore hello restituiti da ogni beccuccio informazioni di base.</span><span class="sxs-lookup"><span data-stu-id="69d29-176">**Spouts** - Basic information about spouts, including hello last error returned by each spout.</span></span>

    * <span data-ttu-id="69d29-177">**Bolts** : informazioni di base sui bolt.</span><span class="sxs-lookup"><span data-stu-id="69d29-177">**Bolts** - Basic information about bolts.</span></span>

    * <span data-ttu-id="69d29-178">**Configurazione della topologia** -informazioni dettagliate su configurazione della topologia hello.</span><span class="sxs-lookup"><span data-stu-id="69d29-178">**Topology configuration** - Detailed information about hello topology configuration.</span></span>

    <span data-ttu-id="69d29-179">Questa pagina fornisce inoltre le azioni che possono essere eseguite sulla topologia di hello:</span><span class="sxs-lookup"><span data-stu-id="69d29-179">This page also provides actions that can be taken on hello topology:</span></span>

    * <span data-ttu-id="69d29-180">**Activate** : riprende l'elaborazione di una topologia disattivata.</span><span class="sxs-lookup"><span data-stu-id="69d29-180">**Activate** - Resumes processing of a deactivated topology.</span></span>

    * <span data-ttu-id="69d29-181">**Deactivate** : sospende una topologia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="69d29-181">**Deactivate** - Pauses a running topology.</span></span>

    * <span data-ttu-id="69d29-182">**Ribilanciare** -consente di regolare il parallelismo hello della topologia hello.</span><span class="sxs-lookup"><span data-stu-id="69d29-182">**Rebalance** - Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="69d29-183">È necessario ribilanciare topologie in esecuzione dopo avere modificato il numero di hello di nodi nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="69d29-183">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="69d29-184">Ribilanciamento regola toocompensate di parallelismo per il numero di hello aumentato o diminuito di nodi nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="69d29-184">Rebalancing adjusts parallelism toocompensate for hello increased/decreased number of nodes in hello cluster.</span></span> <span data-ttu-id="69d29-185">Per ulteriori informazioni, vedere [comprensione parallelismo hello di una topologia di Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="69d29-185">For more information, see [Understanding hello parallelism of a Storm topology](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

    * <span data-ttu-id="69d29-186">**Kill** -termina una topologia di Storm dopo hello specificato timeout.</span><span class="sxs-lookup"><span data-stu-id="69d29-186">**Kill** - Terminates a Storm topology after hello specified timeout.</span></span>

3. <span data-ttu-id="69d29-187">In questa pagina, selezionare una voce da hello **Spouts** o **bulloni** sezione.</span><span class="sxs-lookup"><span data-stu-id="69d29-187">From this page, select an entry from hello **Spouts** or **Bolts** section.</span></span> <span data-ttu-id="69d29-188">Informazioni sul componente selezionato hello viene visualizzate.</span><span class="sxs-lookup"><span data-stu-id="69d29-188">Information about hello selected component is displayed.</span></span>

    ![Storm Dashboard con informazioni sui componenti selezionati.](./media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

    <span data-ttu-id="69d29-190">Questa pagina consente di visualizzare hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="69d29-190">This page displays hello following information:</span></span>

    * <span data-ttu-id="69d29-191">**Statistiche beccuccio/fulmine** -informazioni di base sulle prestazioni del componente hello, organizzati in intervalli di tempo.</span><span class="sxs-lookup"><span data-stu-id="69d29-191">**Spout/Bolt stats** - Basic information on hello component performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="69d29-192">Se si seleziona un intervallo di tempo specifico tempo finestra modifiche hello per le informazioni visualizzate in altre sezioni della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="69d29-192">Selecting a specific time window changes hello time window for information displayed in other sections of hello page.</span></span>

    * <span data-ttu-id="69d29-193">**Statistiche di input** (bullone solo) - informazioni sui componenti che producono dati utilizzati dalle fulmine hello.</span><span class="sxs-lookup"><span data-stu-id="69d29-193">**Input stats** (bolt only) - Information on components that produce data consumed by hello bolt.</span></span>

    * <span data-ttu-id="69d29-194">**Output stats** : informazioni sui dati generati dal bolt.</span><span class="sxs-lookup"><span data-stu-id="69d29-194">**Output stats** - Information on data emitted by this bolt.</span></span>

    * <span data-ttu-id="69d29-195">**Executors** : informazioni sulle istanze del componente.</span><span class="sxs-lookup"><span data-stu-id="69d29-195">**Executors** - Information on instances of this component.</span></span>

    * <span data-ttu-id="69d29-196">**Errors** : errori generati dal componente.</span><span class="sxs-lookup"><span data-stu-id="69d29-196">**Errors** - Errors produced by this component.</span></span>

4. <span data-ttu-id="69d29-197">Quando si visualizzano i dettagli di hello di un fulmine beccuccio, selezionare una voce da hello **porta** colonna hello **executor** sezione tooview dettagli per un'istanza specifica del componente hello.</span><span class="sxs-lookup"><span data-stu-id="69d29-197">When viewing hello details of a spout or bolt, select an entry from hello **Port** column in hello **Executors** section tooview details for a specific instance of hello component.</span></span>

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    <span data-ttu-id="69d29-198">In questo esempio hello word **sette** si è verificato 1493957 volte.</span><span class="sxs-lookup"><span data-stu-id="69d29-198">In this example, hello word **seven** has occurred 1493957 times.</span></span> <span data-ttu-id="69d29-199">Questo conteggio è quante volte si è verificato parola hello poiché questa topologia è stata avviata.</span><span class="sxs-lookup"><span data-stu-id="69d29-199">This count is how many times hello word has been encountered since this topology was started.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="69d29-200">Arrestare la topologia hello</span><span class="sxs-lookup"><span data-stu-id="69d29-200">Stop hello topology</span></span>

<span data-ttu-id="69d29-201">Restituire toohello **riepilogo topologia** pagina topologia di conteggio parole hello e quindi selezionare hello **Kill** pulsante hello **azioni topologia** sezione.</span><span class="sxs-lookup"><span data-stu-id="69d29-201">Return toohello **Topology summary** page for hello word-count topology, and then select hello **Kill** button from hello **Topology actions** section.</span></span> <span data-ttu-id="69d29-202">Quando richiesto, immettere 10 per hello toowait di secondi prima di arrestare topologia hello.</span><span class="sxs-lookup"><span data-stu-id="69d29-202">When prompted, enter 10 for hello seconds toowait before stopping hello topology.</span></span> <span data-ttu-id="69d29-203">Dopo il periodo di timeout hello topologia hello non viene più visualizzata quando si visita hello **dell'interfaccia utente Storm** sezione dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="69d29-203">After hello timeout period, hello topology no longer appears when you visit hello **Storm UI** section of hello dashboard.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="69d29-204">Eliminare il cluster hello</span><span class="sxs-lookup"><span data-stu-id="69d29-204">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="69d29-205">Se si verifica un problema di creazione del cluster HDInsight, vedere i [requisiti dei controlli di accesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="69d29-205">If you run into an issue with creating HDInsight cluster, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <span data-ttu-id="69d29-206"><a id="next"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="69d29-206"><a id="next"></a>Next steps</span></span>

<span data-ttu-id="69d29-207">In questa esercitazione Apache Storm state hello nozioni fondamentali sulle operazioni con Storm in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="69d29-207">In this Apache Storm tutorial, you learned hello basics of working with Storm on HDInsight.</span></span> <span data-ttu-id="69d29-208">Per ulteriori informazioni come troppo[topologie basate sul linguaggio di sviluppo utilizzando Maven](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="69d29-208">Next, learn how too[Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="69d29-209">Se si ha già familiarità con lo sviluppo basato su Java topologie e si desidera toodeploy un tooHDInsight topologia esistente, vedere [distribuire e gestire le topologie di Apache Storm in HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span><span class="sxs-lookup"><span data-stu-id="69d29-209">If you're already familiar with developing Java-based topologies and want toodeploy an existing topology tooHDInsight, see [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span></span>

<span data-ttu-id="69d29-210">Uno sviluppatore .NET può creare le topologie C# o C#/Java ibride con Virtual Studio.</span><span class="sxs-lookup"><span data-stu-id="69d29-210">If you are a .NET developer, you can create C# or hybrid C#/Java topologies using Visual Studio.</span></span> <span data-ttu-id="69d29-211">Per altre informazioni, vedere [Sviluppare topologie C# per Apache Storm in HDInsight con gli strumenti Hadoop per Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="69d29-211">For more information, see [Develop C# topologies for Apache Storm on HDInsight using Hadoop tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="69d29-212">Per le topologie di esempio che possono essere utilizzate con Storm in HDInsight, vedere hello seguono esempi:</span><span class="sxs-lookup"><span data-stu-id="69d29-212">For example topologies that can be used with Storm on HDInsight, see hello following examples:</span></span>

* [<span data-ttu-id="69d29-213">Topologie di esempio per Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="69d29-213">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[preview-portal]: https://portal.azure.com/
