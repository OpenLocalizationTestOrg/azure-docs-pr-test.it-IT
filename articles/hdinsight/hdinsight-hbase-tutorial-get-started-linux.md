---
title: aaaGet avviato con un esempio di HBase in HDInsight - Azure | Documenti Microsoft
description: Seguire questa toostart esempio Apache HBase con hadoop in HDInsight. Creare tabelle dalla shell di HBase hello e di eseguire le query utilizzando l'Hive.
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
ms.openlocfilehash: 43419780142b320b16180a2b1f25020dee2f7a11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-an-apache-hbase-example-in-hdinsight"></a><span data-ttu-id="3c059-105">Iniziare a usare un esempio di Apache HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="3c059-105">Get started with an Apache HBase example in HDInsight</span></span>

<span data-ttu-id="3c059-106">Informazioni su come toocreate un cluster HBase in HDInsight, creare tabelle di HBase ed eseguire query di tabelle tramite Hive.</span><span class="sxs-lookup"><span data-stu-id="3c059-106">Learn how toocreate an HBase cluster in HDInsight, create HBase tables, and query tables by using Hive.</span></span> <span data-ttu-id="3c059-107">Per informazioni generali su HBase, vedere [Panoramica di HDInsight HBase][hdinsight-hbase-overview].</span><span class="sxs-lookup"><span data-stu-id="3c059-107">For general HBase information, see [HDInsight HBase overview][hdinsight-hbase-overview].</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a><span data-ttu-id="3c059-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3c059-108">Prerequisites</span></span>
<span data-ttu-id="3c059-109">Prima di iniziare cercando in questo esempio di HBase, è necessario disporre di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="3c059-109">Before you begin trying this HBase example, you must have hello following items:</span></span>

* <span data-ttu-id="3c059-110">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="3c059-110">**An Azure subscription**.</span></span> <span data-ttu-id="3c059-111">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="3c059-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="3c059-112">[Secure Shell (SSH)](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="3c059-112">[Secure Shell(SSH)](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> 
* <span data-ttu-id="3c059-113">[curl](http://curl.haxx.se/download.html).</span><span class="sxs-lookup"><span data-stu-id="3c059-113">[curl](http://curl.haxx.se/download.html).</span></span>

## <a name="create-hbase-cluster"></a><span data-ttu-id="3c059-114">Nome del cluster HBase</span><span class="sxs-lookup"><span data-stu-id="3c059-114">Create HBase cluster</span></span>
<span data-ttu-id="3c059-115">Hello procedura riportata di seguito utilizza un toocreate modello di gestione risorse di Azure una versione 3.4 HBase basati su Linux cluster e hello dipendenti di archiviazione di Azure account predefinito.</span><span class="sxs-lookup"><span data-stu-id="3c059-115">hello following procedure uses an Azure Resource Manager template toocreate a version 3.4 Linux-based HBase cluster and hello dependent default Azure Storage account.</span></span> <span data-ttu-id="3c059-116">parametri di hello toounderstand utilizzati nella procedura hello e altri metodi di creazione del cluster, vedere [cluster basati su Linux creare Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="3c059-116">toounderstand hello parameters used in hello procedure and other cluster creation methods, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="3c059-117">Fare clic su hello seguente immagine tooopen hello modello hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3c059-117">Click hello following image tooopen hello template in hello Azure portal.</span></span> <span data-ttu-id="3c059-118">Hello modello si trova in un contenitore di blob pubblici.</span><span class="sxs-lookup"><span data-stu-id="3c059-118">hello template is located in a public blob container.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-tutorial-get-started-linux/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="3c059-119">Da hello **distribuzione personalizzata** pannello immettere hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="3c059-119">From hello **Custom deployment** blade, enter hello following values:</span></span>
   
   * <span data-ttu-id="3c059-120">**Sottoscrizione**: selezionare la sottoscrizione di Azure che è usato toocreate hello cluster.</span><span class="sxs-lookup"><span data-stu-id="3c059-120">**Subscription**: Select your Azure subscription that is used toocreate hello cluster.</span></span>
   * <span data-ttu-id="3c059-121">**Gruppo di risorse**: creare un nuovo gruppo di Azure Resource Manager o usarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="3c059-121">**Resource group**: Create an Azure Resource Management group or use an existing one.</span></span>
   * <span data-ttu-id="3c059-122">**Percorso**: specificare il percorso di hello hello del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="3c059-122">**Location**: Specify hello location of hello resource group.</span></span> 
   * <span data-ttu-id="3c059-123">**ClusterName**: immettere un nome per il cluster di HBase hello.</span><span class="sxs-lookup"><span data-stu-id="3c059-123">**ClusterName**: Enter a name for hello HBase cluster.</span></span>
   * <span data-ttu-id="3c059-124">**Nome account di accesso e la password del cluster**: nome di account di accesso predefinito hello **admin**.</span><span class="sxs-lookup"><span data-stu-id="3c059-124">**Cluster login name and password**: hello default login name is **admin**.</span></span>
   * <span data-ttu-id="3c059-125">**Nome utente SSH e password**: nome utente predefinito hello **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="3c059-125">**SSH username and password**: hello default username is **sshuser**.</span></span>  <span data-ttu-id="3c059-126">È possibile rinominarlo.</span><span class="sxs-lookup"><span data-stu-id="3c059-126">You can rename it.</span></span>
     
     <span data-ttu-id="3c059-127">Gli altri parametri sono facoltativi.</span><span class="sxs-lookup"><span data-stu-id="3c059-127">Other parameters are optional.</span></span>  
     
     <span data-ttu-id="3c059-128">Ogni cluster ha una dipendenza dall'account di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3c059-128">Each cluster has an Azure Storage account dependency.</span></span> <span data-ttu-id="3c059-129">Dopo l'eliminazione di un cluster, i dati di hello mantengono nell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="3c059-129">After you delete a cluster, hello data retains in hello storage account.</span></span> <span data-ttu-id="3c059-130">nome dell'account di archiviazione di Hello cluster predefinito è il nome del cluster hello "archivio" aggiunto.</span><span class="sxs-lookup"><span data-stu-id="3c059-130">hello cluster default storage account name is hello cluster name with "store" appended.</span></span> <span data-ttu-id="3c059-131">È hardcoded nella sezione di hello modello variabili.</span><span class="sxs-lookup"><span data-stu-id="3c059-131">It is hardcoded in hello template variables section.</span></span>
3. <span data-ttu-id="3c059-132">Selezionare **accetto le condizioni indicate in precedenza toohello**, quindi fare clic su **acquisto**.</span><span class="sxs-lookup"><span data-stu-id="3c059-132">Select **I agree toohello terms and conditions stated above**, and then click **Purchase**.</span></span> <span data-ttu-id="3c059-133">Sono necessari circa 20 minuti toocreate un cluster.</span><span class="sxs-lookup"><span data-stu-id="3c059-133">It takes about 20 minutes toocreate a cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="3c059-134">Dopo l'eliminazione di un cluster HBase, è possibile creare un altro cluster HBase tramite hello stesso contenitore di blob predefinito.</span><span class="sxs-lookup"><span data-stu-id="3c059-134">After an HBase cluster is deleted, you can create another HBase cluster by using hello same default blob container.</span></span> <span data-ttu-id="3c059-135">il nuovo cluster di Hello preleva da tabelle di HBase hello creato nel cluster originale hello.</span><span class="sxs-lookup"><span data-stu-id="3c059-135">hello new cluster picks up hello HBase tables you created in hello original cluster.</span></span> <span data-ttu-id="3c059-136">tooavoid incoerenze, è consigliabile disabilitare le tabelle di hello HBase prima di eliminare il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="3c059-136">tooavoid inconsistencies, we recommend that you disable hello HBase tables before you delete hello cluster.</span></span>
> 
> 

## <a name="create-tables-and-insert-data"></a><span data-ttu-id="3c059-137">Creare tabelle e inserire dati</span><span class="sxs-lookup"><span data-stu-id="3c059-137">Create tables and insert data</span></span>
<span data-ttu-id="3c059-138">È possibile utilizzare SSH tooconnect tooHBase cluster e utilizzare la Shell di HBase toocreate HBase tabelle, inserire i dati e i dati di query.</span><span class="sxs-lookup"><span data-stu-id="3c059-138">You can use SSH tooconnect tooHBase clusters and then use HBase Shell toocreate HBase tables, insert data, and query data.</span></span> <span data-ttu-id="3c059-139">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="3c059-139">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="3c059-140">Per la maggior parte degli utenti, i dati vengono visualizzati in formato tabulare hello:</span><span class="sxs-lookup"><span data-stu-id="3c059-140">For most people, data appears in hello tabular format:</span></span>

![Tabella con dati HBase di HDInsight][img-hbase-sample-data-tabular]

<span data-ttu-id="3c059-142">In HBase (un'implementazione di BigTable), hello stesso dati ha un aspetto simile:</span><span class="sxs-lookup"><span data-stu-id="3c059-142">In HBase (an implementation of BigTable), hello same data looks like:</span></span>

![Dati BigTable HBase di HDInsight][img-hbase-sample-data-bigtable]


<span data-ttu-id="3c059-144">**hello toouse shell di HBase**</span><span class="sxs-lookup"><span data-stu-id="3c059-144">**toouse hello HBase shell**</span></span>

1. <span data-ttu-id="3c059-145">Da SSH, eseguire hello HBase comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3c059-145">From SSH, run hello following HBase command:</span></span>
   
    ```bash
    hbase shell
    ```

2. <span data-ttu-id="3c059-146">Creare un HBase con famiglie di due colonne:</span><span class="sxs-lookup"><span data-stu-id="3c059-146">Create an HBase with two-column families:</span></span>

    ```hbaseshell   
    create 'Contacts', 'Personal', 'Office'
    list
    ```
3. <span data-ttu-id="3c059-147">Inserire alcuni dati:</span><span class="sxs-lookup"><span data-stu-id="3c059-147">Insert some data:</span></span>
    
    ```hbaseshell   
    put 'Contacts', '1000', 'Personal:Name', 'John Dole'
    put 'Contacts', '1000', 'Personal:Phone', '1-425-000-0001'
    put 'Contacts', '1000', 'Office:Phone', '1-425-000-0002'
    put 'Contacts', '1000', 'Office:Address', '1111 San Gabriel Dr.'
    scan 'Contacts'
    ```
   
    ![Shell HBase Hadoop di HDInsight][img-hbase-shell]
4. <span data-ttu-id="3c059-149">Ottenere una singola riga</span><span class="sxs-lookup"><span data-stu-id="3c059-149">Get a single row</span></span>
   
    ```hbaseshell
    get 'Contacts', '1000'
    ```
   
    <span data-ttu-id="3c059-150">Hello stesso risultati verrà visualizzato come tramite comando analisi hello perché è presente solo una riga.</span><span class="sxs-lookup"><span data-stu-id="3c059-150">You shall see hello same results as using hello scan command because there is only one row.</span></span>
   
    <span data-ttu-id="3c059-151">Per ulteriori informazioni sullo schema di tabella HBase hello, vedere [tooHBase introduzione progettazione Schema][hbase-schema].</span><span class="sxs-lookup"><span data-stu-id="3c059-151">For more information about hello HBase table schema, see [Introduction tooHBase Schema Design][hbase-schema].</span></span> <span data-ttu-id="3c059-152">Per altri comandi HBase, vedere la [guida di riferimento di Apache HBase][hbase-quick-start].</span><span class="sxs-lookup"><span data-stu-id="3c059-152">For more HBase commands, see [Apache HBase reference guide][hbase-quick-start].</span></span>
5. <span data-ttu-id="3c059-153">Uscire dalla shell hello</span><span class="sxs-lookup"><span data-stu-id="3c059-153">Exit hello shell</span></span>
   
    ```hbaseshell
    exit
    ```

<span data-ttu-id="3c059-154">**toobulk caricare i dati nella tabella HBase di hello contatti**</span><span class="sxs-lookup"><span data-stu-id="3c059-154">**toobulk load data into hello contacts HBase table**</span></span>

<span data-ttu-id="3c059-155">HBase include diversi metodi di caricamento dei dati nelle tabelle.</span><span class="sxs-lookup"><span data-stu-id="3c059-155">HBase includes several methods of loading data into tables.</span></span>  <span data-ttu-id="3c059-156">Per altre informazioni, vedere [Caricamento bulk](http://hbase.apache.org/book.html#arch.bulk.load).</span><span class="sxs-lookup"><span data-stu-id="3c059-156">For more information, see [Bulk loading](http://hbase.apache.org/book.html#arch.bulk.load).</span></span>

<span data-ttu-id="3c059-157">Un file di dati di esempio è disponibile in un contenitore BLOB pubblico, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span><span class="sxs-lookup"><span data-stu-id="3c059-157">A sample data file can be found in a public blob container, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span></span>  <span data-ttu-id="3c059-158">è contenuto Hello hello del file di dati:</span><span class="sxs-lookup"><span data-stu-id="3c059-158">hello content of hello data file is:</span></span>

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

<span data-ttu-id="3c059-159">Facoltativamente, è possibile creare un file di testo e caricare l'account di archiviazione propria tooyour file hello.</span><span class="sxs-lookup"><span data-stu-id="3c059-159">You can optionally create a text file and upload hello file tooyour own storage account.</span></span> <span data-ttu-id="3c059-160">Per istruzioni hello, vedere [caricare dati per i processi di Hadoop in HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="3c059-160">For hello instructions, see [Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data].</span></span>

> [!NOTE]
> <span data-ttu-id="3c059-161">Questa procedura utilizza una tabella HBase contatti hello creata nell'ultima procedura hello.</span><span class="sxs-lookup"><span data-stu-id="3c059-161">This procedure uses hello Contacts HBase table you have created in hello last procedure.</span></span>
> 

1. <span data-ttu-id="3c059-162">SSH, eseguire hello successivo comando tootransform hello tooStoreFiles del file di dati e archiviano in un percorso relativo specificato da Dimporttsv.bulk.output.</span><span class="sxs-lookup"><span data-stu-id="3c059-162">From SSH, run hello following command tootransform hello data file tooStoreFiles and store at a relative path specified by Dimporttsv.bulk.output.</span></span>  <span data-ttu-id="3c059-163">Se si utilizza la Shell di HBase, utilizzare hello uscita comando tooexit.</span><span class="sxs-lookup"><span data-stu-id="3c059-163">If you are in HBase Shell, use hello exit command tooexit.</span></span>

    ```bash   
    hbase org.apache.hadoop.hbase.mapreduce.ImportTsv -Dimporttsv.columns="HBASE_ROW_KEY,Personal:Name,Personal:Phone,Office:Phone,Office:Address" -Dimporttsv.bulk.output="/example/data/storeDataFileOutput" Contacts wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt
    ```

2. <span data-ttu-id="3c059-164">Eseguire i seguenti dati di comando tooupload hello dalla tabella di HBase toohello /example/data/storeDataFileOutput hello:</span><span class="sxs-lookup"><span data-stu-id="3c059-164">Run hello following command tooupload hello data from  /example/data/storeDataFileOutput toohello HBase table:</span></span>
   
    ```bash
    hbase org.apache.hadoop.hbase.mapreduce.LoadIncrementalHFiles /example/data/storeDataFileOutput Contacts
    ```

3. <span data-ttu-id="3c059-165">È possibile aprire la shell di HBase hello e utilizzare il contenuto delle tabelle hello hello analisi comando toolist.</span><span class="sxs-lookup"><span data-stu-id="3c059-165">You can open hello HBase shell, and use hello scan command toolist hello table content.</span></span>

## <a name="use-hive-tooquery-hbase"></a><span data-ttu-id="3c059-166">Usare l'Hive tooquery HBase</span><span class="sxs-lookup"><span data-stu-id="3c059-166">Use Hive tooquery HBase</span></span>

<span data-ttu-id="3c059-167">È possibile eseguire query sui dati nelle tabelle HBase tramite Hive.</span><span class="sxs-lookup"><span data-stu-id="3c059-167">You can query data in HBase tables by using Hive.</span></span> <span data-ttu-id="3c059-168">In questa sezione si crea una tabella Hive che esegue il mapping di tabella HBase toohello e lo Usa dati hello tooquery nella tabella HBase.</span><span class="sxs-lookup"><span data-stu-id="3c059-168">In this section, you create a Hive table that maps toohello HBase table and uses it tooquery hello data in your HBase table.</span></span>

1. <span data-ttu-id="3c059-169">Aprire **PuTTY**e connettersi toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="3c059-169">Open **PuTTY**, and connect toohello cluster.</span></span>  <span data-ttu-id="3c059-170">Vedere le istruzioni di hello nella procedura precedente hello.</span><span class="sxs-lookup"><span data-stu-id="3c059-170">See hello instructions in hello previous procedure.</span></span>
2. <span data-ttu-id="3c059-171">Dalla sessione SSH hello, utilizzare hello comando toostart Beeline seguenti:</span><span class="sxs-lookup"><span data-stu-id="3c059-171">From hello SSH session, use hello following command toostart Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="3c059-172">Per altre informazioni su Beeline, vedere [Usare Hive con Hadoop in HDInsight con Beeline](hdinsight-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="3c059-172">For more information about Beeline, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
       
3. <span data-ttu-id="3c059-173">Eseguire hello toocreate script HiveQL seguente una tabella Hive che esegue il mapping di tabella HBase toohello.</span><span class="sxs-lookup"><span data-stu-id="3c059-173">Run hello following HiveQL script  toocreate a Hive table that maps toohello HBase table.</span></span> <span data-ttu-id="3c059-174">Assicurarsi di aver creato una tabella di esempio hello a cui fa riferimento in precedenza in questa esercitazione utilizzando la shell di HBase hello prima di eseguire questa istruzione.</span><span class="sxs-lookup"><span data-stu-id="3c059-174">Make sure that you have created hello sample table referenced earlier in this tutorial by using hello HBase shell before you run this statement.</span></span>

    ```hiveql   
    CREATE EXTERNAL TABLE hbasecontacts(rowkey STRING, name STRING, homephone STRING, officephone STRING, officeaddress STRING)
    STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
    WITH SERDEPROPERTIES ('hbase.columns.mapping' = ':key,Personal:Name,Personal:Phone,Office:Phone,Office:Address')
    TBLPROPERTIES ('hbase.table.name' = 'Contacts');
    ```

4. <span data-ttu-id="3c059-175">Eseguire hello HiveQL script tooquery hello dati nella tabella HBase hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="3c059-175">Run hello following HiveQL script tooquery hello data in hello HBase table:</span></span>

    ```hiveql   
    SELECT count(rowkey) FROM hbasecontacts;
    ```

## <a name="use-hbase-rest-apis-using-curl"></a><span data-ttu-id="3c059-176">Usare le API REST HBase mediante Curl</span><span class="sxs-lookup"><span data-stu-id="3c059-176">Use HBase REST APIs using Curl</span></span>

<span data-ttu-id="3c059-177">Hello API REST è protetto tramite [l'autenticazione di base](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="3c059-177">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="3c059-178">È sempre deve effettuare richieste tramite HTTPS (Secure HTTP) toohelp assicurarsi che le credenziali vengono inviate in modo sicuro toohello server.</span><span class="sxs-lookup"><span data-stu-id="3c059-178">You shall always make requests by using Secure HTTP (HTTPS) toohelp ensure that your credentials are securely sent toohello server.</span></span>

2. <span data-ttu-id="3c059-179">Utilizzare hello comando toolist hello HBase le tabelle esistenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="3c059-179">Use hello following command toolist hello existing HBase tables:</span></span>

    ```bash
    curl -u <UserName>:<Password> \
    -G https://<ClusterName>.azurehdinsight.net/hbaserest/
    ```

3. <span data-ttu-id="3c059-180">Utilizzare hello comando toocreate una nuova tabella HBase con gruppi di due colonne seguenti:</span><span class="sxs-lookup"><span data-stu-id="3c059-180">Use hello following command toocreate a new HBase table with two-column families:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/schema" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"@name\":\"Contact1\",\"ColumnSchema\":[{\"name\":\"Personal\"},{\"name\":\"Office\"}]}" \
    -v
    ```

    <span data-ttu-id="3c059-181">schema Hello viene fornito in formato JSon hello.</span><span class="sxs-lookup"><span data-stu-id="3c059-181">hello schema is provided in hello JSon format.</span></span>
4. <span data-ttu-id="3c059-182">Utilizzare hello comando che segue tooinsert alcuni dati:</span><span class="sxs-lookup"><span data-stu-id="3c059-182">Use hello following command tooinsert some data:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/false-row-key" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"Row\":[{\"key\":\"MTAwMA==\",\"Cell\": [{\"column\":\"UGVyc29uYWw6TmFtZQ==\", \"$\":\"Sm9obiBEb2xl\"}]}]}" \
    -v
    ```
   
    <span data-ttu-id="3c059-183">È necessario base64 codificare i valori hello specificati nell'opzione -d hello.</span><span class="sxs-lookup"><span data-stu-id="3c059-183">You must base64 encode hello values specified in hello -d switch.</span></span> <span data-ttu-id="3c059-184">Nell'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="3c059-184">In hello example:</span></span>
   
   * <span data-ttu-id="3c059-185">MTAwMA==: 1000</span><span class="sxs-lookup"><span data-stu-id="3c059-185">MTAwMA==: 1000</span></span>
   * <span data-ttu-id="3c059-186">UGVyc29uYWw6TmFtZQ==: Personal:Name</span><span class="sxs-lookup"><span data-stu-id="3c059-186">UGVyc29uYWw6TmFtZQ==: Personal:Name</span></span>
   * <span data-ttu-id="3c059-187">Sm9obiBEb2xl: John Dole</span><span class="sxs-lookup"><span data-stu-id="3c059-187">Sm9obiBEb2xl: John Dole</span></span>
     
     <span data-ttu-id="3c059-188">[chiave di riga false](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) tooinsert consente più valori (batch).</span><span class="sxs-lookup"><span data-stu-id="3c059-188">[false-row-key](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) allows you tooinsert multiple (batched) values.</span></span>
5. <span data-ttu-id="3c059-189">Utilizzare hello tooget comando una riga seguente:</span><span class="sxs-lookup"><span data-stu-id="3c059-189">Use hello following command tooget a row:</span></span>
   
    ```bash 
    curl -u <UserName>:<Password> \
    -X GET "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/1000" \
    -H "Accept: application/json" \
    -v
    ```

<span data-ttu-id="3c059-190">Per altre informazioni sulle API REST HBase, vedere la [Apache HBase Reference Guide](https://hbase.apache.org/book.html#_rest)(Guida di riferimento di Apache HBase).</span><span class="sxs-lookup"><span data-stu-id="3c059-190">For more information about HBase Rest, see [Apache HBase Reference Guide](https://hbase.apache.org/book.html#_rest).</span></span>

> [!NOTE]
> <span data-ttu-id="3c059-191">Thrift non è supportato da HBase in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3c059-191">Thrift is not supported by HBase in HDInsight.</span></span>
>
> <span data-ttu-id="3c059-192">Quando si utilizza Curl o qualsiasi altra comunicazione REST con WebHCat, è necessario autenticare le richieste di hello specificando nome utente hello e la password per l'amministratore del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="3c059-192">When using Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span> <span data-ttu-id="3c059-193">Inoltre, è necessario utilizzare il nome del cluster hello come parte di hello Uniform Resource Identifier (URI) utilizzato toosend hello richieste toohello server:</span><span class="sxs-lookup"><span data-stu-id="3c059-193">You must also use hello cluster name as part of hello Uniform Resource Identifier (URI) used toosend hello requests toohello server:</span></span>
> 
>   
>        curl -u <UserName>:<Password> \
>        -G https://<ClusterName>.azurehdinsight.net/templeton/v1/status
>   
>    <span data-ttu-id="3c059-194">Si dovrebbe ricevere un toohello simile di risposta seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="3c059-194">You should receive a response similar toohello following response:</span></span>
>   
>        {"status":"ok","version":"v1"}
   


## <a name="check-cluster-status"></a><span data-ttu-id="3c059-195">Controllare lo stato del cluster</span><span class="sxs-lookup"><span data-stu-id="3c059-195">Check cluster status</span></span>
<span data-ttu-id="3c059-196">HBase in HDInsight viene fornito con un'interfaccia utente Web per il monitoraggio dei cluster.</span><span class="sxs-lookup"><span data-stu-id="3c059-196">HBase in HDInsight ships with a Web UI for monitoring clusters.</span></span> <span data-ttu-id="3c059-197">Utilizza hello dell'interfaccia utente Web, è possibile richiedere informazioni sulle aree o le statistiche.</span><span class="sxs-lookup"><span data-stu-id="3c059-197">Using hello Web UI, you can request statistics or information about regions.</span></span>

<span data-ttu-id="3c059-198">**hello tooaccess UI Master HBase**</span><span class="sxs-lookup"><span data-stu-id="3c059-198">**tooaccess hello HBase Master UI**</span></span>

1. <span data-ttu-id="3c059-199">Sign in hello hello dell'interfaccia utente Web Ambari in https://&lt;Clustername >. cluster>.azurehdinsight.NET.</span><span class="sxs-lookup"><span data-stu-id="3c059-199">Sign into hello hello Ambari Web UI at https://&lt;Clustername>.azurehdinsight.net.</span></span>
2. <span data-ttu-id="3c059-200">Fare clic su **HBase** dal menu a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="3c059-200">Click **HBase** from hello left menu.</span></span>
3. <span data-ttu-id="3c059-201">Fare clic su **collegamenti rapidi** nella parte superiore della pagina hello toohello punto attivo Zookeeper nodo collegamento, hello e quindi fare clic su **HBase Master UI**.</span><span class="sxs-lookup"><span data-stu-id="3c059-201">Click **Quick links** on hello top of hello page, point toohello active Zookeeper node link, and then click **HBase Master UI**.</span></span>  <span data-ttu-id="3c059-202">Hello dell'interfaccia utente viene aperto in un'altra scheda del browser:</span><span class="sxs-lookup"><span data-stu-id="3c059-202">hello UI is opened in another browser tab:</span></span>

  ![Interfaccia utente master HBase di HDInsight](./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hmaster-ui.png)

  <span data-ttu-id="3c059-204">Hello UI HBase Master contiene hello le sezioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="3c059-204">hello HBase Master UI contains hello following sections:</span></span>

  - <span data-ttu-id="3c059-205">server di zona</span><span class="sxs-lookup"><span data-stu-id="3c059-205">region servers</span></span>
  - <span data-ttu-id="3c059-206">master di backup</span><span class="sxs-lookup"><span data-stu-id="3c059-206">backup masters</span></span>
  - <span data-ttu-id="3c059-207">tables</span><span class="sxs-lookup"><span data-stu-id="3c059-207">tables</span></span>
  - <span data-ttu-id="3c059-208">attività</span><span class="sxs-lookup"><span data-stu-id="3c059-208">tasks</span></span>
  - <span data-ttu-id="3c059-209">attributi di software</span><span class="sxs-lookup"><span data-stu-id="3c059-209">software attributes</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="3c059-210">Eliminare il cluster hello</span><span class="sxs-lookup"><span data-stu-id="3c059-210">Delete hello cluster</span></span>
<span data-ttu-id="3c059-211">tooavoid incoerenze, è consigliabile disabilitare le tabelle di hello HBase prima di eliminare il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="3c059-211">tooavoid inconsistencies, we recommend that you disable hello HBase tables before you delete hello cluster.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="3c059-212">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="3c059-212">Troubleshoot</span></span>

<span data-ttu-id="3c059-213">Se si verificano problemi di creazione dei cluster HDInsight, vedere i [requisiti dei controlli di accesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="3c059-213">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c059-214">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3c059-214">Next steps</span></span>
<span data-ttu-id="3c059-215">In questo articolo è stato illustrato come un cluster HBase toocreate e come visualizzare e tabelle toocreate hello dati in tali tabelle da hello shell di HBase.</span><span class="sxs-lookup"><span data-stu-id="3c059-215">In this article, you learned how toocreate an HBase cluster and how toocreate tables and view hello data in those tables from hello HBase shell.</span></span> <span data-ttu-id="3c059-216">È stato inoltre descritto come toouse un Hive eseguire query sui dati in HBase tabelle e come toouse hello toocreate HBase in c# le API REST di una tabella HBase e recuperare dati dalla tabella di hello.</span><span class="sxs-lookup"><span data-stu-id="3c059-216">You also learned how toouse a Hive query on data in HBase tables and how toouse hello HBase C# REST APIs toocreate an HBase table and retrieve data from hello table.</span></span>

<span data-ttu-id="3c059-217">toolearn informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="3c059-217">toolearn more, see:</span></span>

* <span data-ttu-id="3c059-218">[Panoramica di HDInsight HBase][hdinsight-hbase-overview]: HBase è un database NoSQL open source Apache basato su Hadoop che fornisce un accesso casuale e coerenza assoluta a grandi quantità di dati non strutturati e semistrutturati.</span><span class="sxs-lookup"><span data-stu-id="3c059-218">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>

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
