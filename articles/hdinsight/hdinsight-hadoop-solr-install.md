---
title: Usare l'azione script per installare Solr in cluster Hadoop| Documentazione Microsoft
description: Informazioni su come personalizzare cluster HDInsight con Solr tramite le azioni script.
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
ms.openlocfilehash: 6efb7ea26c3cdf7748fff4b02b5810c85cc41e1a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="f808c-103">Installare e usare Solr nei cluster HDInsight basati su Windows</span><span class="sxs-lookup"><span data-stu-id="f808c-103">Install and use Solr on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="f808c-104">Informazioni su come personalizzare i cluster HDInsight basati su Windows con Solr usando Azioni script e usare Solr per cercare i dati.</span><span class="sxs-lookup"><span data-stu-id="f808c-104">Learn how to customize Windows-based HDInsight cluster with Solr using Script Action, and how to use Solr to search data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f808c-105">I passaggi descritti in questo documento funzionano solo con i cluster HDInsight basati su Windows.</span><span class="sxs-lookup"><span data-stu-id="f808c-105">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="f808c-106">HDInsight è disponibile in Windows solo per le versioni precedenti a HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="f808c-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="f808c-107">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="f808c-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f808c-108">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="f808c-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="f808c-109">Per informazioni sull'uso di Solr con un cluster basato su Linux, vedere [Installare e usare Solr nei cluster Hadoop HDInsight (Linux)](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f808c-109">For information on using Solr with a Linux-based cluster, see [Install and use Solr on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-solr-install-linux.md).</span></span>


<span data-ttu-id="f808c-110">È possibile installare Solr in qualsiasi tipo di cluster (Hadoop, Storm, HBase, Spark) su Azure HDInsight usando *Script azione*.</span><span class="sxs-lookup"><span data-stu-id="f808c-110">You can install Solr on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="f808c-111">Uno script di esempio per l'installazione di Solr in un cluster HDInsight è disponibile in un BLOB di archiviazione di Azure di sola lettura all'indirizzo [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="f808c-111">A sample script to install Solr on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

<span data-ttu-id="f808c-112">Lo script di esempio funziona solo con cluster HDInsight versione 3.1.</span><span class="sxs-lookup"><span data-stu-id="f808c-112">The sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="f808c-113">Per altre informazioni sulle versioni dei cluster HDInsight, vedere [Versioni cluster HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="f808c-113">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="f808c-114">Lo script di esempio usato in questo argomento crea un cluster Solr basato su Windows con una configurazione specifica.</span><span class="sxs-lookup"><span data-stu-id="f808c-114">The sample script used in this topic creates a Windows-based Solr cluster with a specific configuration.</span></span> <span data-ttu-id="f808c-115">Per configurare il cluster Solr con raccolte, partizioni, schemi, repliche diverse e così via, sarà necessario modificare di conseguenza lo script e i file binari di Solr.</span><span class="sxs-lookup"><span data-stu-id="f808c-115">If you want to configure the Solr cluster with different collections, shards, schemas, replicas, etc., you must modify the script and Solr binaries accordingly.</span></span>

<span data-ttu-id="f808c-116">**Articoli correlati**</span><span class="sxs-lookup"><span data-stu-id="f808c-116">**Related articles**</span></span>

* [<span data-ttu-id="f808c-117">Installare e usare Solr nei cluster Hadoop di HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="f808c-117">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="f808c-118">[Creare cluster Hadoop in HDInsight](hdinsight-provision-clusters.md): informazioni generali sulla creazione di cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="f808c-118">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="f808c-119">[Personalizzare cluster HDInsight mediante l'azione Script][hdinsight-cluster-customize]: informazioni generali sulla personalizzazione di cluster HDInsight tramite Azione script.</span><span class="sxs-lookup"><span data-stu-id="f808c-119">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="f808c-120">[Sviluppare script di Azione script per HDInsight](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="f808c-120">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-solr"></a><span data-ttu-id="f808c-121">Che cos'è Solr?</span><span class="sxs-lookup"><span data-stu-id="f808c-121">What is Solr?</span></span>
<span data-ttu-id="f808c-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> è una piattaforma di ricerca aziendale che permette di eseguire ricerche full-text avanzate sui dati.</span><span class="sxs-lookup"><span data-stu-id="f808c-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="f808c-123">Mentre Hadoop consente di archiviare e gestire quantità elevate di dati, Apache Solr offre le funzionalità di ricerca necessarie per recuperare rapidamente i dati.</span><span class="sxs-lookup"><span data-stu-id="f808c-123">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides the search capabilities to quickly retrieve the data.</span></span>

## <a name="install-solr-using-portal"></a><span data-ttu-id="f808c-124">Installare Solr utilizzando il portale</span><span class="sxs-lookup"><span data-stu-id="f808c-124">Install Solr using portal</span></span>
1. <span data-ttu-id="f808c-125">Avviare la creazione di un cluster usando l'opzione **CREAZIONE PERSONALIZZATA**, come descritto in [Creare cluster Hadoop in HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="f808c-125">Start creating a cluster by using the **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="f808c-126">Nella pagina **Azioni script** della procedura guidata fare clic su **aggiungi azione script** per specificare i dettagli relativi all'azione script, come descritto di seguito:</span><span class="sxs-lookup"><span data-stu-id="f808c-126">On the **Script Actions** page of the wizard, click **add script action** to provide details about the script action, as shown below:</span></span>

    <span data-ttu-id="f808c-127">![Usare l'azione script per personalizzare un cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "Usare l'azione script per personalizzare un cluster")</span><span class="sxs-lookup"><span data-stu-id="f808c-127">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="f808c-128">Proprietà</span><span class="sxs-lookup"><span data-stu-id="f808c-128">Property</span></span></th><th><span data-ttu-id="f808c-129">Valore</span><span class="sxs-lookup"><span data-stu-id="f808c-129">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="f808c-130">Nome</span><span class="sxs-lookup"><span data-stu-id="f808c-130">Name</span></span></td>
            <td><span data-ttu-id="f808c-131">Specificare un nome per l'azione script.</span><span class="sxs-lookup"><span data-stu-id="f808c-131">Specify a name for the script action.</span></span> <span data-ttu-id="f808c-132">Ad esempio, <b>Install Solr</b>.</span><span class="sxs-lookup"><span data-stu-id="f808c-132">For example, <b>Install Solr</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="f808c-133">URI script</span><span class="sxs-lookup"><span data-stu-id="f808c-133">Script URI</span></span></td>
            <td><span data-ttu-id="f808c-134">Specificare l'URI (Uniform Resource Identifier) dello script da richiamare per personalizzare il cluster.</span><span class="sxs-lookup"><span data-stu-id="f808c-134">Specify the Uniform Resource Identifier (URI) to the script that is invoked to customize the cluster.</span></span> <span data-ttu-id="f808c-135">Ad esempio, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="f808c-135">For example, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="f808c-136">Tipo di nodo</span><span class="sxs-lookup"><span data-stu-id="f808c-136">Node Type</span></span></td>
            <td><span data-ttu-id="f808c-137">Specificare i nodi in cui viene eseguito lo script di personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="f808c-137">Specify the nodes on which the customization script is run.</span></span> <span data-ttu-id="f808c-138">È possibile scegliere <b>Tutti i nodi</b>, <b>Solo nodi head</b> o <b>Solo nodi di lavoro</b>.</span><span class="sxs-lookup"><span data-stu-id="f808c-138">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="f808c-139">Parametri</span><span class="sxs-lookup"><span data-stu-id="f808c-139">Parameters</span></span></td>
            <td><span data-ttu-id="f808c-140">Specificare i parametri, se richiesti dallo script.</span><span class="sxs-lookup"><span data-stu-id="f808c-140">Specify the parameters, if required by the script.</span></span> <span data-ttu-id="f808c-141">Lo script per installare Solr non richiede alcun parametro, di conseguenza è possibile lasciare vuoto questo campo.</span><span class="sxs-lookup"><span data-stu-id="f808c-141">The script to install Solr does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="f808c-142">È possibile aggiungere altre azioni script per installare più componenti nel cluster.</span><span class="sxs-lookup"><span data-stu-id="f808c-142">You can add more than one script action to install multiple components on the cluster.</span></span> <span data-ttu-id="f808c-143">Dopo aver aggiunto gli script, fare clic sul segno di spunta per avviare la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="f808c-143">After you have added the scripts, click the checkmark to start creating the cluster.</span></span>

## <a name="use-solr"></a><span data-ttu-id="f808c-144">Utilizzare Solr</span><span class="sxs-lookup"><span data-stu-id="f808c-144">Use Solr</span></span>
<span data-ttu-id="f808c-145">È prima di tutto necessario indicizzare Solr con alcuni file di dati.</span><span class="sxs-lookup"><span data-stu-id="f808c-145">You must start with indexing Solr with some data files.</span></span> <span data-ttu-id="f808c-146">Sarà quindi possibile usare Solr per eseguire query di ricerca sui dati indicizzati.</span><span class="sxs-lookup"><span data-stu-id="f808c-146">You can then use Solr to run search queries on the indexed data.</span></span> <span data-ttu-id="f808c-147">Eseguire la procedura seguente per usare Solr in un cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="f808c-147">Perform the following steps to use Solr in an HDInsight cluster:</span></span>

1. <span data-ttu-id="f808c-148">**Usare RDP (Remote Desktop Protocol) per accedere in remoto al cluster HDInsight con Solr installato**.</span><span class="sxs-lookup"><span data-stu-id="f808c-148">**Use Remote Desktop Protocol (RDP) to remote into the HDInsight cluster with Solr installed**.</span></span> <span data-ttu-id="f808c-149">Dal portale di Azure abilitare il desktop remoto per il cluster creato con Solr installato, quindi accedere in remoto al cluster.</span><span class="sxs-lookup"><span data-stu-id="f808c-149">From the Azure portal, enable Remote Desktop for the cluster you created with Solr installed, and then remote into the cluster.</span></span> <span data-ttu-id="f808c-150">Per istruzioni, vedere [Connettersi a cluster HDInsight tramite RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="f808c-150">For instructions, see [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="f808c-151">**Indicizzare Solr mediante il caricamento di file di dati**.</span><span class="sxs-lookup"><span data-stu-id="f808c-151">**Index Solr by uploading data files**.</span></span> <span data-ttu-id="f808c-152">Quando si indicizza Solr, si inseriscono documenti su cui potrebbe essere necessario eseguire ricerche.</span><span class="sxs-lookup"><span data-stu-id="f808c-152">When you index Solr, you put documents in it that you may need to search on.</span></span> <span data-ttu-id="f808c-153">Per indicizzare Solr, usare RDP per accedere in remoto al cluster, passare al desktop, aprire la riga di comando di Hadoop e quindi passare a **C:\apps\dist\solr-4.7.2\example\exampledocs**.</span><span class="sxs-lookup"><span data-stu-id="f808c-153">To index Solr, use RDP to remote into the cluster, navigate to the desktop, open the Hadoop command line, and navigate to **C:\apps\dist\solr-4.7.2\example\exampledocs**.</span></span> <span data-ttu-id="f808c-154">Eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f808c-154">Run the following command:</span></span>

        java -jar post.jar solr.xml monitor.xml

    <span data-ttu-id="f808c-155">Nella console viene visualizzato il seguente risultato:</span><span class="sxs-lookup"><span data-stu-id="f808c-155">You'll see the following output on the console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes to http://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="f808c-156">L'utilità post.jar indicizza Solr con due documenti di esempio, **solr.xml** e **monitor.xml**.</span><span class="sxs-lookup"><span data-stu-id="f808c-156">The post.jar utility indexes Solr with two sample documents, **solr.xml** and **monitor.xml**.</span></span> <span data-ttu-id="f808c-157">L'utilità post.jar e i documenti di esempio sono disponibili con l'installazione di Solr.</span><span class="sxs-lookup"><span data-stu-id="f808c-157">The post.jar utility and the sample documents are available with Solr installation.</span></span>
3. <span data-ttu-id="f808c-158">**Usare il dashboard di Solr per eseguire ricerche nei documenti indicizzati**.</span><span class="sxs-lookup"><span data-stu-id="f808c-158">**Use the Solr dashboard to search within the indexed documents**.</span></span> <span data-ttu-id="f808c-159">Nella sessione RDP per il cluster HDInsight, aprire Internet Explorer, quindi avviare il dashboard di Solr all'indirizzo **http://headnodehost:8983/solr/#/**.</span><span class="sxs-lookup"><span data-stu-id="f808c-159">In the RDP session to the HDInsight cluster, open Internet Explorer, and launch the Solr dashboard at **http://headnodehost:8983/solr/#/**.</span></span> <span data-ttu-id="f808c-160">Nel riquadro a sinistra selezionare **collection1** dal menu a discesa **Core Selector** (Selettore principale) e quindi fare clic su **Query**.</span><span class="sxs-lookup"><span data-stu-id="f808c-160">From the left pane, from the **Core Selector** drop-down, select **collection1**, and within that, click **Query**.</span></span> <span data-ttu-id="f808c-161">Ad esempio, per selezionare e restituire tutti i documenti in Solr, specificare i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="f808c-161">As an example, to select and return all the docs in Solr, provide the following values:</span></span>

   * <span data-ttu-id="f808c-162">Nella casella di testo **q** immettere **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="f808c-162">In the **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="f808c-163">Verranno restituiti tutti i documenti indicizzati in Solr.</span><span class="sxs-lookup"><span data-stu-id="f808c-163">This will return all the documents that are indexed in Solr.</span></span> <span data-ttu-id="f808c-164">Per cercare una stringa specifica nei documenti, è possibile immettere qui la stringa.</span><span class="sxs-lookup"><span data-stu-id="f808c-164">If you want to search for a specific string within the documents, you can enter that string here.</span></span>
   * <span data-ttu-id="f808c-165">Selezionare il formato di output nella casella di testo **wt** .</span><span class="sxs-lookup"><span data-stu-id="f808c-165">In the **wt** text box, select the output format.</span></span> <span data-ttu-id="f808c-166">Il valore predefinito è **json**.</span><span class="sxs-lookup"><span data-stu-id="f808c-166">Default is **json**.</span></span> <span data-ttu-id="f808c-167">Fare clic su **Esegui query**.</span><span class="sxs-lookup"><span data-stu-id="f808c-167">Click **Execute Query**.</span></span>

     <span data-ttu-id="f808c-168">![Usare l'azione script per personalizzare un cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Eseguire una query sul dashboard Solr")</span><span class="sxs-lookup"><span data-stu-id="f808c-168">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Run a query on Solr dashboard")</span></span>

     <span data-ttu-id="f808c-169">L'output restituisce i due documenti usati per l'indicizzazione di Solr.</span><span class="sxs-lookup"><span data-stu-id="f808c-169">The output returns the two docs that we used for indexing Solr.</span></span> <span data-ttu-id="f808c-170">L'output sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="f808c-170">The output resembles the following:</span></span>

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
4. <span data-ttu-id="f808c-171">**Consigliato: backup dei dati indicizzati da Solr all'archivio BLOB di Azure associato al cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="f808c-171">**Recommended: Back up the indexed data from Solr to Azure Blob storage associated with the HDInsight cluster**.</span></span> <span data-ttu-id="f808c-172">È consigliabile eseguire il backup dei dati indicizzati dai nodi del cluster Solr nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="f808c-172">As a good practice, you should back up the indexed data from the Solr cluster nodes onto Azure Blob storage.</span></span> <span data-ttu-id="f808c-173">Eseguire quindi la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f808c-173">Perform the following steps to do so:</span></span>

   1. <span data-ttu-id="f808c-174">Aprire Internet Explorer dalla sessione RDP, quindi selezionare l'URL seguente:</span><span class="sxs-lookup"><span data-stu-id="f808c-174">From the RDP session, open Internet Explorer, and point to the following URL:</span></span>

           http://localhost:8983/solr/replication?command=backup

       <span data-ttu-id="f808c-175">Viene visualizzata una risposta simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="f808c-175">You should see a response like this:</span></span>

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. <span data-ttu-id="f808c-176">Nella sessione remota passare a {SOLR_HOME}\{Collection}\data.</span><span class="sxs-lookup"><span data-stu-id="f808c-176">In the remote session, navigate to {SOLR_HOME}\{Collection}\data.</span></span> <span data-ttu-id="f808c-177">Per il cluster creato tramite lo script di esempio, sarà uguale a **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span><span class="sxs-lookup"><span data-stu-id="f808c-177">For the cluster created via the sample script, this should be **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span></span> <span data-ttu-id="f808c-178">In questo percorso dovrebbe essere creata una cartella snapshot con nome simile a **snapshot.*timestamp***.</span><span class="sxs-lookup"><span data-stu-id="f808c-178">At this location, you should see a snapshot folder created with a name similar to **snapshot.*timestamp***.</span></span>
   3. <span data-ttu-id="f808c-179">Comprimere la cartella snapshot e caricarla nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="f808c-179">Zip the snapshot folder and upload it to Azure Blob storage.</span></span> <span data-ttu-id="f808c-180">Dalla riga di comando di Hadoop passare al percorso della cartella snapshot usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f808c-180">From the Hadoop command line, navigate to the location of the snapshot folder by using the following command:</span></span>

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       <span data-ttu-id="f808c-181">Questo comando copia lo snapshot in /example/data/ nel contenitore disponibile nell'account di archiviazione predefinito associato al cluster.</span><span class="sxs-lookup"><span data-stu-id="f808c-181">This command copies the snapshot to /example/data/ under the container within the default Storage account associated with the cluster.</span></span>

## <a name="install-solr-using-aure-powershell"></a><span data-ttu-id="f808c-182">Installare Solr tramite Aure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f808c-182">Install Solr using Aure PowerShell</span></span>
<span data-ttu-id="f808c-183">Vedere [Personalizzare cluster HDInsight usando l'azione script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="f808c-183">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="f808c-184">L'esempio illustra come installare Spark tramite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f808c-184">The sample demonstrates how to install Spark using Azure PowerShell.</span></span> <span data-ttu-id="f808c-185">È necessario personalizzare lo script da usare [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="f808c-185">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="install-solr-using-net-sdk"></a><span data-ttu-id="f808c-186">Installare Solr tramite .NET SDK</span><span class="sxs-lookup"><span data-stu-id="f808c-186">Install Solr using .NET SDK</span></span>
<span data-ttu-id="f808c-187">Vedere [Personalizzare cluster HDInsight usando l'azione script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="f808c-187">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="f808c-188">L'esempio illustra come installare Spark tramite .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="f808c-188">The sample demonstrates how to install Spark using the .NET SDK.</span></span> <span data-ttu-id="f808c-189">È necessario personalizzare lo script da usare [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="f808c-189">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="f808c-190">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f808c-190">See also</span></span>
* [<span data-ttu-id="f808c-191">Installare e usare Solr nei cluster Hadoop di HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="f808c-191">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="f808c-192">[Creare cluster Hadoop in HDInsight](hdinsight-provision-clusters.md): informazioni generali sulla creazione di cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="f808c-192">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="f808c-193">[Personalizzare cluster HDInsight mediante l'azione Script][hdinsight-cluster-customize]: informazioni generali sulla personalizzazione di cluster HDInsight tramite Azione script.</span><span class="sxs-lookup"><span data-stu-id="f808c-193">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="f808c-194">[Sviluppare script di Azione script per HDInsight](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="f808c-194">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="f808c-195">[Installare e usare Spark nei cluster HDInsight][hdinsight-install-spark]: esempio di azione script sull'installazione di Spark.</span><span class="sxs-lookup"><span data-stu-id="f808c-195">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="f808c-196">[Installare R nei cluster HDInsight][hdinsight-install-r]: esempio di azione script sull'installazione di R.</span><span class="sxs-lookup"><span data-stu-id="f808c-196">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="f808c-197">[Installare e usare Spark nei cluster HDInsight](hdinsight-hadoop-giraph-install.md): esempio di Script azione sull'installazione di Giraph</span><span class="sxs-lookup"><span data-stu-id="f808c-197">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
