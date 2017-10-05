---
title: Installare Presto nei cluster Azure HDInsight Linux | Microsoft Docs
description: Informazioni su come installare Presto e Airpal nei cluster HDInsight Hadoop basati su Linux usando azioni di script.
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
ms.openlocfilehash: 406ef84e72d253fec51a0b37c48f326dafd511b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-use-presto-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="f5a23-103">Installare e usare Presto nei cluster HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="f5a23-103">Install and use Presto on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="f5a23-104">In questo argomento si apprenderà come installare Presto nei cluster HDInsight Hadoop usando le azioni di script.</span><span class="sxs-lookup"><span data-stu-id="f5a23-104">In this topic, you learn how to install Presto on HDInsight Hadoop clusters by using Script Action.</span></span> <span data-ttu-id="f5a23-105">Si apprenderà anche come installare Airpal in un cluster HDInsight Presto esistente.</span><span class="sxs-lookup"><span data-stu-id="f5a23-105">You also learn how to install Airpal on an existing Presto HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f5a23-106">I passaggi descritti in questo documento richiedono un cluster **HDInsight 3.5 Hadoop** che usa Linux.</span><span class="sxs-lookup"><span data-stu-id="f5a23-106">The steps in this document require an **HDInsight 3.5 Hadoop cluster** that uses Linux.</span></span> <span data-ttu-id="f5a23-107">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="f5a23-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f5a23-108">Per altre informazioni, vedere [Versioni di HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="f5a23-108">For more information, see [HDInsight versions](hdinsight-component-versioning.md).</span></span>

## <a name="what-is-presto"></a><span data-ttu-id="f5a23-109">Che cos'è Presto?</span><span class="sxs-lookup"><span data-stu-id="f5a23-109">What is Presto?</span></span>
<span data-ttu-id="f5a23-110">[Presto](https://prestodb.io/overview.html) è un motore di query SQL distribuito veloce per Big Data.</span><span class="sxs-lookup"><span data-stu-id="f5a23-110">[Presto](https://prestodb.io/overview.html) is a fast distributed SQL query engine for big data.</span></span> <span data-ttu-id="f5a23-111">Presto è adatto per l'esecuzione di query interattive di petabyte di dati.</span><span class="sxs-lookup"><span data-stu-id="f5a23-111">Presto is suitable for interactive querying of petabytes of data.</span></span> <span data-ttu-id="f5a23-112">Per altre informazioni sui componenti di Presto e il relativo funzionamento, vedere [Presto concepts](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst) (Concetti di Presto).</span><span class="sxs-lookup"><span data-stu-id="f5a23-112">For more information on the components of Presto and how they work together, see [Presto concepts](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span></span>

> [!WARNING]
> <span data-ttu-id="f5a23-113">I componenti forniti con il cluster HDInsight sono supportati in modo completo e il Supporto Microsoft contribuirà a isolare e risolvere i problemi correlati a questi componenti.</span><span class="sxs-lookup"><span data-stu-id="f5a23-113">Components provided with the HDInsight cluster are fully supported and Microsoft Support will help to isolate and resolve issues related to these components.</span></span>
> 
> <span data-ttu-id="f5a23-114">I componenti personalizzati, ad esempio Presto, ricevono un supporto commercialmente ragionevole per semplificare la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="f5a23-114">Custom components, such as Presto, receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="f5a23-115">È possibile che si ottenga la risoluzione dei problemi o che venga richiesto di usare i canali disponibili per le tecnologie open source, in cui è possibile ottenere supporto approfondito per la tecnologia specifica.</span><span class="sxs-lookup"><span data-stu-id="f5a23-115">This might result in resolving the issue OR asking you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="f5a23-116">È ad esempio possibile ricorrere a molti siti di community, come il [forum MSDN per HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight) o [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="f5a23-116">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="f5a23-117">Anche per i progetti Apache sono disponibili siti specifici in [http://apache.org](http://apache.org), ad esempio [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="f5a23-117">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>
> 
> 


## <a name="install-presto-using-script-action"></a><span data-ttu-id="f5a23-118">Installare Presto mediante l'azione di script</span><span class="sxs-lookup"><span data-stu-id="f5a23-118">Install Presto using script action</span></span>

<span data-ttu-id="f5a23-119">Questa sezione fornisce istruzioni su come usare lo script di esempio quando si crea un nuovo cluster usando il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5a23-119">This section provides instructions on how to use the sample script when creating a new cluster by using the Azure portal.</span></span> 

1. <span data-ttu-id="f5a23-120">Avviare il provisioning di un cluster seguendo i passaggi descritti in [Effettuare il provisioning di cluster HDInsight basati su Linux](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f5a23-120">Start provisioning a cluster by using the steps in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span> <span data-ttu-id="f5a23-121">Assicurarsi di creare il cluster usando il flusso di creazione del cluster **personalizzato**.</span><span class="sxs-lookup"><span data-stu-id="f5a23-121">Make sure you create the cluster using the **Custom** cluster creation flow.</span></span> <span data-ttu-id="f5a23-122">È necessario assicurarsi che il cluster creato soddisfi i requisiti seguenti.</span><span class="sxs-lookup"><span data-stu-id="f5a23-122">You must ensure that the cluster you create meets the following requirements.</span></span>

    <span data-ttu-id="f5a23-123">a.</span><span class="sxs-lookup"><span data-stu-id="f5a23-123">a.</span></span> <span data-ttu-id="f5a23-124">Deve essere un cluster Hadoop con HDInsight versione 3.5.</span><span class="sxs-lookup"><span data-stu-id="f5a23-124">It must be a Hadoop cluster with HDInsight version 3.5.</span></span>

    <span data-ttu-id="f5a23-125">b.</span><span class="sxs-lookup"><span data-stu-id="f5a23-125">b.</span></span> <span data-ttu-id="f5a23-126">Deve usare Archiviazione di Azure come archivio dati.</span><span class="sxs-lookup"><span data-stu-id="f5a23-126">It must use Azure Storage as the data store.</span></span> <span data-ttu-id="f5a23-127">L'uso di Presto in un cluster che usa Azure Data Lake Store come opzione di archiviazione non è ancora supportato.</span><span class="sxs-lookup"><span data-stu-id="f5a23-127">Using Presto on a cluster that uses Azure Data Lake Store as the storage option is not yet supported.</span></span> 

    ![Creazione del cluster HDInsight con opzioni personalizzate](./media/hdinsight-hadoop-install-presto/hdinsight-install-custom.png)

2. <span data-ttu-id="f5a23-129">Nel pannello **Impostazioni avanzate** selezionare **Azioni script** e specificare le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f5a23-129">On the **Advanced settings** blade, select **Script Actions**, and provide the information below:</span></span>
   
   * <span data-ttu-id="f5a23-130">**NOME**: immettere un nome descrittivo per l'azione script.</span><span class="sxs-lookup"><span data-stu-id="f5a23-130">**NAME**: Enter a friendly name for the script action.</span></span>
   * <span data-ttu-id="f5a23-131">**URI script Bash**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span><span class="sxs-lookup"><span data-stu-id="f5a23-131">**Bash script URI**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span></span>
   * <span data-ttu-id="f5a23-132">**HEAD**: selezionare questa opzione</span><span class="sxs-lookup"><span data-stu-id="f5a23-132">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="f5a23-133">**RUOLO DI LAVORO**: selezionare questa opzione</span><span class="sxs-lookup"><span data-stu-id="f5a23-133">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="f5a23-134">**ZOOKEEPER**: deselezionare questa casella di controllo</span><span class="sxs-lookup"><span data-stu-id="f5a23-134">**ZOOKEEPER**: Clear this check box</span></span>
   * <span data-ttu-id="f5a23-135">**PARAMETRI**: lasciare questo campo vuoto</span><span class="sxs-lookup"><span data-stu-id="f5a23-135">**PARAMETERS**: Leave this field blank</span></span>


3. <span data-ttu-id="f5a23-136">Nella parte inferiore del pannello **Azioni script** fare clic sul pulsante **Seleziona** per salvare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="f5a23-136">At the bottom of the **Script Actions** blade, click the **Select** button to save the configuration.</span></span> <span data-ttu-id="f5a23-137">Infine fare clic sul pulsante **Seleziona** nella parte inferiore del pannello **Impostazioni avanzate** per salvare le informazioni relative alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="f5a23-137">Finally, click  the **Select** button at the bottom of the **Advanced Settings** blade to save the configuration information.</span></span>

4. <span data-ttu-id="f5a23-138">Continuare il provisioning del cluster come descritto nell'argomento relativo all' [esecuzione del provisioning di cluster HDInsight basati su Linux](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f5a23-138">Continue provisioning the cluster as described in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="f5a23-139">Per applicare le azioni script è possibile usare anche Azure PowerShell, l'interfaccia della riga di comando di Azure, HDInsight .NET SDK o i modelli di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f5a23-139">Azure PowerShell, the Azure CLI, the HDInsight .NET SDK, or Azure Resource Manager templates can also be used to apply script actions.</span></span> <span data-ttu-id="f5a23-140">È anche possibile applicare azioni script a cluster già in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f5a23-140">You can also apply script actions to already running clusters.</span></span> <span data-ttu-id="f5a23-141">Per altre informazioni, vedere [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f5a23-141">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
    > 
    > 

## <a name="use-presto-with-hdinsight"></a><span data-ttu-id="f5a23-142">Usare Presto con HDInsight</span><span class="sxs-lookup"><span data-stu-id="f5a23-142">Use Presto with HDInsight</span></span>

<span data-ttu-id="f5a23-143">Eseguire i passaggi seguenti per usare Presto in un cluster HDInsight dopo averlo installato con la procedura descritta in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f5a23-143">Perform the following steps to use Presto in an HDInsight cluster after you have installed it using the steps described above.</span></span>

1. <span data-ttu-id="f5a23-144">Connettersi al cluster HDInsight usando SSH:</span><span class="sxs-lookup"><span data-stu-id="f5a23-144">Connect to the HDInsight cluster using SSH:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="f5a23-145">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f5a23-145">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
     

2. <span data-ttu-id="f5a23-146">Avviare la shell di Presto usando il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="f5a23-146">Start the Presto shell using the following command.</span></span>
   
        presto --schema default

3. <span data-ttu-id="f5a23-147">Eseguire una query sulla tabella di esempio, **hivesampletable**, che è disponibile in tutti i cluster HDInsight per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="f5a23-147">Run a query on a sample table, **hivesampletable**, which is available on all HDInsight clusters by default.</span></span>
   
        select count (*) from hivesampletable;
   
    <span data-ttu-id="f5a23-148">Per impostazione predefinita sono già configurati i connettori [Hive](https://prestodb.io/docs/current/connector/hive.html) e [TPCH](https://prestodb.io/docs/current/connector/tpch.html) per Presto.</span><span class="sxs-lookup"><span data-stu-id="f5a23-148">By default, [Hive](https://prestodb.io/docs/current/connector/hive.html) and [TPCH](https://prestodb.io/docs/current/connector/tpch.html) connectors for Presto are already configured.</span></span> <span data-ttu-id="f5a23-149">Il connettore Hive è configurato per usare l'installazione Hive predefinita, in modo che tutte le tabelle provenienti da Hive diventino automaticamente visibili in Presto.</span><span class="sxs-lookup"><span data-stu-id="f5a23-149">Hive connector is configured to use the default installed Hive installation, so all the tables from Hive will be automatically visible in Presto.</span></span>

    <span data-ttu-id="f5a23-150">Per informazioni dettagliate su come è possibile usate Presto, vedere la [documentazione su Presto](https://prestodb.io/docs/current/index.html).</span><span class="sxs-lookup"><span data-stu-id="f5a23-150">For a detailed description on how you can use Presto, see [Presto documentation](https://prestodb.io/docs/current/index.html).</span></span>

## <a name="use-airpal-with-presto"></a><span data-ttu-id="f5a23-151">Usare Airpal con Presto</span><span class="sxs-lookup"><span data-stu-id="f5a23-151">Use Airpal with Presto</span></span>

<span data-ttu-id="f5a23-152">[Airpal](https://github.com/airbnb/airpal#airpal) è un'interfaccia per query basate su Web open source per Presto.</span><span class="sxs-lookup"><span data-stu-id="f5a23-152">[Airpal](https://github.com/airbnb/airpal#airpal) is an open-source web-based query interface for Presto.</span></span> <span data-ttu-id="f5a23-153">Per altre informazioni su Airpal, vedere la [documentazione su Airpal](https://github.com/airbnb/airpal#airpal).</span><span class="sxs-lookup"><span data-stu-id="f5a23-153">For more information on Airpal, see [Airpal documentation](https://github.com/airbnb/airpal#airpal).</span></span>

<span data-ttu-id="f5a23-154">In questa sezione verrà esaminata la procedura per **installare Airpal sul nodo perimetrale** di un cluster HDInsight Hadoop in cui Presto è già installato.</span><span class="sxs-lookup"><span data-stu-id="f5a23-154">In this section, we look at the steps to **install Airpal on the edgenode** of an HDInsight Hadoop cluster, that already has Presto installed.</span></span> <span data-ttu-id="f5a23-155">Ciò garantisce che l'interfaccia per query Web Airpal sia disponibile su Internet.</span><span class="sxs-lookup"><span data-stu-id="f5a23-155">This ensures that the Airpal web query interface is available over the Internet.</span></span>

1. <span data-ttu-id="f5a23-156">Connettersi tramite SSH al nodo head del cluster HDInsight in cui è installato Presto:</span><span class="sxs-lookup"><span data-stu-id="f5a23-156">Using SSH, connect to the headnode of the HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="f5a23-157">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f5a23-157">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="f5a23-158">Una volta eseguita la connessione, eseguire il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="f5a23-158">Once you are connected, run the following command.</span></span>

        sudo slider registry  --name presto1 --getexp presto 
   
    <span data-ttu-id="f5a23-159">Verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="f5a23-159">You should see an output like the following:</span></span>

        {
            "coordinator_address" : [ {
                "value" : "10.0.0.12:9090",
                "level" : "application",
                "updatedTime" : "Mon Apr 03 20:13:41 UTC 2017"
        } ]

3. <span data-ttu-id="f5a23-160">Nell'output prendere nota del valore per la proprietà **value**.</span><span class="sxs-lookup"><span data-stu-id="f5a23-160">From the output, note the value for the **value** property.</span></span> <span data-ttu-id="f5a23-161">Sarà necessario durante l'installazione di Airpal nel nodo perimetrale del cluster.</span><span class="sxs-lookup"><span data-stu-id="f5a23-161">You will need this while installing Airpal on the cluster edgenode.</span></span> <span data-ttu-id="f5a23-162">Dall'output precedente il valore che sarà necessario è **10.0.0.12:9090**.</span><span class="sxs-lookup"><span data-stu-id="f5a23-162">From the output above, the value that you will need is **10.0.0.12:9090**.</span></span>

4. <span data-ttu-id="f5a23-163">Usare il modello  **[qui](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)**  per creare un nodo perimetrale del cluster HDInsight e fornire i valori come illustrato nello screenshot seguente.</span><span class="sxs-lookup"><span data-stu-id="f5a23-163">Use the template **[here](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)** to create an HDInsight cluster edgenode and provide the values as shown in the following screenshot.</span></span>

    ![Installazione di HDInsight Airpal nel cluster Presto](./media/hdinsight-hadoop-install-presto/hdinsight-install-airpal.png)

5. <span data-ttu-id="f5a23-165">Fare clic su **Acquista**.</span><span class="sxs-lookup"><span data-stu-id="f5a23-165">Click **Purchase**.</span></span>

6. <span data-ttu-id="f5a23-166">Dopo le modifiche vengono applicate alla configurazione del cluster, è possibile accedere all'interfaccia web Airpal usando la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="f5a23-166">Once the changes are applied to the cluster configuration, you can access the Airpal web interface by using the following steps.</span></span>

    <span data-ttu-id="f5a23-167">a.</span><span class="sxs-lookup"><span data-stu-id="f5a23-167">a.</span></span> <span data-ttu-id="f5a23-168">Fare clic su **Applicazioni** nel pannello del cluster.</span><span class="sxs-lookup"><span data-stu-id="f5a23-168">From the cluster blade, click **Applications**.</span></span>

    ![Avvio di HDInsight Airpal nel cluster Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal.png)

    <span data-ttu-id="f5a23-170">b.</span><span class="sxs-lookup"><span data-stu-id="f5a23-170">b.</span></span> <span data-ttu-id="f5a23-171">Dal pannello **App installate** fare clic su **Portale** per Airpal.</span><span class="sxs-lookup"><span data-stu-id="f5a23-171">From the **Installed Apps** blade, click **Portal** against airpal.</span></span>

    ![Avvio di HDInsight Airpal nel cluster Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal-1.png)

    <span data-ttu-id="f5a23-173">c.</span><span class="sxs-lookup"><span data-stu-id="f5a23-173">c.</span></span> <span data-ttu-id="f5a23-174">Quando richiesto, immettere le credenziali admin specificate durante la creazione del cluster HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="f5a23-174">When prompted, enter the admin credentials that you specified while creating the HDInsight Hadoop cluster.</span></span>

## <a name="customize-a-presto-installation-on-hdinsight-cluster"></a><span data-ttu-id="f5a23-175">Personalizzare un'installazione Presto nel cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="f5a23-175">Customize a Presto installation on HDInsight cluster</span></span>

<span data-ttu-id="f5a23-176">Dopo avere installato Presto in un cluster HDInsight Hadoop, è possibile personalizzare l'installazione per apportare modifiche, ad esempio aggiornare le impostazioni della memoria, modificare i connettori e così via. Seguire quindi questa procedura.</span><span class="sxs-lookup"><span data-stu-id="f5a23-176">After you have installed Presto on an HDInsight Hadoop cluster, you can customize the installation to make changes such as update memory settings, change connectors, etc. Perform the following steps to do so.</span></span>

1. <span data-ttu-id="f5a23-177">Connettersi tramite SSH al nodo head del cluster HDInsight in cui è installato Presto:</span><span class="sxs-lookup"><span data-stu-id="f5a23-177">Using SSH, connect to the headnode of the HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="f5a23-178">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f5a23-178">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="f5a23-179">Apportare le modifiche di configurazione nel file `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span><span class="sxs-lookup"><span data-stu-id="f5a23-179">Make your configuration changes in the file `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span></span> <span data-ttu-id="f5a23-180">Per altre informazioni sulla configurazione di Presto, vedere [Configurazione di Presto per i cluster basati su YARN](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).</span><span class="sxs-lookup"><span data-stu-id="f5a23-180">For more information on Presto configuration, see [Presto configuration for YARN-based clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).</span></span>

3. <span data-ttu-id="f5a23-181">Arrestare e terminare l'istanza in esecuzione corrente di Presto.</span><span class="sxs-lookup"><span data-stu-id="f5a23-181">Stop and kill the current running instance of Presto.</span></span>

        sudo slider stop presto1 --force
        sudo slider destroy presto1 --force

4. <span data-ttu-id="f5a23-182">Avviare una nuova istanza di Presto con la personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="f5a23-182">Start a new instance of Presto with the customization.</span></span>

       sudo slider create presto1 --template /var/lib/presto/presto-hdinsight-master/appConfig-default.json --resources /var/lib/presto/presto-hdinsight-master/resources-default.json

5. <span data-ttu-id="f5a23-183">Attendere che la nuova istanza sia pronta e annotare l'indirizzo del coordinatore di Presto.</span><span class="sxs-lookup"><span data-stu-id="f5a23-183">Wait for the new instance to be ready and note presto coordinator address.</span></span>


       sudo slider registry --name presto1 --getexp presto

## <a name="generate-benchmark-data-for-hdinsight-clusters-that-run-presto"></a><span data-ttu-id="f5a23-184">Generare dati di benchmark per i cluster HDInsight in cui è in esecuzione Presto</span><span class="sxs-lookup"><span data-stu-id="f5a23-184">Generate benchmark data for HDInsight clusters that run Presto</span></span>

<span data-ttu-id="f5a23-185">TPC-DS è lo standard del settore per la misurazione delle prestazioni di molti sistemi di supporto decisionale, compresi i sistemi di Big Data.</span><span class="sxs-lookup"><span data-stu-id="f5a23-185">TPC-DS is the industry standard for measuring the performance of many decision support systems, including big data systems.</span></span> <span data-ttu-id="f5a23-186">È possibile usare Presto nei cluster HDInsight per generare i dati e confrontarli con i dati di benchmark di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f5a23-186">You can use Presto on HDInsight clusters to generate data and evaluate how it compares with your own HDInsight benchmark data.</span></span> <span data-ttu-id="f5a23-187">Per altre informazioni, vedere [qui](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="f5a23-187">For more information, see [here](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span></span>



## <a name="see-also"></a><span data-ttu-id="f5a23-188">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f5a23-188">See also</span></span>
* <span data-ttu-id="f5a23-189">[Installare e usare Hue nei cluster HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f5a23-189">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="f5a23-190">Hue è un'interfaccia utente che semplifica la creazione, l'esecuzione e il salvataggio di processi Pig e Hive, nonché l'esplorazione dell'archivio predefinito per il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f5a23-190">Hue is a web UI that makes it easy to create, run and save Pig and Hive jobs, as well as browse the default storage for your HDInsight cluster.</span></span>

* <span data-ttu-id="f5a23-191">[Installare Giraph in cluster HDInsight](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f5a23-191">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="f5a23-192">Usare la personalizzazione cluster per installare Giraph in cluster Hadoop di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f5a23-192">Use cluster customization to install Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="f5a23-193">Giraph permette di elaborare grafici con Hadoop e può essere usato con Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f5a23-193">Giraph allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="f5a23-194">[Installare Solr in cluster HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f5a23-194">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> <span data-ttu-id="f5a23-195">Usare la personalizzazione cluster per installare Solr in cluster Hadoop di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f5a23-195">Use cluster customization to install Solr on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="f5a23-196">Solr consente di eseguire operazioni di ricerca avanzate sui dati archiviati.</span><span class="sxs-lookup"><span data-stu-id="f5a23-196">Solr allows you to perform powerful search operations on stored data.</span></span>

[hdinsight-install-r]: hdinsight-hadoop-r-scripts-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
