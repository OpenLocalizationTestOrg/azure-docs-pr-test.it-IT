---
title: Esempi di Storm Starter in Apache Storm in HDInsight - Azure | Microsoft Docs
description: Informazioni su come eseguire l'analisi di Big Data ed elaborare i dati in tempo reale usando Apache Storm e gli esempi di Storm Starter in HDInsight.
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
ms.openlocfilehash: 83fc6db1ddb43eb87e7c58684505d7196c1e53d0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
#<a name="get-started-with-apache-storm-on-hdinsight-using-the-storm-starter-examples"></a><span data-ttu-id="a9a98-104">Introduzione ad Apache Storm in HDInsight tramite esempi di Storm Starter</span><span class="sxs-lookup"><span data-stu-id="a9a98-104">Get started with Apache Storm on HDInsight using the storm-starter examples</span></span>

<span data-ttu-id="a9a98-105">Questo articolo illustra come usare Apache Storm in HDInsight tramite esempi di Storm Starter.</span><span class="sxs-lookup"><span data-stu-id="a9a98-105">Learn how to use Apache Storm in HDInsight using the storm-starter examples.</span></span>

<span data-ttu-id="a9a98-106">Apache Storm è un sistema di calcolo in tempo reale scalabile, a tolleranza di errore e distribuito per l'elaborazione di flussi di dati.</span><span class="sxs-lookup"><span data-stu-id="a9a98-106">Apache Storm is a scalable, fault-tolerant, distributed, real-time computation system for processing streams of data.</span></span> <span data-ttu-id="a9a98-107">Con Storm in Azure HDInsight è possibile creare un cluster Storm basato sul cloud che esegue analisi di Big Data in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="a9a98-107">With Storm on Azure HDInsight, you can create a cloud-based Storm cluster that performs big data analytics in real time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a9a98-108">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="a9a98-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a9a98-109">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="a9a98-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9a98-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a9a98-110">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="a9a98-111">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="a9a98-111">**An Azure subscription**.</span></span> <span data-ttu-id="a9a98-112">Vedere [Ottenere una versione di prova gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="a9a98-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="a9a98-113">**Familiarità con SSH e SCP**.</span><span class="sxs-lookup"><span data-stu-id="a9a98-113">**Familiarity with SSH and SCP**.</span></span> <span data-ttu-id="a9a98-114">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="a9a98-114">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-a-storm-cluster"></a><span data-ttu-id="a9a98-115">Creare un cluster di Storm</span><span class="sxs-lookup"><span data-stu-id="a9a98-115">Create a Storm cluster</span></span>

<span data-ttu-id="a9a98-116">Per creare uno Storm nel cluster HDInsight, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a9a98-116">Use the following steps to create a Storm on HDInsight cluster:</span></span>

1. <span data-ttu-id="a9a98-117">Nel [portale di Azure](https://portal.azure.com) fare clic su **+ Nuovo**, **Intelligence e analisi** e quindi selezionare **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="a9a98-117">From the [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>

    ![Creazione di un cluster HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. <span data-ttu-id="a9a98-119">Nel pannello **Informazioni di base** immettere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a9a98-119">From the **Basics** blade, enter the following information:</span></span>

    * <span data-ttu-id="a9a98-120">**Nome del cluster**: nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a9a98-120">**Cluster Name**: The name of the HDInsight cluster.</span></span>
    * <span data-ttu-id="a9a98-121">**Sottoscrizione**: selezionare la sottoscrizione da usare.</span><span class="sxs-lookup"><span data-stu-id="a9a98-121">**Subscription**: Select the subscription to use.</span></span>
    * <span data-ttu-id="a9a98-122">**Nome utente dell'account di accesso del cluster** e **Password dell'account di accesso del cluster**: account di accesso usato per il cluster su HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a9a98-122">**Cluster login username** and **Cluster login password**: The login when accessing the cluster over HTTPS.</span></span> <span data-ttu-id="a9a98-123">Queste credenziali vengono usate per accedere a servizi quali l'interfaccia utente Web di Ambari o l'API REST.</span><span class="sxs-lookup"><span data-stu-id="a9a98-123">You use these credentials to access services such as the Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="a9a98-124">**Secure Shell (SSH) username** (Nome utente SSH): account di accesso usato per il cluster su SSH.</span><span class="sxs-lookup"><span data-stu-id="a9a98-124">**Secure Shell (SSH) username**: The login used when accessing the cluster over SSH.</span></span> <span data-ttu-id="a9a98-125">Per impostazione predefinita, la password corrisponde alla password di accesso al cluster.</span><span class="sxs-lookup"><span data-stu-id="a9a98-125">By default the password is the same as the cluster login password.</span></span>
    * <span data-ttu-id="a9a98-126">**Gruppo di risorse**: il gruppo di risorse nel quale viene creato il cluster.</span><span class="sxs-lookup"><span data-stu-id="a9a98-126">**Resource Group**: The resource group to create the cluster in.</span></span>
    * <span data-ttu-id="a9a98-127">**Posizione**: area di Azure in cui creare il cluster.</span><span class="sxs-lookup"><span data-stu-id="a9a98-127">**Location**: The Azure region to create the cluster in.</span></span>

    ![Selezionare la sottoscrizione](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. <span data-ttu-id="a9a98-129">Selezionare **Tipo di cluster**, quindi impostare i valori seguenti nel pannello **Configurazione cluster**:</span><span class="sxs-lookup"><span data-stu-id="a9a98-129">Select **Cluster type**, and then set the following values on the **Cluster configuration** blade:</span></span>

    * <span data-ttu-id="a9a98-130">**Tipo di cluster**: Storm</span><span class="sxs-lookup"><span data-stu-id="a9a98-130">**Cluster Type**: Storm</span></span>

    * <span data-ttu-id="a9a98-131">**Sistema operativo**: Linux</span><span class="sxs-lookup"><span data-stu-id="a9a98-131">**Operating system**: Linux</span></span>

    * <span data-ttu-id="a9a98-132">**Versione**: Storm 1.1.0 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="a9a98-132">**Version**: Storm 1.1.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="a9a98-133">**Livello cluster**: Standard</span><span class="sxs-lookup"><span data-stu-id="a9a98-133">**Cluster Tier**: Standard</span></span>

    <span data-ttu-id="a9a98-134">Usare infine il pulsante **Seleziona** per salvare le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="a9a98-134">Finally, use the **Select** button to save settings.</span></span>

    ![Selezionare il tipo di cluster](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="a9a98-136">Dopo avere selezionato il tipo di cluster, usare il pulsante __Seleziona__ per impostare il tipo di cluster.</span><span class="sxs-lookup"><span data-stu-id="a9a98-136">After selecting the cluster type, use the __Select__ button to set the cluster type.</span></span> <span data-ttu-id="a9a98-137">Usare quindi il pulsante __Avanti__ per completare la configurazione di base.</span><span class="sxs-lookup"><span data-stu-id="a9a98-137">Next, use the __Next__ button to finish basic configuration.</span></span>

5. <span data-ttu-id="a9a98-138">Nel pannello **Archiviazione** selezionare o creare un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="a9a98-138">From the **Storage** blade, select or create a Storage account.</span></span> <span data-ttu-id="a9a98-139">Per la procedura illustrata in questo documento, non modificare i valori predefiniti degli altri campi nel pannello.</span><span class="sxs-lookup"><span data-stu-id="a9a98-139">For the steps in this document, leave the other fields on this blade at the default values.</span></span> <span data-ttu-id="a9a98-140">Usare il pulsante __Avanti__ per salvare la configurazione della risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="a9a98-140">Use the __Next__ button to save storage configuration.</span></span>

    ![Configurare le impostazioni dell'account di archiviazione per HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. <span data-ttu-id="a9a98-142">Nel pannello **Riepilogo** esaminare la configurazione per il cluster.</span><span class="sxs-lookup"><span data-stu-id="a9a98-142">From the **Summary** blade, review the configuration for the cluster.</span></span> <span data-ttu-id="a9a98-143">Usare i collegamenti __Modifica__ per cambiare eventuali impostazioni non corrette.</span><span class="sxs-lookup"><span data-stu-id="a9a98-143">Use the __Edit__ links to change any settings that are incorrect.</span></span> <span data-ttu-id="a9a98-144">Usare infine il pulsante __Crea__ per creare il cluster.</span><span class="sxs-lookup"><span data-stu-id="a9a98-144">Finally, use the__Create__ button to create the cluster.</span></span>

    ![Riepilogo della configurazione del cluster](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > <span data-ttu-id="a9a98-146">La creazione del cluster può richiedere fino a 20 minuti.</span><span class="sxs-lookup"><span data-stu-id="a9a98-146">It can take up to 20 minutes to create the cluster.</span></span>

## <a name="run-a-storm-starter-sample-on-hdinsight"></a><span data-ttu-id="a9a98-147">Eseguire un esempio di Storm Starter in HDInsight</span><span class="sxs-lookup"><span data-stu-id="a9a98-147">Run a storm-starter sample on HDInsight</span></span>

1. <span data-ttu-id="a9a98-148">Connettersi al cluster HDInsight usando SSH:</span><span class="sxs-lookup"><span data-stu-id="a9a98-148">Connect to the HDInsight cluster using SSH:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="a9a98-149">Se è stata usata una password per proteggere l'account utente SSH, viene richiesto di specificarla.</span><span class="sxs-lookup"><span data-stu-id="a9a98-149">If you used a password to secure your SSH user account, you are prompted to enter it.</span></span> <span data-ttu-id="a9a98-150">Se è stata usata una chiave pubblica, può essere necessario usare il parametro `-i` per specificare la chiave privata corrispondente.</span><span class="sxs-lookup"><span data-stu-id="a9a98-150">If you used a public key, you may need use the `-i` parameter to specify the matching private key.</span></span> <span data-ttu-id="a9a98-151">Ad esempio: `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="a9a98-151">For example, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

    <span data-ttu-id="a9a98-152">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="a9a98-152">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="a9a98-153">Usare il comando seguente per avviare una topologia di esempio:</span><span class="sxs-lookup"><span data-stu-id="a9a98-153">Use the following command to start an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    > [!NOTE]
    > <span data-ttu-id="a9a98-154">Nelle versioni precedenti di HDInsight, il nome della classe della topologia è `storm.starter.WordCountTopology` anziché `org.apache.storm.starter.WordCountTopology`.</span><span class="sxs-lookup"><span data-stu-id="a9a98-154">On previous versions of HDInsight, the class name of the topology is `storm.starter.WordCountTopology` instead of `org.apache.storm.starter.WordCountTopology`.</span></span>

    <span data-ttu-id="a9a98-155">Il comando avvierà la topologia di esempio WordCount nel cluster usando "wordcount" come nome descrittivo.</span><span class="sxs-lookup"><span data-stu-id="a9a98-155">This command starts the example WordCount topology on the cluster, with a friendly name of 'wordcount'.</span></span> <span data-ttu-id="a9a98-156">Verranno generate in modo casuale le frasi e verranno conteggiate le occorrenze di ogni parola nelle frasi.</span><span class="sxs-lookup"><span data-stu-id="a9a98-156">It randomly generates sentences and count the occurrence of each word in the sentences.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a9a98-157">Durante l'invio di una topologia al cluster, è prima di tutto necessario copiare il file con estensione jar contenente il cluster prima di usare il comando `storm`.</span><span class="sxs-lookup"><span data-stu-id="a9a98-157">When submitting your own topologies to the cluster, you must first copy the jar file containing the cluster before using the `storm` command.</span></span> <span data-ttu-id="a9a98-158">Usare il comando `scp` per copiare il file.</span><span class="sxs-lookup"><span data-stu-id="a9a98-158">Use the `scp` command to copy the file.</span></span> <span data-ttu-id="a9a98-159">Ad esempio: `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="a9a98-159">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
    >
    > <span data-ttu-id="a9a98-160">L'esempio WordCount e altri esempi di Storm Starter sono già inclusi nel cluster in `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="a9a98-160">The WordCount example, and other storm-starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

<span data-ttu-id="a9a98-161">Se si è interessati a visualizzare il codice sorgente per gli esempi di storm-starter, è disponibile all'indirizzo [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span><span class="sxs-lookup"><span data-stu-id="a9a98-161">If you are interested in viewing the source for the storm-starter examples, you can find the code at [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span></span> <span data-ttu-id="a9a98-162">Questo collegamento riguarda Storm 1.1, che viene offerto con HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="a9a98-162">This link is for Storm 1.1.x, which is provided with HDInsight 3.6.</span></span> <span data-ttu-id="a9a98-163">Per altre versioni di Storm, usare il pulsante __Branch__ nella parte superiore della pagina per selezionare una versione diversa di Storm.</span><span class="sxs-lookup"><span data-stu-id="a9a98-163">For other versions of Storm, use the __Branch__ button at the top of the page to select a different Storm version.</span></span>

## <a name="monitor-the-topology"></a><span data-ttu-id="a9a98-164">Monitorare la topologia</span><span class="sxs-lookup"><span data-stu-id="a9a98-164">Monitor the topology</span></span>

<span data-ttu-id="a9a98-165">L'interfaccia utente di Storm è inclusa nel cluster HDInsight e fornisce un'interfaccia Web da usare con le topologie in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a9a98-165">The Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span>

<span data-ttu-id="a9a98-166">Usare la procedura seguente per monitorare la topologia con l'interfaccia utente Storm:</span><span class="sxs-lookup"><span data-stu-id="a9a98-166">Use the following steps to monitor the topology using the Storm UI:</span></span>

1. <span data-ttu-id="a9a98-167">Per visualizzare l'interfaccia utente di Storm, aprire un Web browser alla pagina https://CLUSTERNAME.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="a9a98-167">To display the Storm UI, open a web browser to https://CLUSTERNAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="a9a98-168">Sostituire **CLUSTERNAME** con il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="a9a98-168">Replace **CLUSTERNAME** with the name of your cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a9a98-169">Se viene richiesto di fornire un nome utente e una password, immettere l'amministratore del cluster e la password usati durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="a9a98-169">If asked to provide a user name and password, enter the cluster administrator (admin) and password that you used when creating the cluster.</span></span>

2. <span data-ttu-id="a9a98-170">Nella sezione **Topology summary** (Riepilogo topologie) selezionare la voce **wordcount** (conteggio parole) nella colonna **Nome**.</span><span class="sxs-lookup"><span data-stu-id="a9a98-170">Under **Topology summary**, select the **wordcount** entry in the **Name** column.</span></span> <span data-ttu-id="a9a98-171">Verranno visualizzate informazioni sulla topologia.</span><span class="sxs-lookup"><span data-stu-id="a9a98-171">Information about the topology is displayed.</span></span>

    ![Dashboard di Storm con informazioni sulla topologia di Storm Starter WordCount.](./media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

    <span data-ttu-id="a9a98-173">In questa pagina sono disponibili le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a9a98-173">This page provides the following information:</span></span>

    * <span data-ttu-id="a9a98-174">**Topology stats** : informazioni di base sulle prestazioni della topologia, organizzate in intervalli di tempo.</span><span class="sxs-lookup"><span data-stu-id="a9a98-174">**Topology stats** - Basic information on the topology performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="a9a98-175">La selezione di un intervallo di tempo specifico determina la modifica dell'intervallo di tempo relativo a informazioni visualizzate in altre sezioni della pagina.</span><span class="sxs-lookup"><span data-stu-id="a9a98-175">Selecting a specific time window changes the time window for information displayed in other sections of the page.</span></span>

    * <span data-ttu-id="a9a98-176">**Spouts** : informazioni di base sugli spout, incluso l'ultimo errore restituito da ciascuno di essi.</span><span class="sxs-lookup"><span data-stu-id="a9a98-176">**Spouts** - Basic information about spouts, including the last error returned by each spout.</span></span>

    * <span data-ttu-id="a9a98-177">**Bolts** : informazioni di base sui bolt.</span><span class="sxs-lookup"><span data-stu-id="a9a98-177">**Bolts** - Basic information about bolts.</span></span>

    * <span data-ttu-id="a9a98-178">**Topology configuration** : informazioni dettagliate sulla configurazione della topologia.</span><span class="sxs-lookup"><span data-stu-id="a9a98-178">**Topology configuration** - Detailed information about the topology configuration.</span></span>

    <span data-ttu-id="a9a98-179">Questa pagina fornisce anche azioni che possono essere eseguite sulla topologia:</span><span class="sxs-lookup"><span data-stu-id="a9a98-179">This page also provides actions that can be taken on the topology:</span></span>

    * <span data-ttu-id="a9a98-180">**Activate** : riprende l'elaborazione di una topologia disattivata.</span><span class="sxs-lookup"><span data-stu-id="a9a98-180">**Activate** - Resumes processing of a deactivated topology.</span></span>

    * <span data-ttu-id="a9a98-181">**Deactivate** : sospende una topologia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a9a98-181">**Deactivate** - Pauses a running topology.</span></span>

    * <span data-ttu-id="a9a98-182">**Rebalance** : regola il parallelismo della topologia.</span><span class="sxs-lookup"><span data-stu-id="a9a98-182">**Rebalance** - Adjusts the parallelism of the topology.</span></span> <span data-ttu-id="a9a98-183">È necessario ribilanciare le topologie in esecuzione dopo aver modificato il numero di nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="a9a98-183">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span></span> <span data-ttu-id="a9a98-184">Il ribilanciamento regola il parallelismo per compensare l'aumento o la diminuzione del numero di nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="a9a98-184">Rebalancing adjusts parallelism to compensate for the increased/decreased number of nodes in the cluster.</span></span> <span data-ttu-id="a9a98-185">Per altre informazioni, vedere l'articolo relativo al [parallelismo di una topologia Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="a9a98-185">For more information, see [Understanding the parallelism of a Storm topology](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

    * <span data-ttu-id="a9a98-186">**Kill** : arresta una topologia Storm dopo il timeout specificato.</span><span class="sxs-lookup"><span data-stu-id="a9a98-186">**Kill** - Terminates a Storm topology after the specified timeout.</span></span>

3. <span data-ttu-id="a9a98-187">In questa pagina selezionare una voce nella sezione **Spouts** o **Bolts**.</span><span class="sxs-lookup"><span data-stu-id="a9a98-187">From this page, select an entry from the **Spouts** or **Bolts** section.</span></span> <span data-ttu-id="a9a98-188">Verranno visualizzate informazioni relative al componente selezionato.</span><span class="sxs-lookup"><span data-stu-id="a9a98-188">Information about the selected component is displayed.</span></span>

    ![Storm Dashboard con informazioni sui componenti selezionati.](./media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

    <span data-ttu-id="a9a98-190">In questa pagina vengono visualizzate le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a9a98-190">This page displays the following information:</span></span>

    * <span data-ttu-id="a9a98-191">**Spout/Bolt stats** : informazioni di base sulle prestazioni, organizzate in intervalli di tempo.</span><span class="sxs-lookup"><span data-stu-id="a9a98-191">**Spout/Bolt stats** - Basic information on the component performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="a9a98-192">La selezione di un intervallo di tempo specifico determina la modifica dell'intervallo di tempo relativo a informazioni visualizzate in altre sezioni della pagina.</span><span class="sxs-lookup"><span data-stu-id="a9a98-192">Selecting a specific time window changes the time window for information displayed in other sections of the page.</span></span>

    * <span data-ttu-id="a9a98-193">**Input stats** (solo bolt): informazioni sui componenti che generano dati utilizzati dal bolt.</span><span class="sxs-lookup"><span data-stu-id="a9a98-193">**Input stats** (bolt only) - Information on components that produce data consumed by the bolt.</span></span>

    * <span data-ttu-id="a9a98-194">**Output stats** : informazioni sui dati generati dal bolt.</span><span class="sxs-lookup"><span data-stu-id="a9a98-194">**Output stats** - Information on data emitted by this bolt.</span></span>

    * <span data-ttu-id="a9a98-195">**Executors** : informazioni sulle istanze del componente.</span><span class="sxs-lookup"><span data-stu-id="a9a98-195">**Executors** - Information on instances of this component.</span></span>

    * <span data-ttu-id="a9a98-196">**Errors** : errori generati dal componente.</span><span class="sxs-lookup"><span data-stu-id="a9a98-196">**Errors** - Errors produced by this component.</span></span>

4. <span data-ttu-id="a9a98-197">Quando si visualizzano i dettagli di uno spout o di un bolt, selezionare una voce nella colonna **Porta** della sezione **Esecutori** per visualizzare i dettagli relativi a una specifica istanza del componente.</span><span class="sxs-lookup"><span data-stu-id="a9a98-197">When viewing the details of a spout or bolt, select an entry from the **Port** column in the **Executors** section to view details for a specific instance of the component.</span></span>

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    <span data-ttu-id="a9a98-198">In questo esempio, la parola **seven** è stata rilevata 1493957 volte.</span><span class="sxs-lookup"><span data-stu-id="a9a98-198">In this example, the word **seven** has occurred 1493957 times.</span></span> <span data-ttu-id="a9a98-199">In altri termini, il numero indica le occorrenze della parola dall'avvio della topologia.</span><span class="sxs-lookup"><span data-stu-id="a9a98-199">This count is how many times the word has been encountered since this topology was started.</span></span>

## <a name="stop-the-topology"></a><span data-ttu-id="a9a98-200">Arrestare la topologia</span><span class="sxs-lookup"><span data-stu-id="a9a98-200">Stop the topology</span></span>

<span data-ttu-id="a9a98-201">Tornare alla pagina **Riepilogo topologie** per la topologia relativa al conteggio delle parole e quindi fare clic sul pulsante **Kill** dalla sezione **Topology actions** (Azioni di topologia).</span><span class="sxs-lookup"><span data-stu-id="a9a98-201">Return to the **Topology summary** page for the word-count topology, and then select the **Kill** button from the **Topology actions** section.</span></span> <span data-ttu-id="a9a98-202">Quando richiesto, immettere 10 per il numero di secondi di attesa prima dell'arresto della topologia.</span><span class="sxs-lookup"><span data-stu-id="a9a98-202">When prompted, enter 10 for the seconds to wait before stopping the topology.</span></span> <span data-ttu-id="a9a98-203">Dopo il periodo di timeout, la topologia non viene più visualizzata nella sezione **Interfaccia utente di Storm** del dashboard.</span><span class="sxs-lookup"><span data-stu-id="a9a98-203">After the timeout period, the topology no longer appears when you visit the **Storm UI** section of the dashboard.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="a9a98-204">Eliminazione del cluster</span><span class="sxs-lookup"><span data-stu-id="a9a98-204">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="a9a98-205">Se si verifica un problema di creazione del cluster HDInsight, vedere i [requisiti dei controlli di accesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="a9a98-205">If you run into an issue with creating HDInsight cluster, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <span data-ttu-id="a9a98-206"><a id="next"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a9a98-206"><a id="next"></a>Next steps</span></span>

<span data-ttu-id="a9a98-207">In questa esercitazione di Apache Storm, sono state illustrate le nozioni di base dell'uso di Storm in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a9a98-207">In this Apache Storm tutorial, you learned the basics of working with Storm on HDInsight.</span></span> <span data-ttu-id="a9a98-208">Vedere quindi altre informazioni su come [sviluppare topologie basate su Java con Maven](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="a9a98-208">Next, learn how to [Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="a9a98-209">Se si ha già familiarità con lo sviluppo di topologie basate su Java e si vuole distribuire una topologia esistente in HDInsight, vedere [Distribuire e gestire topologie Apache Storm in HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a9a98-209">If you're already familiar with developing Java-based topologies and want to deploy an existing topology to HDInsight, see [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span></span>

<span data-ttu-id="a9a98-210">Uno sviluppatore .NET può creare le topologie C# o C#/Java ibride con Virtual Studio.</span><span class="sxs-lookup"><span data-stu-id="a9a98-210">If you are a .NET developer, you can create C# or hybrid C#/Java topologies using Visual Studio.</span></span> <span data-ttu-id="a9a98-211">Per altre informazioni, vedere [Sviluppare topologie C# per Apache Storm in HDInsight con gli strumenti Hadoop per Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="a9a98-211">For more information, see [Develop C# topologies for Apache Storm on HDInsight using Hadoop tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="a9a98-212">Di seguito sono riportati alcuni esempi delle topologie che si possono usare con Storm in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a9a98-212">For example topologies that can be used with Storm on HDInsight, see the following examples:</span></span>

* [<span data-ttu-id="a9a98-213">Topologie di esempio per Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="a9a98-213">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[preview-portal]: https://portal.azure.com/
