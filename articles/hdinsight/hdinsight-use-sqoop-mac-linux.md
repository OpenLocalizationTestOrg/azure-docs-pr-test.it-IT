---
title: aaaApache Sqoop con Hadoop - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come toouse tooimport Sqoop Apache e l'esportazione tra Hadoop in HDInsight e un Database di SQL Azure.
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
author: Blackmist
tags: azure-portal
keywords: hadoop sqoop, sqoop
ms.assetid: 303649a5-4be5-4933-bf1d-4b232083c354
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: b256285659bbcf18ff05e220ccdf51c21eb8fbf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-sqoop-tooimport-and-export-data-between-hadoop-on-hdinsight-and-sql-database"></a><span data-ttu-id="9e487-104">Utilizzare Apache Sqoop tooimport ed esportare dati tra Hadoop in HDInsight e il Database SQL</span><span class="sxs-lookup"><span data-stu-id="9e487-104">Use Apache Sqoop tooimport and export data between Hadoop on HDInsight and SQL Database</span></span>

[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="9e487-105">Informazioni su come toouse Sqoop Apache tooimport ed esportazione tra un Hadoop cluster HDInsight di Azure e Database di SQL Azure o Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9e487-105">Learn how toouse Apache Sqoop tooimport and export between a Hadoop cluster in Azure HDInsight and Azure SQL Database or Microsoft SQL Server database.</span></span> <span data-ttu-id="9e487-106">passaggi di Hello hello di utilizzare questo documento `sqoop` direttamente dal nodo head hello del cluster Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="9e487-106">hello steps in this document use hello `sqoop` command directly from hello headnode of hello Hadoop cluster.</span></span> <span data-ttu-id="9e487-107">Nodo head di SSH tooconnect toohello e di eseguire comandi hello in questo documento.</span><span class="sxs-lookup"><span data-stu-id="9e487-107">You use SSH tooconnect toohello head node and run hello commands in this document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9e487-108">Hello passaggi descritti in questo documento funzionano solo con i cluster HDInsight che utilizzano Linux.</span><span class="sxs-lookup"><span data-stu-id="9e487-108">hello steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="9e487-109">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="9e487-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9e487-110">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="9e487-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="install-freetds"></a><span data-ttu-id="9e487-111">Installare FreeTDS</span><span class="sxs-lookup"><span data-stu-id="9e487-111">Install FreeTDS</span></span>

1. <span data-ttu-id="9e487-112">Utilizzare cluster di HDInsight toohello tooconnect SSH.</span><span class="sxs-lookup"><span data-stu-id="9e487-112">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="9e487-113">Ad esempio, hello comando seguente si connette toohello nodo head primario di un cluster denominato `mycluster`:</span><span class="sxs-lookup"><span data-stu-id="9e487-113">For example, hello following command connects toohello primary headnode of a cluster named `mycluster`:</span></span>

    ```bash
    ssh CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="9e487-114">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="9e487-114">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="9e487-115">Utilizzare hello tooinstall comando disporre di FreeTDS seguenti:</span><span class="sxs-lookup"><span data-stu-id="9e487-115">Use hello following command tooinstall FreeTDS:</span></span>

    ```bash
    sudo apt --assume-yes install freetds-dev freetds-bin
    ```

    <span data-ttu-id="9e487-116">Disporre di FreeTDS viene usato in vari passaggi tooconnect tooSQL Database.</span><span class="sxs-lookup"><span data-stu-id="9e487-116">FreeTDS is used in several steps tooconnect tooSQL Database.</span></span>

## <a name="create-hello-table-in-sql-database"></a><span data-ttu-id="9e487-117">Creare la tabella hello nel Database SQL</span><span class="sxs-lookup"><span data-stu-id="9e487-117">Create hello table in SQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9e487-118">Se si utilizza il cluster di HDInsight hello e Database SQL creato nel [creare cluster e il database SQL](hdinsight-use-sqoop.md), ignorare i passaggi di hello in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="9e487-118">If you are using hello HDInsight cluster and SQL Database created in [Create cluster and SQL database](hdinsight-use-sqoop.md), skip hello steps in this section.</span></span> <span data-ttu-id="9e487-119">Hello database e tabella sono stati creati i passaggi da parte di hello in hello [creare cluster e il database SQL](hdinsight-use-sqoop.md) documento.</span><span class="sxs-lookup"><span data-stu-id="9e487-119">hello database and table were created as part of hello steps in hello [Create cluster and SQL database](hdinsight-use-sqoop.md) document.</span></span>

1. <span data-ttu-id="9e487-120">Dalla sessione SSH hello, utilizzare hello seguente server di Database SQL toohello tooconnect comando.</span><span class="sxs-lookup"><span data-stu-id="9e487-120">From hello SSH session, use hello following command tooconnect toohello SQL Database server.</span></span>

        TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D sqooptest

    <span data-ttu-id="9e487-121">Viene visualizzato toohello simili di output il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="9e487-121">You receive output similar toohello following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toosqooptest
        1>

2. <span data-ttu-id="9e487-122">In hello `1>` richiesto, immettere hello seguente query:</span><span class="sxs-lookup"><span data-stu-id="9e487-122">At hello `1>` prompt, enter hello following query:</span></span>

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)
    GO
    ```

    <span data-ttu-id="9e487-123">Quando hello `GO` istruzione viene immessa, le istruzioni precedenti hello vengono valutate.</span><span class="sxs-lookup"><span data-stu-id="9e487-123">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="9e487-124">In primo luogo, hello **mobiledata** viene creata una tabella, quindi un indice cluster viene aggiunto tooit (obbligatorio dal Database SQL).</span><span class="sxs-lookup"><span data-stu-id="9e487-124">First, hello **mobiledata** table is created, then a clustered index is added tooit (required by SQL Database.)</span></span>

    <span data-ttu-id="9e487-125">Hello utilizzare query tooverify che hello nella tabella seguente è stata creata:</span><span class="sxs-lookup"><span data-stu-id="9e487-125">Use hello following query tooverify that hello table has been created:</span></span>

    ```sql
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="9e487-126">Vedrai toohello simili di output il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="9e487-126">You see output similar toohello following text:</span></span>

        TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
        sqooptest       dbo     mobiledata      BASE TABLE

3. <span data-ttu-id="9e487-127">Immettere `exit` in hello `1>` richiedere utilità di tooexit hello tsql.</span><span class="sxs-lookup"><span data-stu-id="9e487-127">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="sqoop-export"></a><span data-ttu-id="9e487-128">Esportazione con Sqoop</span><span class="sxs-lookup"><span data-stu-id="9e487-128">Sqoop export</span></span>

1. <span data-ttu-id="9e487-129">Da cluster toohello connessione SSH hello utilizzare hello successivo comando tooverify che Sqoop possa vedere il Database SQL:</span><span class="sxs-lookup"><span data-stu-id="9e487-129">From hello SSH connection toohello cluster, use hello following command tooverify that Sqoop can see your SQL Database:</span></span>

    ```bash
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> -P
    ```
    <span data-ttu-id="9e487-130">Quando richiesto, immettere la password di hello per l'accesso al Database SQL hello.</span><span class="sxs-lookup"><span data-stu-id="9e487-130">When prompted, enter hello password for hello SQL Database login.</span></span>

    <span data-ttu-id="9e487-131">Questo comando restituisce un elenco di database, tra cui hello **sqooptest** database creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9e487-131">This command returns a list of databases, including hello **sqooptest** database that you created earlier.</span></span>

2. <span data-ttu-id="9e487-132">dati tooexport **hivesampletable** toohello **mobiledata** tabella, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9e487-132">tooexport data from **hivesampletable** toohello **mobiledata** table, use hello following command:</span></span>

    ```bash
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> -P --table 'mobiledata' --export-dir 'wasb:///hive/warehouse/hivesampletable' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="9e487-133">Questo comando indica Sqoop tooconnect toohello **sqooptest** database.</span><span class="sxs-lookup"><span data-stu-id="9e487-133">This command instructs Sqoop tooconnect toohello **sqooptest** database.</span></span> <span data-ttu-id="9e487-134">Sqoop quindi Esporta dati da **wasb: / / / hive/warehouse/hivesampletable** toohello **mobiledata** tabella.</span><span class="sxs-lookup"><span data-stu-id="9e487-134">Sqoop then exports data from **wasb:///hive/warehouse/hivesampletable** toohello **mobiledata** table.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="9e487-135">Utilizzare `wasb:///` se hello predefinito per il cluster è un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="9e487-135">Use `wasb:///` if hello default storage for your cluster is an Azure Storage account.</span></span> <span data-ttu-id="9e487-136">Usare `adl:///` se è un Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="9e487-136">Use `adl:///` if it is an Azure Data Lake Store.</span></span>

3. <span data-ttu-id="9e487-137">Al termine del comando hello, usare hello database toohello tooconnect di comando tramite TSQL seguente:</span><span class="sxs-lookup"><span data-stu-id="9e487-137">After hello command completes, use hello following command tooconnect toohello database using TSQL:</span></span>

    ```bash
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P -p 1433 -D sqooptest
    ```

    <span data-ttu-id="9e487-138">Una volta connessi, utilizzare hello seguente tooverify istruzioni che hello dati è stato esportato toohello **mobiledata** tabella:</span><span class="sxs-lookup"><span data-stu-id="9e487-138">Once connected, use hello following statements tooverify that hello data was exported toohello **mobiledata** table:</span></span>

    ```sql
    SET ROWCOUNT 50;
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="9e487-139">Verrà visualizzato un elenco di dati nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="9e487-139">You should see a listing of data in hello table.</span></span> <span data-ttu-id="9e487-140">Tipo `exit` utilità di tooexit hello tsql.</span><span class="sxs-lookup"><span data-stu-id="9e487-140">Type `exit` tooexit hello tsql utility.</span></span>

## <a name="sqoop-import"></a><span data-ttu-id="9e487-141">Importazione con Sqoop</span><span class="sxs-lookup"><span data-stu-id="9e487-141">Sqoop import</span></span>

1. <span data-ttu-id="9e487-142">Comando che segue hello di utilizzare dati tooimport hello **mobiledata** tabella nel Database SQL, toohello **wasb: / / / esercitazioni/usesqoop/importeddata** directory HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9e487-142">Use hello following command tooimport data from hello **mobiledata** table in SQL Database, toohello **wasb:///tutorials/usesqoop/importeddata** directory on HDInsight:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

    <span data-ttu-id="9e487-143">i campi di Hello nei dati hello sono separati da un carattere di tabulazione e righe hello vengono terminate da un carattere di nuova riga.</span><span class="sxs-lookup"><span data-stu-id="9e487-143">hello fields in hello data are separated by a tab character, and hello lines are terminated by a new-line character.</span></span>

2. <span data-ttu-id="9e487-144">Una volta completata l'importazione di hello, utilizzare hello toolist comando dati hello nella nuova directory hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="9e487-144">Once hello import has completed, use hello following command toolist out hello data in hello new directory:</span></span>

    ```bash
    hdfs dfs -text /tutorials/usesqoop/importeddata/part-m-00000
    ```

## <a name="using-sql-server"></a><span data-ttu-id="9e487-145">Uso di SQL Server</span><span class="sxs-lookup"><span data-stu-id="9e487-145">Using SQL Server</span></span>

<span data-ttu-id="9e487-146">È inoltre possibile utilizzare Sqoop tooimport ed esportare dati da SQL Server, nel data center o in una macchina virtuale ospitata in Azure.</span><span class="sxs-lookup"><span data-stu-id="9e487-146">You can also use Sqoop tooimport and export data from SQL Server, either in your data center or on a Virtual Machine hosted in Azure.</span></span> <span data-ttu-id="9e487-147">Hello differenze tra l'utilizzo di Database SQL e SQL Server sono:</span><span class="sxs-lookup"><span data-stu-id="9e487-147">hello differences between using SQL Database and SQL Server are:</span></span>

* <span data-ttu-id="9e487-148">HDInsight sia SQL Server deve essere in hello stessa rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9e487-148">Both HDInsight and SQL Server must be on hello same Azure Virtual Network.</span></span>

    <span data-ttu-id="9e487-149">Per un esempio, vedere hello [rete locale di connettersi a HDInsight tooyour](./connect-on-premises-network.md) documento.</span><span class="sxs-lookup"><span data-stu-id="9e487-149">For an example, see hello [Connect HDInsight tooyour on-premises network](./connect-on-premises-network.md) document.</span></span>

    <span data-ttu-id="9e487-150">Per ulteriori informazioni sull'uso di HDInsight con una rete virtuale di Azure, vedere hello [estendere HDInsight con la rete virtuale di Azure](hdinsight-extend-hadoop-virtual-network.md) documento.</span><span class="sxs-lookup"><span data-stu-id="9e487-150">For more information on using HDInsight with an Azure Virtual Network, see hello [Extend HDInsight with Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span> <span data-ttu-id="9e487-151">Per ulteriori informazioni sulla rete virtuale di Azure, vedere hello [Panoramica di rete virtuale](../virtual-network/virtual-networks-overview.md) documento.</span><span class="sxs-lookup"><span data-stu-id="9e487-151">For more information on Azure Virtual Network, see hello [Virtual Network Overview](../virtual-network/virtual-networks-overview.md) document.</span></span>

* <span data-ttu-id="9e487-152">SQL Server deve essere tooallow configurata l'autenticazione di SQL.</span><span class="sxs-lookup"><span data-stu-id="9e487-152">SQL Server must be configured tooallow SQL authentication.</span></span> <span data-ttu-id="9e487-153">Per ulteriori informazioni, vedere hello [Choose an Authentication Mode](https://msdn.microsoft.com/ms144284.aspx) documento.</span><span class="sxs-lookup"><span data-stu-id="9e487-153">For more information, see hello [Choose an Authentication Mode](https://msdn.microsoft.com/ms144284.aspx) document.</span></span>

* <span data-ttu-id="9e487-154">È possibile connessioni remote tooaccept di tooconfigure SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9e487-154">You may have tooconfigure SQL Server tooaccept remote connections.</span></span> <span data-ttu-id="9e487-155">Per ulteriori informazioni, vedere hello [come motore di database tootroubleshoot toohello di connessione SQL Server](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) documento.</span><span class="sxs-lookup"><span data-stu-id="9e487-155">For more information, see hello [How tootroubleshoot connecting toohello SQL Server database engine](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) document.</span></span>

* <span data-ttu-id="9e487-156">Creare hello **sqooptest** database in SQL Server utilizzando un'utilità, ad esempio **SQL Server Management Studio** o **tsql**.</span><span class="sxs-lookup"><span data-stu-id="9e487-156">Create hello **sqooptest** database in SQL Server using a utility such as **SQL Server Management Studio** or **tsql**.</span></span> <span data-ttu-id="9e487-157">procedura di Hello per l'utilizzo di hello CLI di Azure funziona solo per Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="9e487-157">hello steps for using hello Azure CLI only work for Azure SQL Database.</span></span>

    <span data-ttu-id="9e487-158">Hello utilizzare hello toocreate di istruzioni Transact-SQL seguente **mobiledata** tabella:</span><span class="sxs-lookup"><span data-stu-id="9e487-158">Use hello following Transact-SQL statements toocreate hello **mobiledata** table:</span></span>

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    ```

* <span data-ttu-id="9e487-159">Durante la connessione SQL Server toohello da HDInsight, è possibile indirizzo IP di hello toouse di hello SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9e487-159">When connecting toohello SQL Server from HDInsight, you may have toouse hello IP address of hello SQL Server.</span></span> <span data-ttu-id="9e487-160">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="9e487-160">For example:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://10.0.1.1:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

## <a name="limitations"></a><span data-ttu-id="9e487-161">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="9e487-161">Limitations</span></span>

* <span data-ttu-id="9e487-162">Eseguire l'esportazione bulk - HDInsight basati su Linux con, hello Sqoop connettore utilizzato tooexport dati tooMicrosoft SQL Server o Database SQL di Azure attualmente non supporta inserimenti bulk.</span><span class="sxs-lookup"><span data-stu-id="9e487-162">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>

* <span data-ttu-id="9e487-163">Divisione in batch - con HDInsight basati su Linux, quando si utilizza hello `-batch` passare quando l'esecuzione di inserimenti, Sqoop rende più inserimenti anziché l'invio in batch le operazioni di inserimento hello.</span><span class="sxs-lookup"><span data-stu-id="9e487-163">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop makes multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e487-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9e487-164">Next steps</span></span>

<span data-ttu-id="9e487-165">Ora si è appreso come toouse Sqoop.</span><span class="sxs-lookup"><span data-stu-id="9e487-165">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="9e487-166">toolearn informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="9e487-166">toolearn more, see:</span></span>

* <span data-ttu-id="9e487-167">[Usare Oozie con HDInsight][hdinsight-use-oozie]: usare un'azione di Sqoop nel flusso di lavoro di Oozie.</span><span class="sxs-lookup"><span data-stu-id="9e487-167">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="9e487-168">[Analizzare i dati di ritardo volo tramite HDInsight][hdinsight-analyze-flight-data]: utilizzare Hive volo tooanalyze ritardare dati e quindi utilizzare il database SQL di Azure tooan di Sqoop tooexport dati.</span><span class="sxs-lookup"><span data-stu-id="9e487-168">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="9e487-169">[Caricare dati tooHDInsight][hdinsight-upload-data]: trovare altri metodi per il caricamento di archiviazione Blob di dati tooHDInsight/Azure.</span><span class="sxs-lookup"><span data-stu-id="9e487-169">[Upload data tooHDInsight][hdinsight-upload-data]: Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database-create-configure.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
