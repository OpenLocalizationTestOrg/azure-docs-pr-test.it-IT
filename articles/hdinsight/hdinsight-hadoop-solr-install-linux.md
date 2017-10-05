---
title: Usare un'azione script per installare Solr in HDInsight basato su Linux | Documentazione Microsoft
description: Informazioni su come installare Solr nei cluster HDInsight Hadoop basati su Linux utilizzando azioni di Script.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cc93ed5c-a358-456a-91a4-f179185c0e98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: ad930ca023a36fa5874483873c82fdba11d117c7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="install-and-use-solr-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="3e720-103">Installare e usare Solr nei cluster Hadoop di HDInsight</span><span class="sxs-lookup"><span data-stu-id="3e720-103">Install and use Solr on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="3e720-104">Informazioni su come installare Solr in Azure HDInsight usando un'azione script.</span><span class="sxs-lookup"><span data-stu-id="3e720-104">Learn how to install Solr on Azure HDInsight by using Script Action.</span></span> <span data-ttu-id="3e720-105">Solr è una piattaforma di ricerca avanzata e offre funzionalità di ricerca di livello aziendale per i dati gestiti da Hadoop.</span><span class="sxs-lookup"><span data-stu-id="3e720-105">Solr is a powerful search platform and provides enterprise-level search capabilities on data managed by Hadoop.</span></span>

> [!IMPORTANT]
    > <span data-ttu-id="3e720-106">I passaggi descritti in questo documento richiedono un cluster HDInsight che usa Linux.</span><span class="sxs-lookup"><span data-stu-id="3e720-106">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="3e720-107">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="3e720-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3e720-108">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="3e720-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3e720-109">Lo script di esempio usato in questo documento installa Solr 4.9 con una configurazione specifica.</span><span class="sxs-lookup"><span data-stu-id="3e720-109">The sample script used in this document installs Solr 4.9 with a specific configuration.</span></span> <span data-ttu-id="3e720-110">Per configurare il cluster Solr con raccolte, partizioni, schemi, repliche diverse e così via, sarà necessario modificare lo script e i file binari di Solr.</span><span class="sxs-lookup"><span data-stu-id="3e720-110">If you want to configure the Solr cluster with different collections, shards, schemas, replicas, etc., you must modify the script and Solr binaries.</span></span>

## <span data-ttu-id="3e720-111"><a name="whatis"></a>Che cos'è Solr</span><span class="sxs-lookup"><span data-stu-id="3e720-111"><a name="whatis"></a>What is Solr</span></span>

<span data-ttu-id="3e720-112">[Apache Solr](http://lucene.apache.org/solr/features.html) è una piattaforma di ricerca aziendale che permette di eseguire ricerche full-text avanzate sui dati.</span><span class="sxs-lookup"><span data-stu-id="3e720-112">[Apache Solr](http://lucene.apache.org/solr/features.html) is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="3e720-113">Mentre Hadoop consente di archiviare e gestire quantità elevate di dati, Apache Solr offre le funzionalità di ricerca necessarie per recuperare rapidamente i dati.</span><span class="sxs-lookup"><span data-stu-id="3e720-113">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides the search capabilities to quickly retrieve the data.</span></span>

> [!WARNING]
> <span data-ttu-id="3e720-114">I componenti forniti con il cluster HDInsight sono completamente supportati da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3e720-114">Components provided with the HDInsight cluster are fully supported by Microsoft.</span></span>
>
> <span data-ttu-id="3e720-115">I componenti personalizzati, ad esempio Solr, ricevono supporto commercialmente ragionevole per semplificare la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="3e720-115">Custom components, such as Solr, receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="3e720-116">Il supporto tecnico Microsoft potrebbe non essere in grado di risolvere i problemi con componenti personalizzati.</span><span class="sxs-lookup"><span data-stu-id="3e720-116">Microsoft support may not be able to resolve problems with custom components.</span></span> <span data-ttu-id="3e720-117">Potrebbe essere necessario coinvolgere le community open source per ricevere assistenza.</span><span class="sxs-lookup"><span data-stu-id="3e720-117">You may need to engage the open source communities for assistance.</span></span> <span data-ttu-id="3e720-118">È ad esempio possibile ricorrere a molti siti di community, come il [forum MSDN per HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight) o [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="3e720-118">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="3e720-119">Anche per i progetti Apache sono disponibili siti specifici in [http://apache.org](http://apache.org), ad esempio [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="3e720-119">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

## <a name="what-the-script-does"></a><span data-ttu-id="3e720-120">Funzionalità dello script</span><span class="sxs-lookup"><span data-stu-id="3e720-120">What the script does</span></span>

<span data-ttu-id="3e720-121">Questo script apporta le modifiche seguenti al cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="3e720-121">This script makes the following changes to the HDInsight cluster:</span></span>

* <span data-ttu-id="3e720-122">Installa Solr 4.9 in `/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="3e720-122">Installs Solr 4.9 into `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="3e720-123">Crea un utente **solrusr**, usato per eseguire il servizio Solr</span><span class="sxs-lookup"><span data-stu-id="3e720-123">Creates a user, **solrusr**, which is used to run the Solr service</span></span>
* <span data-ttu-id="3e720-124">Imposta **solrusr** come proprietario di `/usr/hdp/current/solr`.</span><span class="sxs-lookup"><span data-stu-id="3e720-124">Sets **solruser** as the owner of `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="3e720-125">Aggiunge una configurazione [Upstart](http://upstart.ubuntu.com/) che avvia automaticamente Solr.</span><span class="sxs-lookup"><span data-stu-id="3e720-125">Adds an [Upstart](http://upstart.ubuntu.com/) configuration that starts Solr automatically.</span></span>

## <span data-ttu-id="3e720-126"><a name="install"></a>Installare R mediante azioni script</span><span class="sxs-lookup"><span data-stu-id="3e720-126"><a name="install"></a>Install Solr using Script Actions</span></span>

<span data-ttu-id="3e720-127">Uno script di esempio per l'installazione di Solr in un cluster HDInsight è disponibile all'indirizzo seguente:</span><span class="sxs-lookup"><span data-stu-id="3e720-127">A sample script to install Solr on an HDInsight cluster is available at the following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh

<span data-ttu-id="3e720-128">Per creare un cluster con Solr installato, usare la procedura nel documento [Creare cluster basati su Linux in HDInsight tramite il portale di Azure](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3e720-128">To create a cluster that has Solr installed, use the steps in the [Create HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md) document.</span></span> <span data-ttu-id="3e720-129">Durante il processo di creazione, usare la procedura seguente per installare Solr:</span><span class="sxs-lookup"><span data-stu-id="3e720-129">During the creation process, use the following steps to install Solr:</span></span>

1. <span data-ttu-id="3e720-130">Dal pannello __Riepilogo cluster__, selezionare__Impostazioni avanzate__ e quindi __Azioni script__.</span><span class="sxs-lookup"><span data-stu-id="3e720-130">From the __Cluster summary__ blade, select__Advanced settings__, then __Script actions__.</span></span> <span data-ttu-id="3e720-131">Usare le seguenti informazioni per popolare il modulo:</span><span class="sxs-lookup"><span data-stu-id="3e720-131">Use the following information to populate the form:</span></span>

   * <span data-ttu-id="3e720-132">**NOME**: immettere un nome descrittivo per l'azione script.</span><span class="sxs-lookup"><span data-stu-id="3e720-132">**NAME**: Enter a friendly name for the script action.</span></span>
   * <span data-ttu-id="3e720-133">**URI SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="3e720-133">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span></span>
   * <span data-ttu-id="3e720-134">**HEAD**: selezionare questa opzione</span><span class="sxs-lookup"><span data-stu-id="3e720-134">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="3e720-135">**RUOLO DI LAVORO**: selezionare questa opzione</span><span class="sxs-lookup"><span data-stu-id="3e720-135">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="3e720-136">**ZOOKEEPER**: selezionare questa opzione per l'installazione nel nodo Zookeeper</span><span class="sxs-lookup"><span data-stu-id="3e720-136">**ZOOKEEPER**: Check this option to install on the Zookeeper node</span></span>
   * <span data-ttu-id="3e720-137">**PARAMETRI**: lasciare questo campo vuoto</span><span class="sxs-lookup"><span data-stu-id="3e720-137">**PARAMETERS**: Leave this field blank</span></span>

2. <span data-ttu-id="3e720-138">Nella parte inferiore del pannello **Azioni script** usare il pulsante **Seleziona** per salvare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="3e720-138">At the bottom of the **Script actions** blade, use the **Select** button to save the configuration.</span></span> <span data-ttu-id="3e720-139">Infine, usare il pulsante **Avanti** per tornare al __Riepilogo cluster__</span><span class="sxs-lookup"><span data-stu-id="3e720-139">Finally, use the **Next** button to return to the __Cluster summary__</span></span>

3. <span data-ttu-id="3e720-140">Dalla pagina __Riepilogo cluster__ selezionare __Crea__ per creare il cluster.</span><span class="sxs-lookup"><span data-stu-id="3e720-140">From the __Cluster summary__ page, select __Create__ to create the cluster.</span></span>

## <span data-ttu-id="3e720-141"><a name="usesolr"></a>Come si usa Solr in HDInsight</span><span class="sxs-lookup"><span data-stu-id="3e720-141"><a name="usesolr"></a>How do I use Solr in HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3e720-142">I passaggi in questa sezione illustrano le funzionalità di base di Solr.</span><span class="sxs-lookup"><span data-stu-id="3e720-142">The steps in this section demonstrate basic Solr functionality.</span></span> <span data-ttu-id="3e720-143">Per altre informazioni sull'uso di Solr, vedere il [sito Apache Solr](http://lucene.apache.org/solr/).</span><span class="sxs-lookup"><span data-stu-id="3e720-143">For more information on using Solr, see the [Apache Solr site](http://lucene.apache.org/solr/).</span></span>

### <a name="index-data"></a><span data-ttu-id="3e720-144">Dati dell'indice</span><span class="sxs-lookup"><span data-stu-id="3e720-144">Index data</span></span>

<span data-ttu-id="3e720-145">Usare i passaggi seguenti per aggiungere dei dati di esempio a Solr e quindi eseguire una query:</span><span class="sxs-lookup"><span data-stu-id="3e720-145">Use the following steps to add example data to Solr, and then query it:</span></span>

1. <span data-ttu-id="3e720-146">Connettersi al cluster HDInsight usando SSH:</span><span class="sxs-lookup"><span data-stu-id="3e720-146">Connect to the HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="3e720-147">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="3e720-147">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="3e720-148">I passaggi successivi di questo documento usano un tunnel SSL per la connessione all'interfaccia utente Web di Solr.</span><span class="sxs-lookup"><span data-stu-id="3e720-148">Steps later in this document use an SSL tunnel to connect to the Solr web UI.</span></span> <span data-ttu-id="3e720-149">Per usare questi passaggi, è necessario stabilire un tunnel SSL e quindi configurare il browser per usarlo.</span><span class="sxs-lookup"><span data-stu-id="3e720-149">To use these steps, you must establish an SSL tunnel and then configure your browser to use it.</span></span>
     >
     > <span data-ttu-id="3e720-150">Per altre informazioni, vedere il documento [Usare il tunneling SSH per accedere all'interfaccia Web di Ambari, JobHistory, NameNode, Oozie e altre interfacce Web](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="3e720-150">For more information, see the [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="3e720-151">Usare i comandi seguenti per indicizzare i dati di esempio tramite Solr:</span><span class="sxs-lookup"><span data-stu-id="3e720-151">Use the following commands to have Solr index sample data:</span></span>

    ```bash
    cd /usr/hdp/current/solr/example/exampledocs
    java -jar post.jar solr.xml monitor.xml
    ```

    <span data-ttu-id="3e720-152">Viene restituito l'output seguente alla console:</span><span class="sxs-lookup"><span data-stu-id="3e720-152">The following output is returned to the console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes to http://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="3e720-153">L'utilità `post.jar` aggiunge i documenti **solr.xml** e **monitor.xml** all'indice.</span><span class="sxs-lookup"><span data-stu-id="3e720-153">The `post.jar` utility adds the **solr.xml** and **monitor.xml** documents to the index.</span></span>
  
3. <span data-ttu-id="3e720-154">Usare il comando seguente per eseguire query nell'API REST Solr:</span><span class="sxs-lookup"><span data-stu-id="3e720-154">Use the following command to query the Solr REST API:</span></span>

    ```bash
    curl "http://localhost:8983/solr/collection1/select?q=*%3A*&wt=json&indent=true"
    ```

    <span data-ttu-id="3e720-155">Questo comando cerca **collection1** per tutti i documenti corrispondenti **\*:\*** (codificato come \*% 3A\* nella stringa della query).</span><span class="sxs-lookup"><span data-stu-id="3e720-155">This command searches **collection1** for any documents matching **\*:\*** (encoded as \*%3A\* in the query string).</span></span> <span data-ttu-id="3e720-156">Il documento JSON seguente è un esempio della risposta:</span><span class="sxs-lookup"><span data-stu-id="3e720-156">The following JSON document is an example of the response:</span></span>

            "response": {
                "numFound": 2,
                "start": 0,
                "maxScore": 1,
                "docs": [
                  {
                    "id": "SOLR1000",
                    "name": "Solr, the Enterprise Search Server",
                    "manu": "Apache Software Foundation",
                    "cat": [
                      "software",
                      "search"
                    ],
                    "features": [
                      "Advanced Full-Text Search Capabilities using Lucene",
                      "Optimized for High Volume Web Traffic",
                      "Standards Based Open Interfaces - XML and HTTP",
                      "Comprehensive HTML Administration Interfaces",
                      "Scalability - Efficient Replication to other Solr Search Servers",
                      "Flexible and Adaptable with XML configuration and Schema",
                      "Good unicode support: héllo (hello with an accent over the e)"
                    ],
                    "price": 0,
                    "price_c": "0,USD",
                    "popularity": 10,
                    "inStock": true,
                    "incubationdate_dt": "2006-01-17T00:00:00Z",
                    "_version_": 1486960636996878300
                  },
                  {
                    "id": "3007WFP",
                    "name": "Dell Widescreen UltraSharp 3007WFP",
                    "manu": "Dell, Inc.",
                    "manu_id_s": "dell",
                    "cat": [
                      "electronics and computer1"
                    ],
                    "features": [
                      "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                    ],
                    "includes": "USB cable",
                    "weight": 401.6,
                    "price": 2199,
                    "price_c": "2199,USD",
                    "popularity": 6,
                    "inStock": true,
                    "store": "43.17614,-90.57341",
                    "_version_": 1486960637584081000
                  }
                ]
              }

### <a name="using-the-solr-dashboard"></a><span data-ttu-id="3e720-157">Uso del dashboard di Solr</span><span class="sxs-lookup"><span data-stu-id="3e720-157">Using the Solr dashboard</span></span>

<span data-ttu-id="3e720-158">Il dashboard di Solr è un'interfaccia utente Web che consente di utilizzare Solr con un Web browser.</span><span class="sxs-lookup"><span data-stu-id="3e720-158">The Solr dashboard is a web UI that allows you to work with Solr through your web browser.</span></span> <span data-ttu-id="3e720-159">Il dashboard di Solr non viene esposto direttamente su Internet dal cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3e720-159">The Solr dashboard is not exposed directly on the Internet from your HDInsight cluster.</span></span> <span data-ttu-id="3e720-160">È possibile usare un tunnel SSH per accedere al servizio.</span><span class="sxs-lookup"><span data-stu-id="3e720-160">You can use an SSH tunnel to access it.</span></span> <span data-ttu-id="3e720-161">Per altre informazioni sull'uso del tunnel SSH, vedere il documento [Usare il tunneling SSH per accedere all'interfaccia Web di Ambari, JobHistory, NameNode, Oozie e altre interfacce Web](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="3e720-161">For more information on using an SSH tunnel, see the [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="3e720-162">Dopo aver stabilito un tunnel SSH, seguire questa procedura per usare il dashboard di Solr:</span><span class="sxs-lookup"><span data-stu-id="3e720-162">Once you have established an SSH tunnel, use the following steps to use the Solr dashboard:</span></span>

1. <span data-ttu-id="3e720-163">Determinare il nome host per il nodo head primario:</span><span class="sxs-lookup"><span data-stu-id="3e720-163">Determine the host name for the primary headnode:</span></span>

   1. <span data-ttu-id="3e720-164">Usare SSH per connettersi al nodo head del cluster.</span><span class="sxs-lookup"><span data-stu-id="3e720-164">Use SSH to connect to the cluster head node.</span></span> <span data-ttu-id="3e720-165">Ad esempio, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="3e720-165">For example, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

       <span data-ttu-id="3e720-166">Per altre informazioni sull'uso di SSH, vedere [Connettersi a HDInsight (Hadoop) con SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="3e720-166">For more information on using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

   2. <span data-ttu-id="3e720-167">Utilizzare il comando seguente per ottenere il nome host completo:</span><span class="sxs-lookup"><span data-stu-id="3e720-167">Use the following command to get the fully qualified hostname:</span></span>

        ```bash
        hostname -f
        ```

        <span data-ttu-id="3e720-168">Il comando restituisce un valore simile al nome host seguente:</span><span class="sxs-lookup"><span data-stu-id="3e720-168">This command returns a value similar to the following host name:</span></span>

            hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

        <span data-ttu-id="3e720-169">Salvare il valore restituito, poiché verrà usato in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="3e720-169">Save the value returned, as it is used later.</span></span>

2. <span data-ttu-id="3e720-170">Nel browser connettersi a **http://NOMEHOST:8983/solr/#/**, dove **NOMEHOST** è il nome stabilito nei passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="3e720-170">In your browser, connect to **http://HOSTNAME:8983/solr/#/**, where **HOSTNAME** is the name you determined in the previous steps.</span></span>

    <span data-ttu-id="3e720-171">La richiesta viene instradata attraverso il tunnel SSH all'interfaccia utente Web di Solr nel cluster.</span><span class="sxs-lookup"><span data-stu-id="3e720-171">The request is routed through the SSH tunnel to the Solr web UI on your cluster.</span></span> <span data-ttu-id="3e720-172">La pagina appare simile alla seguente immagine:</span><span class="sxs-lookup"><span data-stu-id="3e720-172">The page appears similar to the following image:</span></span>

    ![Immagine del dashboard di Solr](./media/hdinsight-hadoop-solr-install-linux/solrdashboard.png)

3. <span data-ttu-id="3e720-174">Nel riquadro sinistro selezionare **collection1** nell'elenco a discesa **Core Selector** (Selettore base).</span><span class="sxs-lookup"><span data-stu-id="3e720-174">From the left pane, use the **Core Selector** drop-down to select **collection1**.</span></span> <span data-ttu-id="3e720-175">Sotto **collection1** dovrebbero essere visualizzate diverse voci.</span><span class="sxs-lookup"><span data-stu-id="3e720-175">Several entries should them appear below **collection1**.</span></span>

4. <span data-ttu-id="3e720-176">Nelle voci elencate sotto **collection1** selezionare **Query**.</span><span class="sxs-lookup"><span data-stu-id="3e720-176">From the entries below **collection1**, select **Query**.</span></span> <span data-ttu-id="3e720-177">Usare i valori seguenti per popolare la pagina di ricerca:</span><span class="sxs-lookup"><span data-stu-id="3e720-177">Use the following values to populate the search page:</span></span>

   * <span data-ttu-id="3e720-178">Nella casella di testo **q** immettere **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="3e720-178">In the **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="3e720-179">Verranno restituiti dalla query tutti i documenti indicizzati in Solr.</span><span class="sxs-lookup"><span data-stu-id="3e720-179">This query returns all the documents that are indexed in Solr.</span></span> <span data-ttu-id="3e720-180">Per cercare una stringa specifica nei documenti, è possibile immettere qui la stringa.</span><span class="sxs-lookup"><span data-stu-id="3e720-180">If you want to search for a specific string within the documents, you can enter that string here.</span></span>
   * <span data-ttu-id="3e720-181">Selezionare il formato di output nella casella di testo **wt** .</span><span class="sxs-lookup"><span data-stu-id="3e720-181">In the **wt** text box, select the output format.</span></span> <span data-ttu-id="3e720-182">Il valore predefinito è **json**.</span><span class="sxs-lookup"><span data-stu-id="3e720-182">Default is **json**.</span></span>

     <span data-ttu-id="3e720-183">Selezionare infine il pulsante **Execute Query** in basso nella pagina di ricerca.</span><span class="sxs-lookup"><span data-stu-id="3e720-183">Finally, select the **Execute Query** button at the bottom of the search pate.</span></span>

     ![Usare l'azione script per personalizzare un cluster](./media/hdinsight-hadoop-solr-install-linux/hdi-solr-dashboard-query.png)

     <span data-ttu-id="3e720-185">L'output restituisce i due documenti che sono stati aggiunti all'indice in precedenza.</span><span class="sxs-lookup"><span data-stu-id="3e720-185">The output returns the two documents that you added to the index earlier.</span></span> <span data-ttu-id="3e720-186">L'output è simile al seguente documento JSON:</span><span class="sxs-lookup"><span data-stu-id="3e720-186">The output is similar to the following JSON document:</span></span>

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, the Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication to other Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over the e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }

### <a name="starting-and-stopping-solr"></a><span data-ttu-id="3e720-187">Avviare e arrestare Solr</span><span class="sxs-lookup"><span data-stu-id="3e720-187">Starting and stopping Solr</span></span>

<span data-ttu-id="3e720-188">Per arrestare o avviare Solr manualmente, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3e720-188">Use the following commands to manually stop and start Solr:</span></span>

```bash
sudo stop solr
sudo start solr
```

## <a name="backup-indexed-data"></a><span data-ttu-id="3e720-189">Eseguire il backup dei dati indicizzati</span><span class="sxs-lookup"><span data-stu-id="3e720-189">Backup indexed data</span></span>

<span data-ttu-id="3e720-190">Per eseguire il backup dei dati Solr nell'archivio predefinito per il cluster, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="3e720-190">Use the following steps to back up Solr data to the default storage for your cluster:</span></span>

1. <span data-ttu-id="3e720-191">Connettersi al cluster tramite SSH, quindi usare il comando seguente per ottenere il nome host per il nodo head:</span><span class="sxs-lookup"><span data-stu-id="3e720-191">Connect to the cluster using SSH, then use the following command to get the host name for the head node:</span></span>

    ```bash
    hostname -f
    ```

2. <span data-ttu-id="3e720-192">Per creare uno snapshot dei dati indicizzati, usare il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="3e720-192">Use the following command to create a snapshot of the indexed data.</span></span> <span data-ttu-id="3e720-193">Sostituire **HOSTNAME** con il nome restituito dal comando precedente:</span><span class="sxs-lookup"><span data-stu-id="3e720-193">Replace **HOSTNAME** with the name returned from the previous command:</span></span>

    ```bash
    curl http://HOSTNAME:8983/solr/replication?command=backup
    ```

    <span data-ttu-id="3e720-194">La risposta restituita è simile al codice XML seguente:</span><span class="sxs-lookup"><span data-stu-id="3e720-194">The response is similar to the following XML:</span></span>

        <?xml version="1.0" encoding="UTF-8"?>
        <response>
          <lst name="responseHeader">
            <int name="status">0</int>
            <int name="QTime">9</int>
          </lst>
          <str name="status">OK</str>
        </response>

3. <span data-ttu-id="3e720-195">Passare le directory a `/usr/hdp/current/solr/example/solr`.</span><span class="sxs-lookup"><span data-stu-id="3e720-195">Change directories to `/usr/hdp/current/solr/example/solr`.</span></span> <span data-ttu-id="3e720-196">Per ogni raccolta è presente una sottodirectory.</span><span class="sxs-lookup"><span data-stu-id="3e720-196">There is a subdirectory here for each collection.</span></span> <span data-ttu-id="3e720-197">Ogni directory di una raccolta contiene una directory `data` che contiene lo snapshot per la raccolta.</span><span class="sxs-lookup"><span data-stu-id="3e720-197">Each collection directory contains a `data` directory that contains the snapshot for the collection.</span></span>

4. <span data-ttu-id="3e720-198">Per creare un archivio compresso della cartella dello snapshot, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3e720-198">To create a compressed archive of the snapshot folder, use the following command:</span></span>

    ```bash
    tar -zcf snapshot.20150806185338855.tgz snapshot.20150806185338855
    ```

    <span data-ttu-id="3e720-199">Sostituire i valori `snapshot.20150806185338855` con il nome dello snapshot per la raccolta.</span><span class="sxs-lookup"><span data-stu-id="3e720-199">Replace the `snapshot.20150806185338855` values with the name of the snapshot for your collection.</span></span>

    <span data-ttu-id="3e720-200">Viene così creato un nuovo archivio denominato **snapshot.20150806185338855.tgz** che include il contenuto della directory **snapshot.20150806185338855**.</span><span class="sxs-lookup"><span data-stu-id="3e720-200">This command creates an archive named **snapshot.20150806185338855.tgz**, which contains the contents of the **snapshot.20150806185338855** directory.</span></span>

5. <span data-ttu-id="3e720-201">Si potrà quindi inserire l'archivio nella risorsa di archiviazione primaria del cluster usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3e720-201">You can then store the archive to the cluster's primary storage using the following command:</span></span>

    ```bash
    hdfs dfs -put snapshot.20150806185338855.tgz /example/data
    ```

<span data-ttu-id="3e720-202">Per altre informazioni sulle operazioni di backup e ripristino di Solr, vedere [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span><span class="sxs-lookup"><span data-stu-id="3e720-202">For more information on working with Solr backup and restores, see [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e720-203">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3e720-203">Next steps</span></span>

* <span data-ttu-id="3e720-204">[Installare Giraph in cluster HDInsight](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="3e720-204">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="3e720-205">Usare la personalizzazione cluster per installare Giraph in cluster Hadoop di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3e720-205">Use cluster customization to install Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="3e720-206">Giraph permette di elaborare grafici con Hadoop e può essere usato con Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3e720-206">Giraph allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="3e720-207">[Installare Hue nei cluster HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="3e720-207">[Install Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="3e720-208">Usare la personalizzazione dei cluster per installare Hue nei cluster Hadoop di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3e720-208">Use cluster customization to install Hue on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="3e720-209">Hue è un insieme di applicazioni Web che consente di interagire con un cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="3e720-209">Hue is a set of Web applications used to interact with a Hadoop cluster.</span></span>

[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
