---
title: Apache Sqoop con Hadoop - Azure HDInsight | Microsoft Docs
description: Informazioni su come usare Apache Sqoop per importare ed esportare tra Hadoop in HDInsight e un database SQL di Azure.
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
ms.openlocfilehash: 35dcbb91e6af1480685c9fd5b829c54277c1c605
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-apache-sqoop-to-import-and-export-data-between-hadoop-on-hdinsight-and-sql-database"></a><span data-ttu-id="30789-104">Usare Apache Sqoop per importare ed esportare dati tra Hadoop su HDInsight e un database SQL</span><span class="sxs-lookup"><span data-stu-id="30789-104">Use Apache Sqoop to import and export data between Hadoop on HDInsight and SQL Database</span></span>

[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="30789-105">Informazioni su come usare Apache Sqoop per eseguire importazioni ed esportazioni tra un cluster Hadoop in Azure HDInsight e un database SQL di Azure o un database Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="30789-105">Learn how to use Apache Sqoop to import and export between a Hadoop cluster in Azure HDInsight and Azure SQL Database or Microsoft SQL Server database.</span></span> <span data-ttu-id="30789-106">La procedura descritta in questo documento usa il comando `sqoop` direttamente dal nodo head del cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="30789-106">The steps in this document use the `sqoop` command directly from the headnode of the Hadoop cluster.</span></span> <span data-ttu-id="30789-107">Usare SSH per connettersi al nodo head ed eseguire i comandi di questo documento.</span><span class="sxs-lookup"><span data-stu-id="30789-107">You use SSH to connect to the head node and run the commands in this document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="30789-108">I passaggi descritti in questo documento funzionano solo con i cluster HDInsight che usano Linux.</span><span class="sxs-lookup"><span data-stu-id="30789-108">The steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="30789-109">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="30789-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="30789-110">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="30789-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="install-freetds"></a><span data-ttu-id="30789-111">Installare FreeTDS</span><span class="sxs-lookup"><span data-stu-id="30789-111">Install FreeTDS</span></span>

1. <span data-ttu-id="30789-112">Connettersi al cluster HDInsight usando SSH.</span><span class="sxs-lookup"><span data-stu-id="30789-112">Use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="30789-113">Ad esempio, il comando seguente si connette al nodo head primario di un cluster denominato `mycluster`:</span><span class="sxs-lookup"><span data-stu-id="30789-113">For example, the following command connects to the primary headnode of a cluster named `mycluster`:</span></span>

    ```bash
    ssh CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="30789-114">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="30789-114">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="30789-115">Immettere il comando seguente per installare FreeTDS:</span><span class="sxs-lookup"><span data-stu-id="30789-115">Use the following command to install FreeTDS:</span></span>

    ```bash
    sudo apt --assume-yes install freetds-dev freetds-bin
    ```

    <span data-ttu-id="30789-116">FreeTDS viene usato in diversi passaggi per connettersi al database SQL.</span><span class="sxs-lookup"><span data-stu-id="30789-116">FreeTDS is used in several steps to connect to SQL Database.</span></span>

## <a name="create-the-table-in-sql-database"></a><span data-ttu-id="30789-117">Creare la tabella nel database SQL</span><span class="sxs-lookup"><span data-stu-id="30789-117">Create the table in SQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="30789-118">Se si usa il cluster HDInsight e il database SQL creato in [Creare cluster e database SQL](hdinsight-use-sqoop.md), saltare i passaggi descritti in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="30789-118">If you are using the HDInsight cluster and SQL Database created in [Create cluster and SQL database](hdinsight-use-sqoop.md), skip the steps in this section.</span></span> <span data-ttu-id="30789-119">Il database e la tabella sono stati creati come parte della procedura del documento [Creare cluster e database SQL](hdinsight-use-sqoop.md).</span><span class="sxs-lookup"><span data-stu-id="30789-119">The database and table were created as part of the steps in the [Create cluster and SQL database](hdinsight-use-sqoop.md) document.</span></span>

1. <span data-ttu-id="30789-120">Nella sessione SSH usare il comando seguente per connettersi al server del database SQL.</span><span class="sxs-lookup"><span data-stu-id="30789-120">From the SSH session, use the following command to connect to the SQL Database server.</span></span>

        TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D sqooptest

    <span data-ttu-id="30789-121">L'output che si riceve è simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="30789-121">You receive output similar to the following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set to sqooptest
        1>

2. <span data-ttu-id="30789-122">Al prompt di `1>` immettere la query seguente:</span><span class="sxs-lookup"><span data-stu-id="30789-122">At the `1>` prompt, enter the following query:</span></span>

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

    <span data-ttu-id="30789-123">Dopo aver immesso l'istruzione `GO`, vengono valutate le istruzioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="30789-123">When the `GO` statement is entered, the previous statements are evaluated.</span></span> <span data-ttu-id="30789-124">Innanzitutto, verrà creata la tabella **mobiledata** a cui verrà aggiunto un indice cluster (richiesto dal Database SQL).</span><span class="sxs-lookup"><span data-stu-id="30789-124">First, the **mobiledata** table is created, then a clustered index is added to it (required by SQL Database.)</span></span>

    <span data-ttu-id="30789-125">Per verificare la corretta creazione della tabella, usare la query seguente:</span><span class="sxs-lookup"><span data-stu-id="30789-125">Use the following query to verify that the table has been created:</span></span>

    ```sql
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="30789-126">L'output sarà simile al seguente testo:</span><span class="sxs-lookup"><span data-stu-id="30789-126">You see output similar to the following text:</span></span>

        TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
        sqooptest       dbo     mobiledata      BASE TABLE

3. <span data-ttu-id="30789-127">Per uscire dall'utilità tsql, immettere `exit` al prompt di `1>`.</span><span class="sxs-lookup"><span data-stu-id="30789-127">Enter `exit` at the `1>` prompt to exit the tsql utility.</span></span>

## <a name="sqoop-export"></a><span data-ttu-id="30789-128">Esportazione con Sqoop</span><span class="sxs-lookup"><span data-stu-id="30789-128">Sqoop export</span></span>

1. <span data-ttu-id="30789-129">Dalla connessione SSH al cluster, usare il comando seguente per verificare che Sqoop possa visualizzare il database SQL:</span><span class="sxs-lookup"><span data-stu-id="30789-129">From the SSH connection to the cluster, use the following command to verify that Sqoop can see your SQL Database:</span></span>

    ```bash
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> -P
    ```
    <span data-ttu-id="30789-130">Quando richiesto, immettere la password per l’accesso al database SQL.</span><span class="sxs-lookup"><span data-stu-id="30789-130">When prompted, enter the password for the SQL Database login.</span></span>

    <span data-ttu-id="30789-131">Questo comando restituisce un elenco di database, compreso il database **sqooptest** creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="30789-131">This command returns a list of databases, including the **sqooptest** database that you created earlier.</span></span>

2. <span data-ttu-id="30789-132">Per esportare dati dalla tabella **hivesampletable** alla tabella **mobiledata**, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="30789-132">To export data from **hivesampletable** to the **mobiledata** table, use the following command:</span></span>

    ```bash
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> -P --table 'mobiledata' --export-dir 'wasb:///hive/warehouse/hivesampletable' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="30789-133">Questo comando indica a Sqoop di connettersi al database **sqooptest**.</span><span class="sxs-lookup"><span data-stu-id="30789-133">This command instructs Sqoop to connect to the **sqooptest** database.</span></span> <span data-ttu-id="30789-134">Sqoop esporta quindi i dati da **wasb:///hive/warehouse/hivesampletable** nella tabella **mobiledata**.</span><span class="sxs-lookup"><span data-stu-id="30789-134">Sqoop then exports data from **wasb:///hive/warehouse/hivesampletable** to the **mobiledata** table.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="30789-135">Usare `wasb:///` se l'archivio predefinito per il cluster è un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="30789-135">Use `wasb:///` if the default storage for your cluster is an Azure Storage account.</span></span> <span data-ttu-id="30789-136">Usare `adl:///` se è un Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="30789-136">Use `adl:///` if it is an Azure Data Lake Store.</span></span>

3. <span data-ttu-id="30789-137">Al termine dell'esecuzione del comando, usare il comando seguente per connettersi al database tramite TSQL:</span><span class="sxs-lookup"><span data-stu-id="30789-137">After the command completes, use the following command to connect to the database using TSQL:</span></span>

    ```bash
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P -p 1433 -D sqooptest
    ```

    <span data-ttu-id="30789-138">Una volta connessi, utilizzare le istruzioni seguenti per verificare che i dati siano stati esportati nella tabella **mobiledata** :</span><span class="sxs-lookup"><span data-stu-id="30789-138">Once connected, use the following statements to verify that the data was exported to the **mobiledata** table:</span></span>

    ```sql
    SET ROWCOUNT 50;
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="30789-139">Dovrebbe essere visualizzato un elenco di dati della tabella.</span><span class="sxs-lookup"><span data-stu-id="30789-139">You should see a listing of data in the table.</span></span> <span data-ttu-id="30789-140">Digitare `exit` per uscire dall'utilità tsql.</span><span class="sxs-lookup"><span data-stu-id="30789-140">Type `exit` to exit the tsql utility.</span></span>

## <a name="sqoop-import"></a><span data-ttu-id="30789-141">Importazione con Sqoop</span><span class="sxs-lookup"><span data-stu-id="30789-141">Sqoop import</span></span>

1. <span data-ttu-id="30789-142">Usare il comando seguente per importare i dati dalla tabella **mobiledata** nel database SQL alla directory **wasb:///tutorials/usesqoop/importeddata** in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="30789-142">Use the following command to import data from the **mobiledata** table in SQL Database, to the **wasb:///tutorials/usesqoop/importeddata** directory on HDInsight:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

    <span data-ttu-id="30789-143">I campi nei dati sono separati da un carattere di tabulazione e le righe terminano con un carattere di nuova riga.</span><span class="sxs-lookup"><span data-stu-id="30789-143">The fields in the data are separated by a tab character, and the lines are terminated by a new-line character.</span></span>

2. <span data-ttu-id="30789-144">Una volta completata l'importazione, usare il comando seguente per elencare i dati della nuova directory:</span><span class="sxs-lookup"><span data-stu-id="30789-144">Once the import has completed, use the following command to list out the data in the new directory:</span></span>

    ```bash
    hdfs dfs -text /tutorials/usesqoop/importeddata/part-m-00000
    ```

## <a name="using-sql-server"></a><span data-ttu-id="30789-145">Uso di SQL Server</span><span class="sxs-lookup"><span data-stu-id="30789-145">Using SQL Server</span></span>

<span data-ttu-id="30789-146">È inoltre possibile usare Sqoop per importare ed esportare dati da SQL Server nel data center o in una macchina virtuale ospitata in Azure.</span><span class="sxs-lookup"><span data-stu-id="30789-146">You can also use Sqoop to import and export data from SQL Server, either in your data center or on a Virtual Machine hosted in Azure.</span></span> <span data-ttu-id="30789-147">Le differenze tra l'uso del database SQL e SQL Server sono:</span><span class="sxs-lookup"><span data-stu-id="30789-147">The differences between using SQL Database and SQL Server are:</span></span>

* <span data-ttu-id="30789-148">HDInsight e SQL Server devono trovarsi nella stessa rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="30789-148">Both HDInsight and SQL Server must be on the same Azure Virtual Network.</span></span>

    <span data-ttu-id="30789-149">Per avere un esempio, vedere il documento [Connettere HDInsight alla rete locale](./connect-on-premises-network.md).</span><span class="sxs-lookup"><span data-stu-id="30789-149">For an example, see the [Connect HDInsight to your on-premises network](./connect-on-premises-network.md) document.</span></span>

    <span data-ttu-id="30789-150">Per altre informazioni sull'uso di HDInsight con le reti virtuali di Azure, vedere il documento [Estendere HDInsight con la rete virtuale di Azure](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="30789-150">For more information on using HDInsight with an Azure Virtual Network, see the [Extend HDInsight with Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span> <span data-ttu-id="30789-151">Per altre informazioni su Rete virtuale di Azure, vedere il documenti di [panoramica sulle reti virtuali](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="30789-151">For more information on Azure Virtual Network, see the [Virtual Network Overview](../virtual-network/virtual-networks-overview.md) document.</span></span>

* <span data-ttu-id="30789-152">SQL Server deve essere configurato per consentire l'autenticazione SQL.</span><span class="sxs-lookup"><span data-stu-id="30789-152">SQL Server must be configured to allow SQL authentication.</span></span> <span data-ttu-id="30789-153">Per altre informazioni, consultare il documento [Scegliere una modalità di autenticazione](https://msdn.microsoft.com/ms144284.aspx).</span><span class="sxs-lookup"><span data-stu-id="30789-153">For more information, see the [Choose an Authentication Mode](https://msdn.microsoft.com/ms144284.aspx) document.</span></span>

* <span data-ttu-id="30789-154">Potrebbe essere necessario configurare SQL Server affinché accetti le connessioni remote.</span><span class="sxs-lookup"><span data-stu-id="30789-154">You may have to configure SQL Server to accept remote connections.</span></span> <span data-ttu-id="30789-155">Per altre informazioni, vedere il documento [Come risolvere i problemi di connessione al motore di database di SQL Server](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx).</span><span class="sxs-lookup"><span data-stu-id="30789-155">For more information, see the [How to troubleshoot connecting to the SQL Server database engine](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) document.</span></span>

* <span data-ttu-id="30789-156">Creare il database **sqooptest** in SQL Server usando un'utilità, ad esempio **SQL Server Management Studio** o **tsql**.</span><span class="sxs-lookup"><span data-stu-id="30789-156">Create the **sqooptest** database in SQL Server using a utility such as **SQL Server Management Studio** or **tsql**.</span></span> <span data-ttu-id="30789-157">La procedura per usare l'interfaccia della riga di comando di Azure funzionano solo per il database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="30789-157">The steps for using the Azure CLI only work for Azure SQL Database.</span></span>

    <span data-ttu-id="30789-158">Usare le seguenti istruzioni Transact-SQL per creare la tabella **mobiledata**:</span><span class="sxs-lookup"><span data-stu-id="30789-158">Use the following Transact-SQL statements to create the **mobiledata** table:</span></span>

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

* <span data-ttu-id="30789-159">Quando ci si connette a SQL Server da HDInsight, è necessario usare l'indirizzo IP del Server SQL.</span><span class="sxs-lookup"><span data-stu-id="30789-159">When connecting to the SQL Server from HDInsight, you may have to use the IP address of the SQL Server.</span></span> <span data-ttu-id="30789-160">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="30789-160">For example:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://10.0.1.1:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

## <a name="limitations"></a><span data-ttu-id="30789-161">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="30789-161">Limitations</span></span>

* <span data-ttu-id="30789-162">Esportazione di massa: con HDInsight basato su Linux, attualmente il connettore Sqoop, usato per esportare dati in Microsoft SQL Server o nel database SQL di Azure, non supporta inserimenti di massa.</span><span class="sxs-lookup"><span data-stu-id="30789-162">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>

* <span data-ttu-id="30789-163">Invio in batch: con HDInsight basato su Linux, quando si usa il comando `-batch` durante gli inserimenti, Sqoop esegue più inserimenti invece di suddividere in batch le operazioni di inserimento.</span><span class="sxs-lookup"><span data-stu-id="30789-163">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop makes multiple inserts instead of batching the insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30789-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="30789-164">Next steps</span></span>

<span data-ttu-id="30789-165">In questa esercitazione si è appreso come usare Sqoop.</span><span class="sxs-lookup"><span data-stu-id="30789-165">Now you have learned how to use Sqoop.</span></span> <span data-ttu-id="30789-166">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="30789-166">To learn more, see:</span></span>

* <span data-ttu-id="30789-167">[Usare Oozie con HDInsight][hdinsight-use-oozie]: usare un'azione di Sqoop nel flusso di lavoro di Oozie.</span><span class="sxs-lookup"><span data-stu-id="30789-167">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="30789-168">[Analizzare i dati sui ritardi dei voli con HDInsight][hdinsight-analyze-flight-data]: usare Hive per analizzare i dati sui ritardi dei voli e quindi usare Sqoop per esportare dati in un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="30789-168">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span></span>
* <span data-ttu-id="30789-169">[Caricare dati in HDInsight][hdinsight-upload-data]: altri metodi per caricare dati in HDInsight e nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="30789-169">[Upload data to HDInsight][hdinsight-upload-data]: Find other methods for uploading data to HDInsight/Azure Blob storage.</span></span>

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
