---
title: aaaUse genera Script azione tooinstall Solr nel cluster Hadoop - Azure | Documenti Microsoft
description: Informazioni su come cluster di HDInsight toocustomize con Solr mediante l'azione di Script.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b1e6f338-8ac1-4b38-bbb5-2f7388b9de3b
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 022ba56b7499390a91bfe869e5069893e56b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="b07e3-103">Installare e usare Solr nei cluster HDInsight basati su Windows</span><span class="sxs-lookup"><span data-stu-id="b07e3-103">Install and use Solr on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="b07e3-104">Informazioni su come toocustomize HDInsight basati su Windows cluster con Solr mediante l'azione di Script e come toouse Solr toosearch dati.</span><span class="sxs-lookup"><span data-stu-id="b07e3-104">Learn how toocustomize Windows-based HDInsight cluster with Solr using Script Action, and how toouse Solr toosearch data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b07e3-105">Hello passaggi di questa operazione solo documenti con i cluster HDInsight basati su Windows.</span><span class="sxs-lookup"><span data-stu-id="b07e3-105">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="b07e3-106">HDInsight è disponibile in Windows solo per le versioni precedenti a HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="b07e3-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="b07e3-107">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="b07e3-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b07e3-108">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="b07e3-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="b07e3-109">Per informazioni sull'uso di Solr con un cluster basato su Linux, vedere [Installare e usare Solr nei cluster Hadoop HDInsight (Linux)](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b07e3-109">For information on using Solr with a Linux-based cluster, see [Install and use Solr on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-solr-install-linux.md).</span></span>


<span data-ttu-id="b07e3-110">È possibile installare Solr in qualsiasi tipo di cluster (Hadoop, Storm, HBase, Spark) su Azure HDInsight usando *Script azione*.</span><span class="sxs-lookup"><span data-stu-id="b07e3-110">You can install Solr on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="b07e3-111">Un tooinstall di script di esempio Solr in un cluster HDInsight è disponibile da un blob di archiviazione di Azure di sola lettura in [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="b07e3-111">A sample script tooinstall Solr on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

<span data-ttu-id="b07e3-112">script di esempio Hello funziona solo con versione 3.1 del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b07e3-112">hello sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="b07e3-113">Per altre informazioni sulle versioni dei cluster HDInsight, vedere [Versioni cluster HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="b07e3-113">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="b07e3-114">script di esempio Hello utilizzato in questo argomento crea un cluster basato su Windows Solr con una configurazione specifica.</span><span class="sxs-lookup"><span data-stu-id="b07e3-114">hello sample script used in this topic creates a Windows-based Solr cluster with a specific configuration.</span></span> <span data-ttu-id="b07e3-115">Se si desidera che tooconfigure hello Solr cluster con raccolte diverse, le partizioni, schemi, le repliche, e così via, è necessario modificare di conseguenza script hello e file binari di Solr.</span><span class="sxs-lookup"><span data-stu-id="b07e3-115">If you want tooconfigure hello Solr cluster with different collections, shards, schemas, replicas, etc., you must modify hello script and Solr binaries accordingly.</span></span>

<span data-ttu-id="b07e3-116">**Articoli correlati**</span><span class="sxs-lookup"><span data-stu-id="b07e3-116">**Related articles**</span></span>

* [<span data-ttu-id="b07e3-117">Installare e usare Solr nei cluster Hadoop di HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="b07e3-117">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="b07e3-118">[Creare cluster Hadoop in HDInsight](hdinsight-provision-clusters.md): informazioni generali sulla creazione di cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="b07e3-118">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="b07e3-119">[Personalizzare cluster HDInsight mediante l'azione Script][hdinsight-cluster-customize]: informazioni generali sulla personalizzazione di cluster HDInsight tramite Azione script.</span><span class="sxs-lookup"><span data-stu-id="b07e3-119">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="b07e3-120">[Sviluppare script di Azione script per HDInsight](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="b07e3-120">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-solr"></a><span data-ttu-id="b07e3-121">Che cos'è Solr?</span><span class="sxs-lookup"><span data-stu-id="b07e3-121">What is Solr?</span></span>
<span data-ttu-id="b07e3-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> è una piattaforma di ricerca aziendale che permette di eseguire ricerche full-text avanzate sui dati.</span><span class="sxs-lookup"><span data-stu-id="b07e3-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="b07e3-123">Mentre Hadoop consente di archiviare e gestire grandi quantità di dati, Solr Apache fornisce funzionalità di ricerca di hello tooquickly recuperare i dati hello.</span><span class="sxs-lookup"><span data-stu-id="b07e3-123">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides hello search capabilities tooquickly retrieve hello data.</span></span>

## <a name="install-solr-using-portal"></a><span data-ttu-id="b07e3-124">Installare Solr utilizzando il portale</span><span class="sxs-lookup"><span data-stu-id="b07e3-124">Install Solr using portal</span></span>
1. <span data-ttu-id="b07e3-125">Avviare la creazione di un cluster tramite hello **creazione personalizzata** opzione, come descritto in [cluster creare Hadoop in HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="b07e3-125">Start creating a cluster by using hello **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="b07e3-126">In hello **azioni Script** pagina della procedura guidata hello, fare clic su **aggiungere script azione** tooprovide i dettagli sulla azione script hello, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b07e3-126">On hello **Script Actions** page of hello wizard, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="b07e3-127">![Utilizzare l'azione Script toocustomize un cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "toocustomize azione Script Usa un cluster")</span><span class="sxs-lookup"><span data-stu-id="b07e3-127">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="b07e3-128">Proprietà</span><span class="sxs-lookup"><span data-stu-id="b07e3-128">Property</span></span></th><th><span data-ttu-id="b07e3-129">Valore</span><span class="sxs-lookup"><span data-stu-id="b07e3-129">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="b07e3-130">Nome</span><span class="sxs-lookup"><span data-stu-id="b07e3-130">Name</span></span></td>
            <td><span data-ttu-id="b07e3-131">Specificare un nome per l'azione script hello.</span><span class="sxs-lookup"><span data-stu-id="b07e3-131">Specify a name for hello script action.</span></span> <span data-ttu-id="b07e3-132">Ad esempio, <b>Install Solr</b>.</span><span class="sxs-lookup"><span data-stu-id="b07e3-132">For example, <b>Install Solr</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="b07e3-133">URI script</span><span class="sxs-lookup"><span data-stu-id="b07e3-133">Script URI</span></span></td>
            <td><span data-ttu-id="b07e3-134">Specificare hello Uniform Resource Identifier (URI) toohello script che è richiamato toocustomize hello cluster.</span><span class="sxs-lookup"><span data-stu-id="b07e3-134">Specify hello Uniform Resource Identifier (URI) toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="b07e3-135">Ad esempio, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="b07e3-135">For example, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="b07e3-136">Tipo di nodo</span><span class="sxs-lookup"><span data-stu-id="b07e3-136">Node Type</span></span></td>
            <td><span data-ttu-id="b07e3-137">Specificare i nodi di hello in cui viene eseguito uno script di personalizzazione di hello.</span><span class="sxs-lookup"><span data-stu-id="b07e3-137">Specify hello nodes on which hello customization script is run.</span></span> <span data-ttu-id="b07e3-138">È possibile scegliere <b>Tutti i nodi</b>, <b>Solo nodi head</b> o <b>Solo nodi di lavoro</b>.</span><span class="sxs-lookup"><span data-stu-id="b07e3-138">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="b07e3-139">parameters</span><span class="sxs-lookup"><span data-stu-id="b07e3-139">Parameters</span></span></td>
            <td><span data-ttu-id="b07e3-140">Specificare i parametri di hello, se richiesti dallo script hello.</span><span class="sxs-lookup"><span data-stu-id="b07e3-140">Specify hello parameters, if required by hello script.</span></span> <span data-ttu-id="b07e3-141">Hello script tooinstall Solr non richiede alcun parametro, pertanto è possibile lasciare vuoto questo.</span><span class="sxs-lookup"><span data-stu-id="b07e3-141">hello script tooinstall Solr does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="b07e3-142">È possibile aggiungere più di uno script azione tooinstall più componenti nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b07e3-142">You can add more than one script action tooinstall multiple components on hello cluster.</span></span> <span data-ttu-id="b07e3-143">Dopo aver aggiunto gli script hello, fare clic su hello segno di spunta toostart la creazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b07e3-143">After you have added hello scripts, click hello checkmark toostart creating hello cluster.</span></span>

## <a name="use-solr"></a><span data-ttu-id="b07e3-144">Utilizzare Solr</span><span class="sxs-lookup"><span data-stu-id="b07e3-144">Use Solr</span></span>
<span data-ttu-id="b07e3-145">È prima di tutto necessario indicizzare Solr con alcuni file di dati.</span><span class="sxs-lookup"><span data-stu-id="b07e3-145">You must start with indexing Solr with some data files.</span></span> <span data-ttu-id="b07e3-146">Quindi, è possibile utilizzare le query di ricerca di Solr toorun sui dati hello indicizzato.</span><span class="sxs-lookup"><span data-stu-id="b07e3-146">You can then use Solr toorun search queries on hello indexed data.</span></span> <span data-ttu-id="b07e3-147">Eseguire hello seguendo i passaggi toouse Solr in un cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b07e3-147">Perform hello following steps toouse Solr in an HDInsight cluster:</span></span>

1. <span data-ttu-id="b07e3-148">**Utilizzare tooremote Remote Desktop Protocol (RDP) in cluster di HDInsight hello con Solr installato**.</span><span class="sxs-lookup"><span data-stu-id="b07e3-148">**Use Remote Desktop Protocol (RDP) tooremote into hello HDInsight cluster with Solr installed**.</span></span> <span data-ttu-id="b07e3-149">Dal portale di Azure hello, abilitare Desktop remoto per il cluster hello che è stato creato con cluster hello installato e quindi remoto in Solr.</span><span class="sxs-lookup"><span data-stu-id="b07e3-149">From hello Azure portal, enable Remote Desktop for hello cluster you created with Solr installed, and then remote into hello cluster.</span></span> <span data-ttu-id="b07e3-150">Per istruzioni, vedere [connettersi tooHDInsight cluster tramite RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="b07e3-150">For instructions, see [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="b07e3-151">**Indicizzare Solr mediante il caricamento di file di dati**.</span><span class="sxs-lookup"><span data-stu-id="b07e3-151">**Index Solr by uploading data files**.</span></span> <span data-ttu-id="b07e3-152">Quando si indicizzano Solr, inserire i documenti che potrebbe essere necessario toosearch in.</span><span class="sxs-lookup"><span data-stu-id="b07e3-152">When you index Solr, you put documents in it that you may need toosearch on.</span></span> <span data-ttu-id="b07e3-153">tooindex Solr, utilizzare il protocollo RDP tooremote in cluster hello, passare toohello desktop, aprire hello Hadoop riga di comando e passare troppo**C:\apps\dist\solr-4.7.2\example\exampledocs**.</span><span class="sxs-lookup"><span data-stu-id="b07e3-153">tooindex Solr, use RDP tooremote into hello cluster, navigate toohello desktop, open hello Hadoop command line, and navigate too**C:\apps\dist\solr-4.7.2\example\exampledocs**.</span></span> <span data-ttu-id="b07e3-154">Eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b07e3-154">Run hello following command:</span></span>

        java -jar post.jar solr.xml monitor.xml

    <span data-ttu-id="b07e3-155">Si noterà hello seguente output sulla console hello:</span><span class="sxs-lookup"><span data-stu-id="b07e3-155">You'll see hello following output on hello console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="b07e3-156">utilità post.jar Hello indicizzati Solr con due documenti di esempio, **solr.xml** e **monitor.xml**.</span><span class="sxs-lookup"><span data-stu-id="b07e3-156">hello post.jar utility indexes Solr with two sample documents, **solr.xml** and **monitor.xml**.</span></span> <span data-ttu-id="b07e3-157">utilità post.jar Hello e documenti di esempio hello sono disponibili con l'installazione di Solr.</span><span class="sxs-lookup"><span data-stu-id="b07e3-157">hello post.jar utility and hello sample documents are available with Solr installation.</span></span>
3. <span data-ttu-id="b07e3-158">**Utilizzare hello Solr dashboard toosearch all'interno di hello indicizzata documenti**.</span><span class="sxs-lookup"><span data-stu-id="b07e3-158">**Use hello Solr dashboard toosearch within hello indexed documents**.</span></span> <span data-ttu-id="b07e3-159">In hello RDP sessione toohello HDInsight del cluster, aprire Internet Explorer e avviare il dashboard di Solr hello in **http://headnodehost:8983/solr / #/**.</span><span class="sxs-lookup"><span data-stu-id="b07e3-159">In hello RDP session toohello HDInsight cluster, open Internet Explorer, and launch hello Solr dashboard at **http://headnodehost:8983/solr/#/**.</span></span> <span data-ttu-id="b07e3-160">Dal riquadro sinistro di hello, da hello **selettore Core** elenco a discesa, selezionare **collection1**, all'interno di esso, fare clic su **Query**.</span><span class="sxs-lookup"><span data-stu-id="b07e3-160">From hello left pane, from hello **Core Selector** drop-down, select **collection1**, and within that, click **Query**.</span></span> <span data-ttu-id="b07e3-161">Un esempio, tooselect e restituire tutti i documenti di hello Solr, fornire hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="b07e3-161">As an example, tooselect and return all hello docs in Solr, provide hello following values:</span></span>

   * <span data-ttu-id="b07e3-162">In hello **q** testo immettere  **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="b07e3-162">In hello **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="b07e3-163">Ciò restituirà tutti i documenti indicizzati hello in Solr.</span><span class="sxs-lookup"><span data-stu-id="b07e3-163">This will return all hello documents that are indexed in Solr.</span></span> <span data-ttu-id="b07e3-164">Se si desidera toosearch una stringa specifica all'interno dei documenti hello, è possibile immettere qui la stringa.</span><span class="sxs-lookup"><span data-stu-id="b07e3-164">If you want toosearch for a specific string within hello documents, you can enter that string here.</span></span>
   * <span data-ttu-id="b07e3-165">In hello **wt** casella di testo, il formato di output di hello selezionare.</span><span class="sxs-lookup"><span data-stu-id="b07e3-165">In hello **wt** text box, select hello output format.</span></span> <span data-ttu-id="b07e3-166">Il valore predefinito è **json**.</span><span class="sxs-lookup"><span data-stu-id="b07e3-166">Default is **json**.</span></span> <span data-ttu-id="b07e3-167">Fare clic su **Esegui query**.</span><span class="sxs-lookup"><span data-stu-id="b07e3-167">Click **Execute Query**.</span></span>

     <span data-ttu-id="b07e3-168">![Utilizzare l'azione Script toocustomize un cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "eseguire una query su dashboard Solr")</span><span class="sxs-lookup"><span data-stu-id="b07e3-168">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Run a query on Solr dashboard")</span></span>

     <span data-ttu-id="b07e3-169">output di Hello restituisce hello due documenti che è stata utilizzata per l'indicizzazione di Solr.</span><span class="sxs-lookup"><span data-stu-id="b07e3-169">hello output returns hello two docs that we used for indexing Solr.</span></span> <span data-ttu-id="b07e3-170">output di Hello analogo al seguente hello:</span><span class="sxs-lookup"><span data-stu-id="b07e3-170">hello output resembles hello following:</span></span>

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
4. <span data-ttu-id="b07e3-171">**Consigliato: Eseguire il backup hello indicizzata dati da Solr tooAzure archiviazione Blob associato al cluster HDInsight hello**.</span><span class="sxs-lookup"><span data-stu-id="b07e3-171">**Recommended: Back up hello indexed data from Solr tooAzure Blob storage associated with hello HDInsight cluster**.</span></span> <span data-ttu-id="b07e3-172">È buona norma, è consigliabile eseguire backup dati hello indicizzato dai nodi di cluster Solr hello in archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="b07e3-172">As a good practice, you should back up hello indexed data from hello Solr cluster nodes onto Azure Blob storage.</span></span> <span data-ttu-id="b07e3-173">Eseguire hello seguendo i passaggi toodo pertanto:</span><span class="sxs-lookup"><span data-stu-id="b07e3-173">Perform hello following steps toodo so:</span></span>

   1. <span data-ttu-id="b07e3-174">Dalla sessione RDP hello, aprire Internet Explorer e toohello punto URL seguente:</span><span class="sxs-lookup"><span data-stu-id="b07e3-174">From hello RDP session, open Internet Explorer, and point toohello following URL:</span></span>

           http://localhost:8983/solr/replication?command=backup

       <span data-ttu-id="b07e3-175">Viene visualizzata una risposta simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="b07e3-175">You should see a response like this:</span></span>

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. <span data-ttu-id="b07e3-176">Nella sessione remota hello, passare troppo {SOLR_HOME}\{raccolta} \data.</span><span class="sxs-lookup"><span data-stu-id="b07e3-176">In hello remote session, navigate too{SOLR_HOME}\{Collection}\data.</span></span> <span data-ttu-id="b07e3-177">Per cluster hello creati tramite script di esempio hello, deve essere **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span><span class="sxs-lookup"><span data-stu-id="b07e3-177">For hello cluster created via hello sample script, this should be **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span></span> <span data-ttu-id="b07e3-178">In questa posizione, si dovrebbe essere una cartella snapshot creata con un nome simile troppo**snapshot.* timestamp** *.</span><span class="sxs-lookup"><span data-stu-id="b07e3-178">At this location, you should see a snapshot folder created with a name similar too**snapshot.*timestamp***.</span></span>
   3. <span data-ttu-id="b07e3-179">Codice postale cartella snapshot hello e caricarlo nell'archiviazione Blob tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b07e3-179">Zip hello snapshot folder and upload it tooAzure Blob storage.</span></span> <span data-ttu-id="b07e3-180">Dalla riga di comando hello Hadoop, passare toohello percorso della cartella snapshot hello utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b07e3-180">From hello Hadoop command line, navigate toohello location of hello snapshot folder by using hello following command:</span></span>

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       <span data-ttu-id="b07e3-181">Questo comando copia hello dati dello snapshot troppo/esempio / / nel contenitore hello all'interno di predefinito hello Storage account associato hello cluster.</span><span class="sxs-lookup"><span data-stu-id="b07e3-181">This command copies hello snapshot too/example/data/ under hello container within hello default Storage account associated with hello cluster.</span></span>

## <a name="install-solr-using-aure-powershell"></a><span data-ttu-id="b07e3-182">Installare Solr tramite Aure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b07e3-182">Install Solr using Aure PowerShell</span></span>
<span data-ttu-id="b07e3-183">Vedere [Personalizzare cluster HDInsight usando l'azione script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="b07e3-183">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="b07e3-184">esempio Hello viene illustrato come tooinstall Spark con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b07e3-184">hello sample demonstrates how tooinstall Spark using Azure PowerShell.</span></span> <span data-ttu-id="b07e3-185">È necessario toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="b07e3-185">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="install-solr-using-net-sdk"></a><span data-ttu-id="b07e3-186">Installare Solr tramite .NET SDK</span><span class="sxs-lookup"><span data-stu-id="b07e3-186">Install Solr using .NET SDK</span></span>
<span data-ttu-id="b07e3-187">Vedere [Personalizzare cluster HDInsight usando l'azione script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="b07e3-187">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="b07e3-188">esempio Hello viene illustrato come tooinstall Spark usando hello .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="b07e3-188">hello sample demonstrates how tooinstall Spark using hello .NET SDK.</span></span> <span data-ttu-id="b07e3-189">È necessario toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="b07e3-189">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="b07e3-190">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="b07e3-190">See also</span></span>
* [<span data-ttu-id="b07e3-191">Installare e usare Solr nei cluster Hadoop di HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="b07e3-191">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="b07e3-192">[Creare cluster Hadoop in HDInsight](hdinsight-provision-clusters.md): informazioni generali sulla creazione di cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="b07e3-192">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="b07e3-193">[Personalizzare cluster HDInsight mediante l'azione Script][hdinsight-cluster-customize]: informazioni generali sulla personalizzazione di cluster HDInsight tramite Azione script.</span><span class="sxs-lookup"><span data-stu-id="b07e3-193">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="b07e3-194">[Sviluppare script di Azione script per HDInsight](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="b07e3-194">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="b07e3-195">[Installare e usare Spark nei cluster HDInsight][hdinsight-install-spark]: esempio di azione script sull'installazione di Spark.</span><span class="sxs-lookup"><span data-stu-id="b07e3-195">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="b07e3-196">[Installare R nei cluster HDInsight][hdinsight-install-r]: esempio di azione script sull'installazione di R.</span><span class="sxs-lookup"><span data-stu-id="b07e3-196">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="b07e3-197">[Installare e usare Spark nei cluster HDInsight](hdinsight-hadoop-giraph-install.md): esempio di Script azione sull'installazione di Giraph</span><span class="sxs-lookup"><span data-stu-id="b07e3-197">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
