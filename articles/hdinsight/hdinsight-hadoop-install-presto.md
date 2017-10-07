---
title: cluster di accedere in Linux di Azure HDInsight aaaInstall | Documenti Microsoft
description: Informazioni su come accedere tooinstall Airpal in basati su Linux HDInsight Hadoop cluster e tramite le azioni Script.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: nitinme
ms.openlocfilehash: 5d54d0efc3e5fdc6f5a8d3a94ad2f61d16df24c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-presto-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="587e2-103">Installare e usare Presto nei cluster HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="587e2-103">Install and use Presto on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="587e2-104">In questo argomento, viene illustrato come accedere in HDInsight Hadoop tooinstall cluster utilizzando l'azione di Script.</span><span class="sxs-lookup"><span data-stu-id="587e2-104">In this topic, you learn how tooinstall Presto on HDInsight Hadoop clusters by using Script Action.</span></span> <span data-ttu-id="587e2-105">Verrà inoltre descritto come tooinstall Airpal su un cluster HDInsight Presto esistente.</span><span class="sxs-lookup"><span data-stu-id="587e2-105">You also learn how tooinstall Airpal on an existing Presto HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="587e2-106">Hello passaggi in questo documento richiedono un **cluster HDInsight Hadoop 3.5** che utilizza Linux.</span><span class="sxs-lookup"><span data-stu-id="587e2-106">hello steps in this document require an **HDInsight 3.5 Hadoop cluster** that uses Linux.</span></span> <span data-ttu-id="587e2-107">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="587e2-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="587e2-108">Per altre informazioni, vedere [Versioni di HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="587e2-108">For more information, see [HDInsight versions](hdinsight-component-versioning.md).</span></span>

## <a name="what-is-presto"></a><span data-ttu-id="587e2-109">Che cos'è Presto?</span><span class="sxs-lookup"><span data-stu-id="587e2-109">What is Presto?</span></span>
<span data-ttu-id="587e2-110">[Presto](https://prestodb.io/overview.html) è un motore di query SQL distribuito veloce per Big Data.</span><span class="sxs-lookup"><span data-stu-id="587e2-110">[Presto](https://prestodb.io/overview.html) is a fast distributed SQL query engine for big data.</span></span> <span data-ttu-id="587e2-111">Presto è adatto per l'esecuzione di query interattive di petabyte di dati.</span><span class="sxs-lookup"><span data-stu-id="587e2-111">Presto is suitable for interactive querying of petabytes of data.</span></span> <span data-ttu-id="587e2-112">Per ulteriori informazioni sui componenti hello di accedere e come interagiscono tra loro, vedere [concetti Presto](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span><span class="sxs-lookup"><span data-stu-id="587e2-112">For more information on hello components of Presto and how they work together, see [Presto concepts](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span></span>

> [!WARNING]
> <span data-ttu-id="587e2-113">I componenti forniti con i cluster di HDInsight hello sono completamente supportati e il supporto Microsoft verrà Guida tooisolate e risolvere i problemi correlati toothese componenti.</span><span class="sxs-lookup"><span data-stu-id="587e2-113">Components provided with hello HDInsight cluster are fully supported and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>
> 
> <span data-ttu-id="587e2-114">I componenti personalizzati, ad esempio Presto, ricevano supporto commercialmente ragionevole toohelp toofurther per risolvere il problema di hello.</span><span class="sxs-lookup"><span data-stu-id="587e2-114">Custom components, such as Presto, receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="587e2-115">Ciò potrebbe comportare la risoluzione problema hello o chiedere che tooengage i canali disponibili per hello apertura di tecnologie di origine in cui si trova esperienza completa per tale tecnologia.</span><span class="sxs-lookup"><span data-stu-id="587e2-115">This might result in resolving hello issue OR asking you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="587e2-116">È ad esempio possibile ricorrere a molti siti di community, come il [forum MSDN per HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight) o [http://stackoverflow.com](http://stackoverflow.com). Anche per i progetti Apache sono disponibili siti specifici in [http://apache.org](http://apache.org), ad esempio [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="587e2-116">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>
> 
> 


## <a name="install-presto-using-script-action"></a><span data-ttu-id="587e2-117">Installare Presto mediante l'azione di script</span><span class="sxs-lookup"><span data-stu-id="587e2-117">Install Presto using script action</span></span>

<span data-ttu-id="587e2-118">In questa sezione vengono fornite istruzioni su come script di esempio hello toouse quando si crea un nuovo cluster mediante hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="587e2-118">This section provides instructions on how toouse hello sample script when creating a new cluster by using hello Azure portal.</span></span> 

1. <span data-ttu-id="587e2-119">Avviare il provisioning di un cluster attenendosi alla procedura hello in [cluster HDInsight basati su Linux provisioning](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="587e2-119">Start provisioning a cluster by using hello steps in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span> <span data-ttu-id="587e2-120">Assicurarsi di creare cluster di hello utilizzando hello **personalizzato** flusso di creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="587e2-120">Make sure you create hello cluster using hello **Custom** cluster creation flow.</span></span> <span data-ttu-id="587e2-121">È necessario assicurarsi di tale cluster hello che crei soddisfi hello seguenti requisiti.</span><span class="sxs-lookup"><span data-stu-id="587e2-121">You must ensure that hello cluster you create meets hello following requirements.</span></span>

    <span data-ttu-id="587e2-122">a.</span><span class="sxs-lookup"><span data-stu-id="587e2-122">a.</span></span> <span data-ttu-id="587e2-123">Deve essere un cluster Hadoop con HDInsight versione 3.5.</span><span class="sxs-lookup"><span data-stu-id="587e2-123">It must be a Hadoop cluster with HDInsight version 3.5.</span></span>

    <span data-ttu-id="587e2-124">b.</span><span class="sxs-lookup"><span data-stu-id="587e2-124">b.</span></span> <span data-ttu-id="587e2-125">È necessario usare l'archiviazione di Azure come archivio dati hello.</span><span class="sxs-lookup"><span data-stu-id="587e2-125">It must use Azure Storage as hello data store.</span></span> <span data-ttu-id="587e2-126">Utilizzo Presto in un cluster che utilizza l'archivio Azure Data Lake come opzione di archiviazione hello non è ancora supportato.</span><span class="sxs-lookup"><span data-stu-id="587e2-126">Using Presto on a cluster that uses Azure Data Lake Store as hello storage option is not yet supported.</span></span> 

    ![Creazione del cluster HDInsight con opzioni personalizzate](./media/hdinsight-hadoop-install-presto/hdinsight-install-custom.png)

2. <span data-ttu-id="587e2-128">In hello **impostazioni avanzate** pannello seleziona **azioni Script**e fornire informazioni hello riportate di seguito:</span><span class="sxs-lookup"><span data-stu-id="587e2-128">On hello **Advanced settings** blade, select **Script Actions**, and provide hello information below:</span></span>
   
   * <span data-ttu-id="587e2-129">**NOME**: immettere un nome descrittivo per l'azione script hello.</span><span class="sxs-lookup"><span data-stu-id="587e2-129">**NAME**: Enter a friendly name for hello script action.</span></span>
   * <span data-ttu-id="587e2-130">**URI script Bash**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span><span class="sxs-lookup"><span data-stu-id="587e2-130">**Bash script URI**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span></span>
   * <span data-ttu-id="587e2-131">**HEAD**: selezionare questa opzione</span><span class="sxs-lookup"><span data-stu-id="587e2-131">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="587e2-132">**RUOLO DI LAVORO**: selezionare questa opzione</span><span class="sxs-lookup"><span data-stu-id="587e2-132">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="587e2-133">**ZOOKEEPER**: deselezionare questa casella di controllo</span><span class="sxs-lookup"><span data-stu-id="587e2-133">**ZOOKEEPER**: Clear this check box</span></span>
   * <span data-ttu-id="587e2-134">**PARAMETRI**: lasciare questo campo vuoto</span><span class="sxs-lookup"><span data-stu-id="587e2-134">**PARAMETERS**: Leave this field blank</span></span>


3. <span data-ttu-id="587e2-135">Nella parte inferiore di hello di hello **azioni Script** pannello, fare clic su hello **selezionare** configurazione hello toosave dei pulsanti.</span><span class="sxs-lookup"><span data-stu-id="587e2-135">At hello bottom of hello **Script Actions** blade, click hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="587e2-136">Infine, fare clic su hello **selezionare** pulsante nella parte inferiore di hello di hello **impostazioni avanzate** informazioni di configurazione di blade toosave hello.</span><span class="sxs-lookup"><span data-stu-id="587e2-136">Finally, click  hello **Select** button at hello bottom of hello **Advanced Settings** blade toosave hello configuration information.</span></span>

4. <span data-ttu-id="587e2-137">Continuano il provisioning del cluster di hello, come descritto in [cluster HDInsight basati su Linux provisioning](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="587e2-137">Continue provisioning hello cluster as described in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="587e2-138">Azure PowerShell, hello CLI di Azure, HDInsight .NET SDK hello o modelli di gestione risorse di Azure possono anche essere azioni script tooapply utilizzato.</span><span class="sxs-lookup"><span data-stu-id="587e2-138">Azure PowerShell, hello Azure CLI, hello HDInsight .NET SDK, or Azure Resource Manager templates can also be used tooapply script actions.</span></span> <span data-ttu-id="587e2-139">È inoltre possibile applicare tooalready azioni script i cluster in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="587e2-139">You can also apply script actions tooalready running clusters.</span></span> <span data-ttu-id="587e2-140">Per altre informazioni, vedere [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="587e2-140">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
    > 
    > 

## <a name="use-presto-with-hdinsight"></a><span data-ttu-id="587e2-141">Usare Presto con HDInsight</span><span class="sxs-lookup"><span data-stu-id="587e2-141">Use Presto with HDInsight</span></span>

<span data-ttu-id="587e2-142">Eseguire hello seguendo i passaggi toouse accedere in un cluster di HDInsight dopo l'installazione utilizzando i passaggi di hello descritti in precedenza.</span><span class="sxs-lookup"><span data-stu-id="587e2-142">Perform hello following steps toouse Presto in an HDInsight cluster after you have installed it using hello steps described above.</span></span>

1. <span data-ttu-id="587e2-143">Connettere il cluster di HDInsight toohello tramite SSH:</span><span class="sxs-lookup"><span data-stu-id="587e2-143">Connect toohello HDInsight cluster using SSH:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="587e2-144">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="587e2-144">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
     

2. <span data-ttu-id="587e2-145">Avviare shell di hello Presto utilizzando hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="587e2-145">Start hello Presto shell using hello following command.</span></span>
   
        presto --schema default

3. <span data-ttu-id="587e2-146">Eseguire una query sulla tabella di esempio, **hivesampletable**, che è disponibile in tutti i cluster HDInsight per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="587e2-146">Run a query on a sample table, **hivesampletable**, which is available on all HDInsight clusters by default.</span></span>
   
        select count (*) from hivesampletable;
   
    <span data-ttu-id="587e2-147">Per impostazione predefinita sono già configurati i connettori [Hive](https://prestodb.io/docs/current/connector/hive.html) e [TPCH](https://prestodb.io/docs/current/connector/tpch.html) per Presto.</span><span class="sxs-lookup"><span data-stu-id="587e2-147">By default, [Hive](https://prestodb.io/docs/current/connector/hive.html) and [TPCH](https://prestodb.io/docs/current/connector/tpch.html) connectors for Presto are already configured.</span></span> <span data-ttu-id="587e2-148">Hive connettore è configurato toouse hello predefinito installato Hive installazione, pertanto tutte le tabelle di hello dall'Hive saranno automaticamente visibili nell'accedere.</span><span class="sxs-lookup"><span data-stu-id="587e2-148">Hive connector is configured toouse hello default installed Hive installation, so all hello tables from Hive will be automatically visible in Presto.</span></span>

    <span data-ttu-id="587e2-149">Per informazioni dettagliate su come è possibile usate Presto, vedere la [documentazione su Presto](https://prestodb.io/docs/current/index.html).</span><span class="sxs-lookup"><span data-stu-id="587e2-149">For a detailed description on how you can use Presto, see [Presto documentation](https://prestodb.io/docs/current/index.html).</span></span>

## <a name="use-airpal-with-presto"></a><span data-ttu-id="587e2-150">Usare Airpal con Presto</span><span class="sxs-lookup"><span data-stu-id="587e2-150">Use Airpal with Presto</span></span>

<span data-ttu-id="587e2-151">[Airpal](https://github.com/airbnb/airpal#airpal) è un'interfaccia per query basate su Web open source per Presto.</span><span class="sxs-lookup"><span data-stu-id="587e2-151">[Airpal](https://github.com/airbnb/airpal#airpal) is an open-source web-based query interface for Presto.</span></span> <span data-ttu-id="587e2-152">Per altre informazioni su Airpal, vedere la [documentazione su Airpal](https://github.com/airbnb/airpal#airpal).</span><span class="sxs-lookup"><span data-stu-id="587e2-152">For more information on Airpal, see [Airpal documentation](https://github.com/airbnb/airpal#airpal).</span></span>

<span data-ttu-id="587e2-153">In questa sezione viene analizzato in passaggi hello troppo**installarvi Airpal hello edgenode** di un cluster HDInsight Hadoop, che sono già disponibili accedere installato.</span><span class="sxs-lookup"><span data-stu-id="587e2-153">In this section, we look at hello steps too**install Airpal on hello edgenode** of an HDInsight Hadoop cluster, that already has Presto installed.</span></span> <span data-ttu-id="587e2-154">In questo modo il che interfaccia di query che hello Airpal web è disponibile sulla hello Internet.</span><span class="sxs-lookup"><span data-stu-id="587e2-154">This ensures that hello Airpal web query interface is available over hello Internet.</span></span>

1. <span data-ttu-id="587e2-155">Tramite SSH, connettersi toohello nodo head del cluster HDInsight hello Presto installato:</span><span class="sxs-lookup"><span data-stu-id="587e2-155">Using SSH, connect toohello headnode of hello HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="587e2-156">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="587e2-156">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="587e2-157">Una volta connessi, eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="587e2-157">Once you are connected, run hello following command.</span></span>

        sudo slider registry  --name presto1 --getexp presto 
   
    <span data-ttu-id="587e2-158">Verrà visualizzato un output simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="587e2-158">You should see an output like hello following:</span></span>

        {
            "coordinator_address" : [ {
                "value" : "10.0.0.12:9090",
                "level" : "application",
                "updatedTime" : "Mon Apr 03 20:13:41 UTC 2017"
        } ]

3. <span data-ttu-id="587e2-159">Dall'output di hello, si noti il valore di hello per hello **valore** proprietà.</span><span class="sxs-lookup"><span data-stu-id="587e2-159">From hello output, note hello value for hello **value** property.</span></span> <span data-ttu-id="587e2-160">È necessario durante l'installazione di Airpal nel edgenode cluster hello.</span><span class="sxs-lookup"><span data-stu-id="587e2-160">You will need this while installing Airpal on hello cluster edgenode.</span></span> <span data-ttu-id="587e2-161">Output di hello precedente valore hello che occorre è **10.0.0.12:9090**.</span><span class="sxs-lookup"><span data-stu-id="587e2-161">From hello output above, hello value that you will need is **10.0.0.12:9090**.</span></span>

4. <span data-ttu-id="587e2-162">Usa modello hello  **[qui](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)**  toocreate un HDInsight edgenode del cluster e fornire valori hello, come illustrato nella seguente schermata hello.</span><span class="sxs-lookup"><span data-stu-id="587e2-162">Use hello template **[here](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)** toocreate an HDInsight cluster edgenode and provide hello values as shown in hello following screenshot.</span></span>

    ![Installazione di HDInsight Airpal nel cluster Presto](./media/hdinsight-hadoop-install-presto/hdinsight-install-airpal.png)

5. <span data-ttu-id="587e2-164">Fare clic su **Acquista**.</span><span class="sxs-lookup"><span data-stu-id="587e2-164">Click **Purchase**.</span></span>

6. <span data-ttu-id="587e2-165">Una volta apportate modifiche hello toohello applicato configurazione del cluster, è possibile accedere interfaccia web di hello Airpal utilizzando hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="587e2-165">Once hello changes are applied toohello cluster configuration, you can access hello Airpal web interface by using hello following steps.</span></span>

    <span data-ttu-id="587e2-166">a.</span><span class="sxs-lookup"><span data-stu-id="587e2-166">a.</span></span> <span data-ttu-id="587e2-167">Dal Pannello di hello cluster, fare clic su **applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="587e2-167">From hello cluster blade, click **Applications**.</span></span>

    ![Avvio di HDInsight Airpal nel cluster Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal.png)

    <span data-ttu-id="587e2-169">b.</span><span class="sxs-lookup"><span data-stu-id="587e2-169">b.</span></span> <span data-ttu-id="587e2-170">Da hello **App installate** pannello, fare clic su **portale** contro airpal.</span><span class="sxs-lookup"><span data-stu-id="587e2-170">From hello **Installed Apps** blade, click **Portal** against airpal.</span></span>

    ![Avvio di HDInsight Airpal nel cluster Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal-1.png)

    <span data-ttu-id="587e2-172">c.</span><span class="sxs-lookup"><span data-stu-id="587e2-172">c.</span></span> <span data-ttu-id="587e2-173">Quando richiesto, immettere le credenziali di amministratore hello specificato durante la creazione di hello cluster HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="587e2-173">When prompted, enter hello admin credentials that you specified while creating hello HDInsight Hadoop cluster.</span></span>

## <a name="customize-a-presto-installation-on-hdinsight-cluster"></a><span data-ttu-id="587e2-174">Personalizzare un'installazione Presto nel cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="587e2-174">Customize a Presto installation on HDInsight cluster</span></span>

<span data-ttu-id="587e2-175">Dopo aver installato in un cluster HDInsight Hadoop accedere, è possibile personalizzare hello installazione toomake modifiche, ad esempio le impostazioni di aggiornamento della memoria, modificare i connettori e così via. Eseguire hello seguendo i passaggi toodo così.</span><span class="sxs-lookup"><span data-stu-id="587e2-175">After you have installed Presto on an HDInsight Hadoop cluster, you can customize hello installation toomake changes such as update memory settings, change connectors, etc. Perform hello following steps toodo so.</span></span>

1. <span data-ttu-id="587e2-176">Tramite SSH, connettersi toohello nodo head del cluster HDInsight hello Presto installato:</span><span class="sxs-lookup"><span data-stu-id="587e2-176">Using SSH, connect toohello headnode of hello HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="587e2-177">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="587e2-177">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="587e2-178">Apportare le modifiche di configurazione nel file hello `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span><span class="sxs-lookup"><span data-stu-id="587e2-178">Make your configuration changes in hello file `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span></span> <span data-ttu-id="587e2-179">Per altre informazioni sulla configurazione di Presto, vedere [Configurazione di Presto per i cluster basati su YARN](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).</span><span class="sxs-lookup"><span data-stu-id="587e2-179">For more information on Presto configuration, see [Presto configuration for YARN-based clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).</span></span>

3. <span data-ttu-id="587e2-180">Interrompere e terminare hello istanza attualmente in esecuzione di accedere.</span><span class="sxs-lookup"><span data-stu-id="587e2-180">Stop and kill hello current running instance of Presto.</span></span>

        sudo slider stop presto1 --force
        sudo slider destroy presto1 --force

4. <span data-ttu-id="587e2-181">Avviare una nuova istanza di accedere a personalizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="587e2-181">Start a new instance of Presto with hello customization.</span></span>

       sudo slider create presto1 --template /var/lib/presto/presto-hdinsight-master/appConfig-default.json --resources /var/lib/presto/presto-hdinsight-master/resources-default.json

5. <span data-ttu-id="587e2-182">Attendere hello nuova istanza toobe pronto e prendere nota indirizzo coordinator presto.</span><span class="sxs-lookup"><span data-stu-id="587e2-182">Wait for hello new instance toobe ready and note presto coordinator address.</span></span>


       sudo slider registry --name presto1 --getexp presto

## <a name="generate-benchmark-data-for-hdinsight-clusters-that-run-presto"></a><span data-ttu-id="587e2-183">Generare dati di benchmark per i cluster HDInsight in cui è in esecuzione Presto</span><span class="sxs-lookup"><span data-stu-id="587e2-183">Generate benchmark data for HDInsight clusters that run Presto</span></span>

<span data-ttu-id="587e2-184">TPC-DS è hello standard per la misurazione delle prestazioni di hello di molti sistemi di supporto decisionale, inclusi i sistemi di dati.</span><span class="sxs-lookup"><span data-stu-id="587e2-184">TPC-DS is hello industry standard for measuring hello performance of many decision support systems, including big data systems.</span></span> <span data-ttu-id="587e2-185">È possibile utilizzare Presto sui dati di toogenerate cluster HDInsight e valutare mette a confronto con i propri dati di riferimento di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="587e2-185">You can use Presto on HDInsight clusters toogenerate data and evaluate how it compares with your own HDInsight benchmark data.</span></span> <span data-ttu-id="587e2-186">Per altre informazioni, vedere [qui](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="587e2-186">For more information, see [here](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span></span>



## <a name="see-also"></a><span data-ttu-id="587e2-187">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="587e2-187">See also</span></span>
* <span data-ttu-id="587e2-188">[Installare e usare Hue nei cluster HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="587e2-188">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="587e2-189">La tonalità corrisponde a un sito web dell'interfaccia utente che rende facile toocreate, eseguire e salvare i processi Pig e Hive, nonché come Sfoglia risorsa di archiviazione di hello predefinito per il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="587e2-189">Hue is a web UI that makes it easy toocreate, run and save Pig and Hive jobs, as well as browse hello default storage for your HDInsight cluster.</span></span>

* <span data-ttu-id="587e2-190">[Installare Giraph in cluster HDInsight](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="587e2-190">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="587e2-191">Utilizzare cluster personalizzazione tooinstall che cluster Giraph in HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="587e2-191">Use cluster customization tooinstall Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="587e2-192">Giraph consente grafico tooperform elaborazione tramite Hadoop e può essere utilizzato con Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="587e2-192">Giraph allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="587e2-193">[Installare Solr in cluster HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="587e2-193">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> <span data-ttu-id="587e2-194">Utilizzare cluster personalizzazione tooinstall che cluster Solr in HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="587e2-194">Use cluster customization tooinstall Solr on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="587e2-195">Solr consente operazioni di ricerca avanzate tooperform sui dati archiviati.</span><span class="sxs-lookup"><span data-stu-id="587e2-195">Solr allows you tooperform powerful search operations on stored data.</span></span>

[hdinsight-install-r]: hdinsight-hadoop-r-scripts-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
