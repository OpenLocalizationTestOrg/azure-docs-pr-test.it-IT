---
title: Iniziare a usare un esempio di HBase in HDInsight - Azure | Microsoft Docs
description: Seguire questo esempio di Apache HBase per iniziare a usare Hadoop in HDInsight. Creare tabelle dalla shell HBase e sottoporle a query tramite Hive.
keywords: hbasecommand, esempio di hbase
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 4d6a2658-6b19-4268-95ee-822890f5a33a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: bbd8a838062795ee03ae02dc5e3fd45d841a6e17
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-an-apache-hbase-example-in-hdinsight"></a><span data-ttu-id="04e1b-105">Iniziare a usare un esempio di Apache HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="04e1b-105">Get started with an Apache HBase example in HDInsight</span></span>

<span data-ttu-id="04e1b-106">Informazioni su come creare un cluster HBase in HDInsight, creare tabelle HBase ed eseguire query sulle tabelle con Hive.</span><span class="sxs-lookup"><span data-stu-id="04e1b-106">Learn how to create an HBase cluster in HDInsight, create HBase tables, and query tables by using Hive.</span></span> <span data-ttu-id="04e1b-107">Per informazioni generali su HBase, vedere [Panoramica di HDInsight HBase][hdinsight-hbase-overview].</span><span class="sxs-lookup"><span data-stu-id="04e1b-107">For general HBase information, see [HDInsight HBase overview][hdinsight-hbase-overview].</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a><span data-ttu-id="04e1b-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="04e1b-108">Prerequisites</span></span>
<span data-ttu-id="04e1b-109">Prima di iniziare a provare questo esempio di HBase, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="04e1b-109">Before you begin trying this HBase example, you must have the following items:</span></span>

* <span data-ttu-id="04e1b-110">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="04e1b-110">**An Azure subscription**.</span></span> <span data-ttu-id="04e1b-111">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="04e1b-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="04e1b-112">[Secure Shell (SSH)](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="04e1b-112">[Secure Shell(SSH)](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> 
* <span data-ttu-id="04e1b-113">[curl](http://curl.haxx.se/download.html).</span><span class="sxs-lookup"><span data-stu-id="04e1b-113">[curl](http://curl.haxx.se/download.html).</span></span>

## <a name="create-hbase-cluster"></a><span data-ttu-id="04e1b-114">Nome del cluster HBase</span><span class="sxs-lookup"><span data-stu-id="04e1b-114">Create HBase cluster</span></span>
<span data-ttu-id="04e1b-115">La procedura seguente usa un modello di Azure Resource Manager per creare un cluster HBase basato su Linux versione 3.4 e il valore predefinito dipendente dall'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="04e1b-115">The following procedure uses an Azure Resource Manager template to create a version 3.4 Linux-based HBase cluster and the dependent default Azure Storage account.</span></span> <span data-ttu-id="04e1b-116">Per comprendere i parametri usati nella procedure e altri metodi di creazione del cluster, vedere [Creare cluster Hadoop basati su Linux in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="04e1b-116">To understand the parameters used in the procedure and other cluster creation methods, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="04e1b-117">Fare clic sull'immagine seguente per aprire il modello nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="04e1b-117">Click the following image to open the template in the Azure portal.</span></span> <span data-ttu-id="04e1b-118">Il modello è disponibile in un contenitore BLOB pubblico.</span><span class="sxs-lookup"><span data-stu-id="04e1b-118">The template is located in a public blob container.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-tutorial-get-started-linux/deploy-to-azure.png" alt="Deploy to Azure"></a>
2. <span data-ttu-id="04e1b-119">Compilare i campi seguenti del pannello **Distribuzione personalizzata**:</span><span class="sxs-lookup"><span data-stu-id="04e1b-119">From the **Custom deployment** blade, enter the following values:</span></span>
   
   * <span data-ttu-id="04e1b-120">**Sottoscrizione**: selezionare la sottoscrizione di Azure che viene usata per creare il cluster.</span><span class="sxs-lookup"><span data-stu-id="04e1b-120">**Subscription**: Select your Azure subscription that is used to create the cluster.</span></span>
   * <span data-ttu-id="04e1b-121">**Gruppo di risorse**: creare un nuovo gruppo di Azure Resource Manager o usarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="04e1b-121">**Resource group**: Create an Azure Resource Management group or use an existing one.</span></span>
   * <span data-ttu-id="04e1b-122">**Posizione**: consente di specificare la posizione del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="04e1b-122">**Location**: Specify the location of the resource group.</span></span> 
   * <span data-ttu-id="04e1b-123">**Nome del cluster**: immettere un nome per il cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="04e1b-123">**ClusterName**: Enter a name for the HBase cluster.</span></span>
   * <span data-ttu-id="04e1b-124">**Cluster login name and password**: il nome dell'account di accesso predefinito è **admin**.</span><span class="sxs-lookup"><span data-stu-id="04e1b-124">**Cluster login name and password**: The default login name is **admin**.</span></span>
   * <span data-ttu-id="04e1b-125">**SSH username and password**: il nome utente predefinito è **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="04e1b-125">**SSH username and password**: The default username is **sshuser**.</span></span>  <span data-ttu-id="04e1b-126">È possibile rinominarlo.</span><span class="sxs-lookup"><span data-stu-id="04e1b-126">You can rename it.</span></span>
     
     <span data-ttu-id="04e1b-127">Gli altri parametri sono facoltativi.</span><span class="sxs-lookup"><span data-stu-id="04e1b-127">Other parameters are optional.</span></span>  
     
     <span data-ttu-id="04e1b-128">Ogni cluster ha una dipendenza dall'account di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="04e1b-128">Each cluster has an Azure Storage account dependency.</span></span> <span data-ttu-id="04e1b-129">Dopo aver eliminato un cluster, i dati vengono mantenuti nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="04e1b-129">After you delete a cluster, the data retains in the storage account.</span></span> <span data-ttu-id="04e1b-130">Il nome dell'account di archiviazione predefinito del cluster è il nome del cluster a cui viene aggiunto "store".</span><span class="sxs-lookup"><span data-stu-id="04e1b-130">The cluster default storage account name is the cluster name with "store" appended.</span></span> <span data-ttu-id="04e1b-131">È hardcoded nella sezione delle variabili del modello.</span><span class="sxs-lookup"><span data-stu-id="04e1b-131">It is hardcoded in the template variables section.</span></span>
3. <span data-ttu-id="04e1b-132">Selezionare **Accetto le condizioni riportate sopra**, quindi fare clic su **Acquista**.</span><span class="sxs-lookup"><span data-stu-id="04e1b-132">Select **I agree to the terms and conditions stated above**, and then click **Purchase**.</span></span> <span data-ttu-id="04e1b-133">La creazione di un cluster richiede circa 20 minuti.</span><span class="sxs-lookup"><span data-stu-id="04e1b-133">It takes about 20 minutes to create a cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="04e1b-134">Dopo l'eliminazione di un cluster HBase, è possibile creare un altro cluster HBase usando lo stesso contenitore di BLOB predefinito.</span><span class="sxs-lookup"><span data-stu-id="04e1b-134">After an HBase cluster is deleted, you can create another HBase cluster by using the same default blob container.</span></span> <span data-ttu-id="04e1b-135">Il nuovo cluster seleziona le tabelle HBase create nel cluster originale.</span><span class="sxs-lookup"><span data-stu-id="04e1b-135">The new cluster picks up the HBase tables you created in the original cluster.</span></span> <span data-ttu-id="04e1b-136">Per evitare incoerenze, è consigliabile disabilitare le tabelle HBase prima di eliminare il cluster.</span><span class="sxs-lookup"><span data-stu-id="04e1b-136">To avoid inconsistencies, we recommend that you disable the HBase tables before you delete the cluster.</span></span>
> 
> 

## <a name="create-tables-and-insert-data"></a><span data-ttu-id="04e1b-137">Creare tabelle e inserire dati</span><span class="sxs-lookup"><span data-stu-id="04e1b-137">Create tables and insert data</span></span>
<span data-ttu-id="04e1b-138">È possibile usare SSH per connettersi ai cluster HBase e usare la shell di HBase per creare tabelle HBase, inserire dati ed eseguire query sui dati.</span><span class="sxs-lookup"><span data-stu-id="04e1b-138">You can use SSH to connect to HBase clusters and then use HBase Shell to create HBase tables, insert data, and query data.</span></span> <span data-ttu-id="04e1b-139">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="04e1b-139">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="04e1b-140">Per la maggior parte delle persone, i dati vengono visualizzati in formato tabulare:</span><span class="sxs-lookup"><span data-stu-id="04e1b-140">For most people, data appears in the tabular format:</span></span>

![Tabella con dati HBase di HDInsight][img-hbase-sample-data-tabular]

<span data-ttu-id="04e1b-142">In HBase, che rappresenta un'implementazione di BigTable, gli stessi dati sono simili a:</span><span class="sxs-lookup"><span data-stu-id="04e1b-142">In HBase (an implementation of BigTable), the same data looks like:</span></span>

![Dati BigTable HBase di HDInsight][img-hbase-sample-data-bigtable]


<span data-ttu-id="04e1b-144">**Per usare la shell HBase**</span><span class="sxs-lookup"><span data-stu-id="04e1b-144">**To use the HBase shell**</span></span>

1. <span data-ttu-id="04e1b-145">In SSH eseguire il comando HBase seguente:</span><span class="sxs-lookup"><span data-stu-id="04e1b-145">From SSH, run the following HBase command:</span></span>
   
    ```bash
    hbase shell
    ```

2. <span data-ttu-id="04e1b-146">Creare un HBase con famiglie di due colonne:</span><span class="sxs-lookup"><span data-stu-id="04e1b-146">Create an HBase with two-column families:</span></span>

    ```hbaseshell   
    create 'Contacts', 'Personal', 'Office'
    list
    ```
3. <span data-ttu-id="04e1b-147">Inserire alcuni dati:</span><span class="sxs-lookup"><span data-stu-id="04e1b-147">Insert some data:</span></span>
    
    ```hbaseshell   
    put 'Contacts', '1000', 'Personal:Name', 'John Dole'
    put 'Contacts', '1000', 'Personal:Phone', '1-425-000-0001'
    put 'Contacts', '1000', 'Office:Phone', '1-425-000-0002'
    put 'Contacts', '1000', 'Office:Address', '1111 San Gabriel Dr.'
    scan 'Contacts'
    ```
   
    ![Shell HBase Hadoop di HDInsight][img-hbase-shell]
4. <span data-ttu-id="04e1b-149">Ottenere una singola riga</span><span class="sxs-lookup"><span data-stu-id="04e1b-149">Get a single row</span></span>
   
    ```hbaseshell
    get 'Contacts', '1000'
    ```
   
    <span data-ttu-id="04e1b-150">Verranno visualizzati gli stessi risultati usando il comando di analisi, perché esiste solo una riga.</span><span class="sxs-lookup"><span data-stu-id="04e1b-150">You shall see the same results as using the scan command because there is only one row.</span></span>
   
    <span data-ttu-id="04e1b-151">Per altre informazioni sullo schema di tabella HBase, vedere [Introduzione alla progettazione dello schema HBase][hbase-schema].</span><span class="sxs-lookup"><span data-stu-id="04e1b-151">For more information about the HBase table schema, see [Introduction to HBase Schema Design][hbase-schema].</span></span> <span data-ttu-id="04e1b-152">Per altri comandi HBase, vedere la [guida di riferimento di Apache HBase][hbase-quick-start].</span><span class="sxs-lookup"><span data-stu-id="04e1b-152">For more HBase commands, see [Apache HBase reference guide][hbase-quick-start].</span></span>
5. <span data-ttu-id="04e1b-153">Chiudere la shell</span><span class="sxs-lookup"><span data-stu-id="04e1b-153">Exit the shell</span></span>
   
    ```hbaseshell
    exit
    ```

<span data-ttu-id="04e1b-154">**Per il caricamento bulk dei dati nella tabella HBase dei contatti**</span><span class="sxs-lookup"><span data-stu-id="04e1b-154">**To bulk load data into the contacts HBase table**</span></span>

<span data-ttu-id="04e1b-155">HBase include diversi metodi di caricamento dei dati nelle tabelle.</span><span class="sxs-lookup"><span data-stu-id="04e1b-155">HBase includes several methods of loading data into tables.</span></span>  <span data-ttu-id="04e1b-156">Per altre informazioni, vedere [Caricamento bulk](http://hbase.apache.org/book.html#arch.bulk.load).</span><span class="sxs-lookup"><span data-stu-id="04e1b-156">For more information, see [Bulk loading](http://hbase.apache.org/book.html#arch.bulk.load).</span></span>

<span data-ttu-id="04e1b-157">Un file di dati di esempio è disponibile in un contenitore BLOB pubblico, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span><span class="sxs-lookup"><span data-stu-id="04e1b-157">A sample data file can be found in a public blob container, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span></span>  <span data-ttu-id="04e1b-158">Il contenuto del file di dati è il seguente:</span><span class="sxs-lookup"><span data-stu-id="04e1b-158">The content of the data file is:</span></span>

    8396    Calvin Raji      230-555-0191    230-555-0191    5415 San Gabriel Dr.
    16600   Karen Wu         646-555-0113    230-555-0192    9265 La Paz
    4324    Karl Xie         508-555-0163    230-555-0193    4912 La Vuelta
    16891   Jonn Jackson     674-555-0110    230-555-0194    40 Ellis St.
    3273    Miguel Miller    397-555-0155    230-555-0195    6696 Anchor Drive
    3588    Osa Agbonile     592-555-0152    230-555-0196    1873 Lion Circle
    10272   Julia Lee        870-555-0110    230-555-0197    3148 Rose Street
    4868    Jose Hayes       599-555-0171    230-555-0198    793 Crawford Street
    4761    Caleb Alexander  670-555-0141    230-555-0199    4775 Kentucky Dr.
    16443   Terry Chander    998-555-0171    230-555-0200    771 Northridge Drive

<span data-ttu-id="04e1b-159">È facoltativamente possibile creare un file di testo e caricare il file nel proprio account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="04e1b-159">You can optionally create a text file and upload the file to your own storage account.</span></span> <span data-ttu-id="04e1b-160">Per le istruzioni, vedere [Caricare dati per processi Hadoop in HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="04e1b-160">For the instructions, see [Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data].</span></span>

> [!NOTE]
> <span data-ttu-id="04e1b-161">In questa procedura viene utilizzata la tabella HBase dei contatti creata nella procedura precedente.</span><span class="sxs-lookup"><span data-stu-id="04e1b-161">This procedure uses the Contacts HBase table you have created in the last procedure.</span></span>
> 

1. <span data-ttu-id="04e1b-162">In SSH eseguire questo comando per trasformare il file di dati in StoreFiles e archiviarlo in un percorso relativo specificato da Dimporttsv.bulk.output.</span><span class="sxs-lookup"><span data-stu-id="04e1b-162">From SSH, run the following command to transform the data file to StoreFiles and store at a relative path specified by Dimporttsv.bulk.output.</span></span>  <span data-ttu-id="04e1b-163">Se si è nella shell di HBase, usare il comando exit per uscire.</span><span class="sxs-lookup"><span data-stu-id="04e1b-163">If you are in HBase Shell, use the exit command to exit.</span></span>

    ```bash   
    hbase org.apache.hadoop.hbase.mapreduce.ImportTsv -Dimporttsv.columns="HBASE_ROW_KEY,Personal:Name,Personal:Phone,Office:Phone,Office:Address" -Dimporttsv.bulk.output="/example/data/storeDataFileOutput" Contacts wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt
    ```

2. <span data-ttu-id="04e1b-164">Eseguire questo comando per caricare i dati da /example/data/storeDataFileOutput nella tabella di HBase:</span><span class="sxs-lookup"><span data-stu-id="04e1b-164">Run the following command to upload the data from  /example/data/storeDataFileOutput to the HBase table:</span></span>
   
    ```bash
    hbase org.apache.hadoop.hbase.mapreduce.LoadIncrementalHFiles /example/data/storeDataFileOutput Contacts
    ```

3. <span data-ttu-id="04e1b-165">È possibile aprire la shell HBase e usare il comando di analisi per visualizzare il contenuto della tabella.</span><span class="sxs-lookup"><span data-stu-id="04e1b-165">You can open the HBase shell, and use the scan command to list the table content.</span></span>

## <a name="use-hive-to-query-hbase"></a><span data-ttu-id="04e1b-166">Usare Hive per eseguire query su HBase</span><span class="sxs-lookup"><span data-stu-id="04e1b-166">Use Hive to query HBase</span></span>

<span data-ttu-id="04e1b-167">È possibile eseguire query sui dati nelle tabelle HBase tramite Hive.</span><span class="sxs-lookup"><span data-stu-id="04e1b-167">You can query data in HBase tables by using Hive.</span></span> <span data-ttu-id="04e1b-168">In questa sezione si crea una tabella Hive che esegue il mapping alla tabella HBase e la usa per la query dei dati nella tabella HBase.</span><span class="sxs-lookup"><span data-stu-id="04e1b-168">In this section, you create a Hive table that maps to the HBase table and uses it to query the data in your HBase table.</span></span>

1. <span data-ttu-id="04e1b-169">Aprire **PuTTY**e connettersi al cluster.</span><span class="sxs-lookup"><span data-stu-id="04e1b-169">Open **PuTTY**, and connect to the cluster.</span></span>  <span data-ttu-id="04e1b-170">Vedere le istruzioni nella procedura precedente.</span><span class="sxs-lookup"><span data-stu-id="04e1b-170">See the instructions in the previous procedure.</span></span>
2. <span data-ttu-id="04e1b-171">Nella sessione SSH usare il comando seguente per avviare Beeline:</span><span class="sxs-lookup"><span data-stu-id="04e1b-171">From the SSH session, use the following command to start Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="04e1b-172">Per altre informazioni su Beeline, vedere [Usare Hive con Hadoop in HDInsight con Beeline](hdinsight-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="04e1b-172">For more information about Beeline, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
       
3. <span data-ttu-id="04e1b-173">Eseguire il seguente script HiveQL per creare una tabella Hive mappata alla tabella HBase.</span><span class="sxs-lookup"><span data-stu-id="04e1b-173">Run the following HiveQL script  to create a Hive table that maps to the HBase table.</span></span> <span data-ttu-id="04e1b-174">Prima di eseguire questa istruzione, assicurarsi di aver creato la tabella di esempio usata precedentemente in questa esercitazione come riferimento con la shell HBase.</span><span class="sxs-lookup"><span data-stu-id="04e1b-174">Make sure that you have created the sample table referenced earlier in this tutorial by using the HBase shell before you run this statement.</span></span>

    ```hiveql   
    CREATE EXTERNAL TABLE hbasecontacts(rowkey STRING, name STRING, homephone STRING, officephone STRING, officeaddress STRING)
    STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
    WITH SERDEPROPERTIES ('hbase.columns.mapping' = ':key,Personal:Name,Personal:Phone,Office:Phone,Office:Address')
    TBLPROPERTIES ('hbase.table.name' = 'Contacts');
    ```

4. <span data-ttu-id="04e1b-175">Eseguire il seguente script HiveQL per eseguire query sui dati nella tabella HBase:</span><span class="sxs-lookup"><span data-stu-id="04e1b-175">Run the following HiveQL script to query the data in the HBase table:</span></span>

    ```hiveql   
    SELECT count(rowkey) FROM hbasecontacts;
    ```

## <a name="use-hbase-rest-apis-using-curl"></a><span data-ttu-id="04e1b-176">Usare le API REST HBase mediante Curl</span><span class="sxs-lookup"><span data-stu-id="04e1b-176">Use HBase REST APIs using Curl</span></span>

<span data-ttu-id="04e1b-177">L'API REST viene protetta tramite l' [autenticazione di base](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="04e1b-177">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="04e1b-178">Le richieste vengono sempre eseguite usando il protocollo HTTPS (Secure HTTP) per essere certi che le credenziali vengano inviate in modo sicuro al server.</span><span class="sxs-lookup"><span data-stu-id="04e1b-178">You shall always make requests by using Secure HTTP (HTTPS) to help ensure that your credentials are securely sent to the server.</span></span>

2. <span data-ttu-id="04e1b-179">Usare il comando seguente per ottenere l'elenco delle tabelle HBase esistenti:</span><span class="sxs-lookup"><span data-stu-id="04e1b-179">Use the following command to list the existing HBase tables:</span></span>

    ```bash
    curl -u <UserName>:<Password> \
    -G https://<ClusterName>.azurehdinsight.net/hbaserest/
    ```

3. <span data-ttu-id="04e1b-180">Usare il comando seguente per creare una nuova tabella HBase con famiglie di due colonne:</span><span class="sxs-lookup"><span data-stu-id="04e1b-180">Use the following command to create a new HBase table with two-column families:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/schema" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"@name\":\"Contact1\",\"ColumnSchema\":[{\"name\":\"Personal\"},{\"name\":\"Office\"}]}" \
    -v
    ```

    <span data-ttu-id="04e1b-181">Lo schema viene fornito nel formato JSON.</span><span class="sxs-lookup"><span data-stu-id="04e1b-181">The schema is provided in the JSon format.</span></span>
4. <span data-ttu-id="04e1b-182">Usare il comando seguente per inserire alcuni dati:</span><span class="sxs-lookup"><span data-stu-id="04e1b-182">Use the following command to insert some data:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/false-row-key" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"Row\":[{\"key\":\"MTAwMA==\",\"Cell\": [{\"column\":\"UGVyc29uYWw6TmFtZQ==\", \"$\":\"Sm9obiBEb2xl\"}]}]}" \
    -v
    ```
   
    <span data-ttu-id="04e1b-183">È necessario applicare la codifica base64 ai valori specificati nell'interruttore -d.</span><span class="sxs-lookup"><span data-stu-id="04e1b-183">You must base64 encode the values specified in the -d switch.</span></span> <span data-ttu-id="04e1b-184">Nell'esempio:</span><span class="sxs-lookup"><span data-stu-id="04e1b-184">In the example:</span></span>
   
   * <span data-ttu-id="04e1b-185">MTAwMA==: 1000</span><span class="sxs-lookup"><span data-stu-id="04e1b-185">MTAwMA==: 1000</span></span>
   * <span data-ttu-id="04e1b-186">UGVyc29uYWw6TmFtZQ==: Personal:Name</span><span class="sxs-lookup"><span data-stu-id="04e1b-186">UGVyc29uYWw6TmFtZQ==: Personal:Name</span></span>
   * <span data-ttu-id="04e1b-187">Sm9obiBEb2xl: John Dole</span><span class="sxs-lookup"><span data-stu-id="04e1b-187">Sm9obiBEb2xl: John Dole</span></span>
     
     <span data-ttu-id="04e1b-188">[false-row-key](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) consente di inserire più valori in batch.</span><span class="sxs-lookup"><span data-stu-id="04e1b-188">[false-row-key](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) allows you to insert multiple (batched) values.</span></span>
5. <span data-ttu-id="04e1b-189">Usare il comando seguente per ottenere una riga:</span><span class="sxs-lookup"><span data-stu-id="04e1b-189">Use the following command to get a row:</span></span>
   
    ```bash 
    curl -u <UserName>:<Password> \
    -X GET "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/1000" \
    -H "Accept: application/json" \
    -v
    ```

<span data-ttu-id="04e1b-190">Per altre informazioni sulle API REST HBase, vedere la [Apache HBase Reference Guide](https://hbase.apache.org/book.html#_rest)(Guida di riferimento di Apache HBase).</span><span class="sxs-lookup"><span data-stu-id="04e1b-190">For more information about HBase Rest, see [Apache HBase Reference Guide](https://hbase.apache.org/book.html#_rest).</span></span>

> [!NOTE]
> <span data-ttu-id="04e1b-191">Thrift non è supportato da HBase in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="04e1b-191">Thrift is not supported by HBase in HDInsight.</span></span>
>
> <span data-ttu-id="04e1b-192">Quando si usa Curl o qualsiasi altra forma di comunicazione REST con WebHCat, è necessario autenticare le richieste fornendo il nome utente e la password dell'amministratore cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="04e1b-192">When using Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span></span> <span data-ttu-id="04e1b-193">È anche necessario specificare il nome del cluster come parte dell'URI (Uniform Resource Identifier) usato per inviare le richieste al server:</span><span class="sxs-lookup"><span data-stu-id="04e1b-193">You must also use the cluster name as part of the Uniform Resource Identifier (URI) used to send the requests to the server:</span></span>
> 
>   
>        curl -u <UserName>:<Password> \
>        -G https://<ClusterName>.azurehdinsight.net/templeton/v1/status
>   
>    <span data-ttu-id="04e1b-194">Verrà visualizzato un messaggio simile alla risposta seguente:</span><span class="sxs-lookup"><span data-stu-id="04e1b-194">You should receive a response similar to the following response:</span></span>
>   
>        {"status":"ok","version":"v1"}
   


## <a name="check-cluster-status"></a><span data-ttu-id="04e1b-195">Controllare lo stato del cluster</span><span class="sxs-lookup"><span data-stu-id="04e1b-195">Check cluster status</span></span>
<span data-ttu-id="04e1b-196">HBase in HDInsight viene fornito con un'interfaccia utente Web per il monitoraggio dei cluster.</span><span class="sxs-lookup"><span data-stu-id="04e1b-196">HBase in HDInsight ships with a Web UI for monitoring clusters.</span></span> <span data-ttu-id="04e1b-197">Usando l’interfaccia Web è possibile richiedere statistiche o informazioni sulle aree.</span><span class="sxs-lookup"><span data-stu-id="04e1b-197">Using the Web UI, you can request statistics or information about regions.</span></span>

<span data-ttu-id="04e1b-198">**Per accedere all'interfaccia utente master HBase**</span><span class="sxs-lookup"><span data-stu-id="04e1b-198">**To access the HBase Master UI**</span></span>

1. <span data-ttu-id="04e1b-199">Accedere all'interfaccia utente Web Ambari all'indirizzo https://&lt;Nomecluster>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="04e1b-199">Sign into the the Ambari Web UI at https://&lt;Clustername>.azurehdinsight.net.</span></span>
2. <span data-ttu-id="04e1b-200">Fare clic su **HBase** nel menu di sinistra.</span><span class="sxs-lookup"><span data-stu-id="04e1b-200">Click **HBase** from the left menu.</span></span>
3. <span data-ttu-id="04e1b-201">Fare clic su **Quick links** (Collegamenti rapidi) nella parte superiore della pagina, scegliere il collegamento di nodo Zookeeper attivo e quindi fare clic su **HBase Master UI** (Interfaccia utente master HBase).</span><span class="sxs-lookup"><span data-stu-id="04e1b-201">Click **Quick links** on the top of the page, point to the active Zookeeper node link, and then click **HBase Master UI**.</span></span>  <span data-ttu-id="04e1b-202">L'interfaccia utente viene aperta in un'altra scheda del browser:</span><span class="sxs-lookup"><span data-stu-id="04e1b-202">The UI is opened in another browser tab:</span></span>

  ![Interfaccia utente master HBase di HDInsight](./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hmaster-ui.png)

  <span data-ttu-id="04e1b-204">L'interfaccia utente master HBase contiene le sezioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="04e1b-204">The HBase Master UI contains the following sections:</span></span>

  - <span data-ttu-id="04e1b-205">server di zona</span><span class="sxs-lookup"><span data-stu-id="04e1b-205">region servers</span></span>
  - <span data-ttu-id="04e1b-206">master di backup</span><span class="sxs-lookup"><span data-stu-id="04e1b-206">backup masters</span></span>
  - <span data-ttu-id="04e1b-207">tables</span><span class="sxs-lookup"><span data-stu-id="04e1b-207">tables</span></span>
  - <span data-ttu-id="04e1b-208">attività</span><span class="sxs-lookup"><span data-stu-id="04e1b-208">tasks</span></span>
  - <span data-ttu-id="04e1b-209">attributi di software</span><span class="sxs-lookup"><span data-stu-id="04e1b-209">software attributes</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="04e1b-210">Eliminazione del cluster</span><span class="sxs-lookup"><span data-stu-id="04e1b-210">Delete the cluster</span></span>
<span data-ttu-id="04e1b-211">Per evitare incoerenze, è consigliabile disabilitare le tabelle HBase prima di eliminare il cluster.</span><span class="sxs-lookup"><span data-stu-id="04e1b-211">To avoid inconsistencies, we recommend that you disable the HBase tables before you delete the cluster.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="04e1b-212">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="04e1b-212">Troubleshoot</span></span>

<span data-ttu-id="04e1b-213">Se si verificano problemi di creazione dei cluster HDInsight, vedere i [requisiti dei controlli di accesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="04e1b-213">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="04e1b-214">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="04e1b-214">Next steps</span></span>
<span data-ttu-id="04e1b-215">In questo articolo si è appreso come creare tabelle e un cluster HBase e come visualizzare i dati delle tabelle dalla shell HBase.</span><span class="sxs-lookup"><span data-stu-id="04e1b-215">In this article, you learned how to create an HBase cluster and how to create tables and view the data in those tables from the HBase shell.</span></span> <span data-ttu-id="04e1b-216">Si è inoltre appreso come usare una query Hive sui dati nelle tabelle HBase e come usare le API REST C# di HBase per creare una tabella HBase e recuperare i dati dalla tabella.</span><span class="sxs-lookup"><span data-stu-id="04e1b-216">You also learned how to use a Hive query on data in HBase tables and how to use the HBase C# REST APIs to create an HBase table and retrieve data from the table.</span></span>

<span data-ttu-id="04e1b-217">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="04e1b-217">To learn more, see:</span></span>

* <span data-ttu-id="04e1b-218">[Panoramica di HDInsight HBase][hdinsight-hbase-overview]: HBase è un database NoSQL open source Apache basato su Hadoop che fornisce un accesso casuale e coerenza assoluta a grandi quantità di dati non strutturati e semistrutturati.</span><span class="sxs-lookup"><span data-stu-id="04e1b-218">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>

[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hbase-reference]: http://hbase.apache.org/book.html#importtsv
[hbase-schema]: http://0b4af6cdc2f0c5998459-c0245c5c937c5dedcca3f1764ecc9b2f.r43.cf2.rackcdn.com/9353-login1210_khurana.pdf
[hbase-quick-start]: http://hbase.apache.org/book.html#quickstart





[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-versions]: hdinsight-component-versioning.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-portal]: https://portal.azure.com/
[azure-create-storageaccount]: http://azure.microsoft.com/documentation/articles/storage-create-storage-account/

[img-hdinsight-hbase-cluster-quick-create]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-quick-create.png
[img-hdinsight-hbase-hive-editor]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hive-editor.png
[img-hdinsight-hbase-file-browser]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-file-browser.png
[img-hbase-shell]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-shell.png
[img-hbase-sample-data-tabular]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-tabular.png
[img-hbase-sample-data-bigtable]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-bigtable.png
