---
title: aaaUse genera Script azione tooinstall Solr in HDInsight basati su Linux - Azure | Documenti Microsoft
description: Informazioni su come i cluster usando le azioni Script tooinstall Solr in HDInsight Hadoop basati su Linux.
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
ms.openlocfilehash: 4c179032b95ae187f1830d8927f8796372fa8ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="f4c48-103">Installare e usare Solr nei cluster Hadoop di HDInsight</span><span class="sxs-lookup"><span data-stu-id="f4c48-103">Install and use Solr on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="f4c48-104">Informazioni su come tooinstall Solr in Azure HDInsight utilizzando l'azione di Script.</span><span class="sxs-lookup"><span data-stu-id="f4c48-104">Learn how tooinstall Solr on Azure HDInsight by using Script Action.</span></span> <span data-ttu-id="f4c48-105">Solr è una piattaforma di ricerca avanzata e offre funzionalità di ricerca di livello aziendale per i dati gestiti da Hadoop.</span><span class="sxs-lookup"><span data-stu-id="f4c48-105">Solr is a powerful search platform and provides enterprise-level search capabilities on data managed by Hadoop.</span></span>

> [!IMPORTANT]
    > <span data-ttu-id="f4c48-106">passaggi di Hello in questo documento richiedono un cluster HDInsight che utilizza Linux.</span><span class="sxs-lookup"><span data-stu-id="f4c48-106">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="f4c48-107">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="f4c48-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f4c48-108">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="f4c48-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f4c48-109">script di esempio Hello utilizzato in questo documento viene installato 4.9 Solr con una configurazione specifica.</span><span class="sxs-lookup"><span data-stu-id="f4c48-109">hello sample script used in this document installs Solr 4.9 with a specific configuration.</span></span> <span data-ttu-id="f4c48-110">Se si desidera che tooconfigure hello Solr cluster con raccolte diverse, le partizioni, schemi, le repliche, e così via, è necessario modificare script hello e file binari di Solr.</span><span class="sxs-lookup"><span data-stu-id="f4c48-110">If you want tooconfigure hello Solr cluster with different collections, shards, schemas, replicas, etc., you must modify hello script and Solr binaries.</span></span>

## <span data-ttu-id="f4c48-111"><a name="whatis"></a>Che cos'è Solr</span><span class="sxs-lookup"><span data-stu-id="f4c48-111"><a name="whatis"></a>What is Solr</span></span>

<span data-ttu-id="f4c48-112">[Apache Solr](http://lucene.apache.org/solr/features.html) è una piattaforma di ricerca aziendale che permette di eseguire ricerche full-text avanzate sui dati.</span><span class="sxs-lookup"><span data-stu-id="f4c48-112">[Apache Solr](http://lucene.apache.org/solr/features.html) is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="f4c48-113">Mentre Hadoop consente di archiviare e gestire grandi quantità di dati, Solr Apache fornisce funzionalità di ricerca di hello tooquickly recuperare i dati hello.</span><span class="sxs-lookup"><span data-stu-id="f4c48-113">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides hello search capabilities tooquickly retrieve hello data.</span></span>

> [!WARNING]
> <span data-ttu-id="f4c48-114">I componenti forniti con i cluster di HDInsight hello sono completamente supportati da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f4c48-114">Components provided with hello HDInsight cluster are fully supported by Microsoft.</span></span>
>
> <span data-ttu-id="f4c48-115">I componenti personalizzati, ad esempio Solr, ricevano supporto commercialmente ragionevole toohelp toofurther per risolvere il problema di hello.</span><span class="sxs-lookup"><span data-stu-id="f4c48-115">Custom components, such as Solr, receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="f4c48-116">Supporto tecnico Microsoft potrebbe non essere in grado di tooresolve problemi con componenti personalizzati.</span><span class="sxs-lookup"><span data-stu-id="f4c48-116">Microsoft support may not be able tooresolve problems with custom components.</span></span> <span data-ttu-id="f4c48-117">Community di origine aprire hello tooengage potrebbe essere necessario per ottenere assistenza.</span><span class="sxs-lookup"><span data-stu-id="f4c48-117">You may need tooengage hello open source communities for assistance.</span></span> <span data-ttu-id="f4c48-118">È ad esempio possibile ricorrere a molti siti di community, come il [forum MSDN per HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight) o [http://stackoverflow.com](http://stackoverflow.com). Anche per i progetti Apache sono disponibili siti specifici in [http://apache.org](http://apache.org), ad esempio [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="f4c48-118">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

## <a name="what-hello-script-does"></a><span data-ttu-id="f4c48-119">Quali script hello esegue</span><span class="sxs-lookup"><span data-stu-id="f4c48-119">What hello script does</span></span>

<span data-ttu-id="f4c48-120">Questo script esegue hello cluster di HDInsight toohello le modifiche seguenti:</span><span class="sxs-lookup"><span data-stu-id="f4c48-120">This script makes hello following changes toohello HDInsight cluster:</span></span>

* <span data-ttu-id="f4c48-121">Installa Solr 4.9 in `/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="f4c48-121">Installs Solr 4.9 into `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="f4c48-122">Crea un utente, **solrusr**, ovvero hello toorun utilizzati Solr servizio</span><span class="sxs-lookup"><span data-stu-id="f4c48-122">Creates a user, **solrusr**, which is used toorun hello Solr service</span></span>
* <span data-ttu-id="f4c48-123">Set **solruser** come proprietario di hello di`/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="f4c48-123">Sets **solruser** as hello owner of `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="f4c48-124">Aggiunge una configurazione [Upstart](http://upstart.ubuntu.com/) che avvia automaticamente Solr.</span><span class="sxs-lookup"><span data-stu-id="f4c48-124">Adds an [Upstart](http://upstart.ubuntu.com/) configuration that starts Solr automatically.</span></span>

## <span data-ttu-id="f4c48-125"><a name="install"></a>Installare R mediante azioni script</span><span class="sxs-lookup"><span data-stu-id="f4c48-125"><a name="install"></a>Install Solr using Script Actions</span></span>

<span data-ttu-id="f4c48-126">Un tooinstall di script di esempio Solr in un cluster HDInsight è disponibile in hello seguente posizione:</span><span class="sxs-lookup"><span data-stu-id="f4c48-126">A sample script tooinstall Solr on an HDInsight cluster is available at hello following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh

<span data-ttu-id="f4c48-127">toocreate un cluster con Solr installato, utilizzare hello passaggi hello [cluster HDInsight creare](hdinsight-hadoop-create-linux-clusters-portal.md) documento.</span><span class="sxs-lookup"><span data-stu-id="f4c48-127">toocreate a cluster that has Solr installed, use hello steps in hello [Create HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md) document.</span></span> <span data-ttu-id="f4c48-128">Durante il processo di creazione di hello, utilizzare hello seguendo i passaggi tooinstall Solr:</span><span class="sxs-lookup"><span data-stu-id="f4c48-128">During hello creation process, use hello following steps tooinstall Solr:</span></span>

1. <span data-ttu-id="f4c48-129">Da hello __riepilogo Cluster__ blade, settings__ select__Advanced, __Script azioni__.</span><span class="sxs-lookup"><span data-stu-id="f4c48-129">From hello __Cluster summary__ blade, select__Advanced settings__, then __Script actions__.</span></span> <span data-ttu-id="f4c48-130">Utilizzare hello modulo hello toopopulate di informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f4c48-130">Use hello following information toopopulate hello form:</span></span>

   * <span data-ttu-id="f4c48-131">**NOME**: immettere un nome descrittivo per l'azione script hello.</span><span class="sxs-lookup"><span data-stu-id="f4c48-131">**NAME**: Enter a friendly name for hello script action.</span></span>
   * <span data-ttu-id="f4c48-132">**URI SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="f4c48-132">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span></span>
   * <span data-ttu-id="f4c48-133">**HEAD**: selezionare questa opzione</span><span class="sxs-lookup"><span data-stu-id="f4c48-133">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="f4c48-134">**RUOLO DI LAVORO**: selezionare questa opzione</span><span class="sxs-lookup"><span data-stu-id="f4c48-134">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="f4c48-135">**ZOOKEEPER**: selezionare questa opzione tooinstall nel nodo Zookeeper hello</span><span class="sxs-lookup"><span data-stu-id="f4c48-135">**ZOOKEEPER**: Check this option tooinstall on hello Zookeeper node</span></span>
   * <span data-ttu-id="f4c48-136">**PARAMETRI**: lasciare questo campo vuoto</span><span class="sxs-lookup"><span data-stu-id="f4c48-136">**PARAMETERS**: Leave this field blank</span></span>

2. <span data-ttu-id="f4c48-137">Nella parte inferiore di hello di hello **Script azioni** blade, utilizzare hello **selezionare** configurazione hello toosave dei pulsanti.</span><span class="sxs-lookup"><span data-stu-id="f4c48-137">At hello bottom of hello **Script actions** blade, use hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="f4c48-138">Infine, utilizzare hello **Avanti** pulsante tooreturn toohello __riepilogo di Cluster__</span><span class="sxs-lookup"><span data-stu-id="f4c48-138">Finally, use hello **Next** button tooreturn toohello __Cluster summary__</span></span>

3. <span data-ttu-id="f4c48-139">Da hello __riepilogo Cluster__ selezionare __crea__ cluster hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="f4c48-139">From hello __Cluster summary__ page, select __Create__ toocreate hello cluster.</span></span>

## <span data-ttu-id="f4c48-140"><a name="usesolr"></a>Come si usa Solr in HDInsight</span><span class="sxs-lookup"><span data-stu-id="f4c48-140"><a name="usesolr"></a>How do I use Solr in HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f4c48-141">passaggi di Hello in questa sezione illustrano le funzionalità di base Solr.</span><span class="sxs-lookup"><span data-stu-id="f4c48-141">hello steps in this section demonstrate basic Solr functionality.</span></span> <span data-ttu-id="f4c48-142">Per ulteriori informazioni sull'utilizzo di Solr, vedere hello [Solr Apache sito](http://lucene.apache.org/solr/).</span><span class="sxs-lookup"><span data-stu-id="f4c48-142">For more information on using Solr, see hello [Apache Solr site](http://lucene.apache.org/solr/).</span></span>

### <a name="index-data"></a><span data-ttu-id="f4c48-143">Dati dell'indice</span><span class="sxs-lookup"><span data-stu-id="f4c48-143">Index data</span></span>

<span data-ttu-id="f4c48-144">Utilizzare i seguenti passaggi tooadd esempio dati tooSolr hello e quindi eseguire una query:</span><span class="sxs-lookup"><span data-stu-id="f4c48-144">Use hello following steps tooadd example data tooSolr, and then query it:</span></span>

1. <span data-ttu-id="f4c48-145">Connettere il cluster di HDInsight toohello tramite SSH:</span><span class="sxs-lookup"><span data-stu-id="f4c48-145">Connect toohello HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="f4c48-146">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f4c48-146">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="f4c48-147">Passaggi più avanti in questo documento usano un SSL tunnel tooconnect toohello Solr interfaccia utente web.</span><span class="sxs-lookup"><span data-stu-id="f4c48-147">Steps later in this document use an SSL tunnel tooconnect toohello Solr web UI.</span></span> <span data-ttu-id="f4c48-148">toouse questi passaggi, è necessario stabilire un SSL tunnel e quindi configurare toouse il browser è.</span><span class="sxs-lookup"><span data-stu-id="f4c48-148">toouse these steps, you must establish an SSL tunnel and then configure your browser toouse it.</span></span>
     >
     > <span data-ttu-id="f4c48-149">Per ulteriori informazioni, vedere hello [usare SSH Tunneling con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) documento.</span><span class="sxs-lookup"><span data-stu-id="f4c48-149">For more information, see hello [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="f4c48-150">Utilizzare hello dati di esempio dell'indice Solr toohave i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f4c48-150">Use hello following commands toohave Solr index sample data:</span></span>

    ```bash
    cd /usr/hdp/current/solr/example/exampledocs
    java -jar post.jar solr.xml monitor.xml
    ```

    <span data-ttu-id="f4c48-151">Hello output seguente viene restituito toohello console:</span><span class="sxs-lookup"><span data-stu-id="f4c48-151">hello following output is returned toohello console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="f4c48-152">Hello `post.jar` utilità aggiunge hello **solr.xml** e **monitor.xml** indice toohello documenti.</span><span class="sxs-lookup"><span data-stu-id="f4c48-152">hello `post.jar` utility adds hello **solr.xml** and **monitor.xml** documents toohello index.</span></span>
  
3. <span data-ttu-id="f4c48-153">Utilizzare hello comando tooquery hello Solr REST API seguenti:</span><span class="sxs-lookup"><span data-stu-id="f4c48-153">Use hello following command tooquery hello Solr REST API:</span></span>

    ```bash
    curl "http://localhost:8983/solr/collection1/select?q=*%3A*&wt=json&indent=true"
    ```

    <span data-ttu-id="f4c48-154">Questo comando Cerca **collection1** per tutti i documenti corrispondenti  **\*:\***  (codificato come \*% 3A\* nella stringa di query hello).</span><span class="sxs-lookup"><span data-stu-id="f4c48-154">This command searches **collection1** for any documents matching **\*:\*** (encoded as \*%3A\* in hello query string).</span></span> <span data-ttu-id="f4c48-155">Hello seguente documento JSON è un esempio di risposta hello:</span><span class="sxs-lookup"><span data-stu-id="f4c48-155">hello following JSON document is an example of hello response:</span></span>

            "response": {
                "numFound": 2,
                "start": 0,
                "maxScore": 1,
                "docs": [
                  {
                    "id": "SOLR1000",
                    "name": "Solr, hello Enterprise Search Server",
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
                      "Scalability - Efficient Replication tooother Solr Search Servers",
                      "Flexible and Adaptable with XML configuration and Schema",
                      "Good unicode support: héllo (hello with an accent over hello e)"
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

### <a name="using-hello-solr-dashboard"></a><span data-ttu-id="f4c48-156">Tramite il dashboard di Solr hello</span><span class="sxs-lookup"><span data-stu-id="f4c48-156">Using hello Solr dashboard</span></span>

<span data-ttu-id="f4c48-157">dashboard Solr Hello è un'interfaccia utente che consente di toowork con Solr attraverso il web browser web.</span><span class="sxs-lookup"><span data-stu-id="f4c48-157">hello Solr dashboard is a web UI that allows you toowork with Solr through your web browser.</span></span> <span data-ttu-id="f4c48-158">dashboard Solr Hello non è esposta direttamente su Internet di hello dal cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f4c48-158">hello Solr dashboard is not exposed directly on hello Internet from your HDInsight cluster.</span></span> <span data-ttu-id="f4c48-159">È possibile utilizzare un tooaccess tunnel SSH è.</span><span class="sxs-lookup"><span data-stu-id="f4c48-159">You can use an SSH tunnel tooaccess it.</span></span> <span data-ttu-id="f4c48-160">Per ulteriori informazioni sull'utilizzo di un tunnel SSH, vedere hello [usare SSH Tunneling con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) documento.</span><span class="sxs-lookup"><span data-stu-id="f4c48-160">For more information on using an SSH tunnel, see hello [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="f4c48-161">Dopo aver stabilito un tunnel SSH, utilizzare hello dashboard Solr hello toouse di passaggi seguente:</span><span class="sxs-lookup"><span data-stu-id="f4c48-161">Once you have established an SSH tunnel, use hello following steps toouse hello Solr dashboard:</span></span>

1. <span data-ttu-id="f4c48-162">Determinare il nome host hello per nodo head primario hello:</span><span class="sxs-lookup"><span data-stu-id="f4c48-162">Determine hello host name for hello primary headnode:</span></span>

   1. <span data-ttu-id="f4c48-163">Usare SSH tooconnect toohello nodo head del cluster.</span><span class="sxs-lookup"><span data-stu-id="f4c48-163">Use SSH tooconnect toohello cluster head node.</span></span> <span data-ttu-id="f4c48-164">ad esempio `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="f4c48-164">For example, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

       <span data-ttu-id="f4c48-165">Per ulteriori informazioni sull'utilizzo di SSH, vedere hello [utilizzo di SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f4c48-165">For more information on using SSH, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

   2. <span data-ttu-id="f4c48-166">Utilizzare hello comando tooget hello nome host completo seguente:</span><span class="sxs-lookup"><span data-stu-id="f4c48-166">Use hello following command tooget hello fully qualified hostname:</span></span>

        ```bash
        hostname -f
        ```

        <span data-ttu-id="f4c48-167">Questo comando restituisce un toohello simile valore dopo il nome host:</span><span class="sxs-lookup"><span data-stu-id="f4c48-167">This command returns a value similar toohello following host name:</span></span>

            hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

        <span data-ttu-id="f4c48-168">Salvare il valore di hello restituito, perché è usato in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="f4c48-168">Save hello value returned, as it is used later.</span></span>

2. <span data-ttu-id="f4c48-169">Nel browser, connettersi troppo**http://HOSTNAME:8983/solr / #/**, dove **HOSTNAME** nome hello è determinato nei passaggi precedenti hello.</span><span class="sxs-lookup"><span data-stu-id="f4c48-169">In your browser, connect too**http://HOSTNAME:8983/solr/#/**, where **HOSTNAME** is hello name you determined in hello previous steps.</span></span>

    <span data-ttu-id="f4c48-170">Hello richiesta è instradata tramite hello SSH tunnel toohello Solr interfaccia utente web sul cluster.</span><span class="sxs-lookup"><span data-stu-id="f4c48-170">hello request is routed through hello SSH tunnel toohello Solr web UI on your cluster.</span></span> <span data-ttu-id="f4c48-171">verrà visualizzata la pagina di Hello simile toohello seguente immagine:</span><span class="sxs-lookup"><span data-stu-id="f4c48-171">hello page appears similar toohello following image:</span></span>

    ![Immagine del dashboard di Solr](./media/hdinsight-hadoop-solr-install-linux/solrdashboard.png)

3. <span data-ttu-id="f4c48-173">Nel riquadro di sinistra hello, utilizzare hello **selettore Core** elenco a discesa tooselect **collection1**.</span><span class="sxs-lookup"><span data-stu-id="f4c48-173">From hello left pane, use hello **Core Selector** drop-down tooselect **collection1**.</span></span> <span data-ttu-id="f4c48-174">Sotto **collection1** dovrebbero essere visualizzate diverse voci.</span><span class="sxs-lookup"><span data-stu-id="f4c48-174">Several entries should them appear below **collection1**.</span></span>

4. <span data-ttu-id="f4c48-175">Le voci di hello seguente **collection1**selezionare **Query**.</span><span class="sxs-lookup"><span data-stu-id="f4c48-175">From hello entries below **collection1**, select **Query**.</span></span> <span data-ttu-id="f4c48-176">Utilizzare hello seguente pagina di ricerca di valori toopopulate hello:</span><span class="sxs-lookup"><span data-stu-id="f4c48-176">Use hello following values toopopulate hello search page:</span></span>

   * <span data-ttu-id="f4c48-177">In hello **q** testo immettere  **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="f4c48-177">In hello **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="f4c48-178">Questa query restituisce tutti i documenti indicizzati hello in Solr.</span><span class="sxs-lookup"><span data-stu-id="f4c48-178">This query returns all hello documents that are indexed in Solr.</span></span> <span data-ttu-id="f4c48-179">Se si desidera toosearch una stringa specifica all'interno dei documenti hello, è possibile immettere qui la stringa.</span><span class="sxs-lookup"><span data-stu-id="f4c48-179">If you want toosearch for a specific string within hello documents, you can enter that string here.</span></span>
   * <span data-ttu-id="f4c48-180">In hello **wt** casella di testo, il formato di output di hello selezionare.</span><span class="sxs-lookup"><span data-stu-id="f4c48-180">In hello **wt** text box, select hello output format.</span></span> <span data-ttu-id="f4c48-181">Il valore predefinito è **json**.</span><span class="sxs-lookup"><span data-stu-id="f4c48-181">Default is **json**.</span></span>

     <span data-ttu-id="f4c48-182">Infine, selezionare hello **Esegui Query** pulsante nella parte inferiore di hello del pate ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="f4c48-182">Finally, select hello **Execute Query** button at hello bottom of hello search pate.</span></span>

     ![Utilizzare l'azione Script toocustomize un cluster](./media/hdinsight-hadoop-solr-install-linux/hdi-solr-dashboard-query.png)

     <span data-ttu-id="f4c48-184">output di Hello restituisce hello due documenti aggiunti toohello indicizzare in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f4c48-184">hello output returns hello two documents that you added toohello index earlier.</span></span> <span data-ttu-id="f4c48-185">l'output è simile toohello seguente documento JSON Hello:</span><span class="sxs-lookup"><span data-stu-id="f4c48-185">hello output is similar toohello following JSON document:</span></span>

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
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
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
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

### <a name="starting-and-stopping-solr"></a><span data-ttu-id="f4c48-186">Avviare e arrestare Solr</span><span class="sxs-lookup"><span data-stu-id="f4c48-186">Starting and stopping Solr</span></span>

<span data-ttu-id="f4c48-187">Utilizzare i seguenti comandi toomanually arrestare e avviare Solr hello:</span><span class="sxs-lookup"><span data-stu-id="f4c48-187">Use hello following commands toomanually stop and start Solr:</span></span>

```bash
sudo stop solr
sudo start solr
```

## <a name="backup-indexed-data"></a><span data-ttu-id="f4c48-188">Eseguire il backup dei dati indicizzati</span><span class="sxs-lookup"><span data-stu-id="f4c48-188">Backup indexed data</span></span>

<span data-ttu-id="f4c48-189">Utilizzare hello seguendo i passaggi tooback backup Solr dati toohello spazio di archiviazione predefinito per il cluster:</span><span class="sxs-lookup"><span data-stu-id="f4c48-189">Use hello following steps tooback up Solr data toohello default storage for your cluster:</span></span>

1. <span data-ttu-id="f4c48-190">Connettere il cluster toohello tramite SSH, quindi utilizzare hello dopo il nome di comando tooget hello host per il nodo head hello:</span><span class="sxs-lookup"><span data-stu-id="f4c48-190">Connect toohello cluster using SSH, then use hello following command tooget hello host name for hello head node:</span></span>

    ```bash
    hostname -f
    ```

2. <span data-ttu-id="f4c48-191">Utilizzare hello successivo comando toocreate uno snapshot dei dati indicizzato hello.</span><span class="sxs-lookup"><span data-stu-id="f4c48-191">Use hello following command toocreate a snapshot of hello indexed data.</span></span> <span data-ttu-id="f4c48-192">Sostituire **HOSTNAME** con nome hello restituito dal comando precedente hello:</span><span class="sxs-lookup"><span data-stu-id="f4c48-192">Replace **HOSTNAME** with hello name returned from hello previous command:</span></span>

    ```bash
    curl http://HOSTNAME:8983/solr/replication?command=backup
    ```

    <span data-ttu-id="f4c48-193">risposta Hello è simile toohello XML seguente:</span><span class="sxs-lookup"><span data-stu-id="f4c48-193">hello response is similar toohello following XML:</span></span>

        <?xml version="1.0" encoding="UTF-8"?>
        <response>
          <lst name="responseHeader">
            <int name="status">0</int>
            <int name="QTime">9</int>
          </lst>
          <str name="status">OK</str>
        </response>

3. <span data-ttu-id="f4c48-194">Passare alla directory troppo`/usr/hdp/current/solr/example/solr`.</span><span class="sxs-lookup"><span data-stu-id="f4c48-194">Change directories too`/usr/hdp/current/solr/example/solr`.</span></span> <span data-ttu-id="f4c48-195">Per ogni raccolta è presente una sottodirectory.</span><span class="sxs-lookup"><span data-stu-id="f4c48-195">There is a subdirectory here for each collection.</span></span> <span data-ttu-id="f4c48-196">Ogni raccolta di directory contiene un `data` directory che contiene snapshot hello per la raccolta di hello.</span><span class="sxs-lookup"><span data-stu-id="f4c48-196">Each collection directory contains a `data` directory that contains hello snapshot for hello collection.</span></span>

4. <span data-ttu-id="f4c48-197">toocreate un archivio compresso della cartella snapshot hello, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f4c48-197">toocreate a compressed archive of hello snapshot folder, use hello following command:</span></span>

    ```bash
    tar -zcf snapshot.20150806185338855.tgz snapshot.20150806185338855
    ```

    <span data-ttu-id="f4c48-198">Sostituire hello `snapshot.20150806185338855` valori con nome hello dello snapshot hello per la raccolta.</span><span class="sxs-lookup"><span data-stu-id="f4c48-198">Replace hello `snapshot.20150806185338855` values with hello name of hello snapshot for your collection.</span></span>

    <span data-ttu-id="f4c48-199">Questo comando crea un archivio denominato **snapshot.20150806185338855.tgz**, che contiene il contenuto di hello di hello **snapshot.20150806185338855** directory.</span><span class="sxs-lookup"><span data-stu-id="f4c48-199">This command creates an archive named **snapshot.20150806185338855.tgz**, which contains hello contents of hello **snapshot.20150806185338855** directory.</span></span>

5. <span data-ttu-id="f4c48-200">È quindi possibile archiviare archiviazione primaria di hello archivio toohello cluster utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f4c48-200">You can then store hello archive toohello cluster's primary storage using hello following command:</span></span>

    ```bash
    hdfs dfs -put snapshot.20150806185338855.tgz /example/data
    ```

<span data-ttu-id="f4c48-201">Per altre informazioni sulle operazioni di backup e ripristino di Solr, vedere [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span><span class="sxs-lookup"><span data-stu-id="f4c48-201">For more information on working with Solr backup and restores, see [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4c48-202">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f4c48-202">Next steps</span></span>

* <span data-ttu-id="f4c48-203">[Installare Giraph in cluster HDInsight](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f4c48-203">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="f4c48-204">Utilizzare cluster personalizzazione tooinstall che cluster Giraph in HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="f4c48-204">Use cluster customization tooinstall Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="f4c48-205">Giraph consente grafico tooperform elaborazione tramite Hadoop e può essere utilizzato con Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f4c48-205">Giraph allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="f4c48-206">[Installare Hue nei cluster HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f4c48-206">[Install Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="f4c48-207">Utilizzare cluster personalizzazione tooinstall tonalità nei cluster HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="f4c48-207">Use cluster customization tooinstall Hue on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="f4c48-208">La tonalità corrisponde che toointeract utilizzato da un set di applicazioni Web con un cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="f4c48-208">Hue is a set of Web applications used toointeract with a Hadoop cluster.</span></span>

[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
