---
title: Copiare i dati tra Data Lake Store e il database SQL di Azure tramite Sqoop | Documentazione Microsoft
description: Usare Sqoop per copiare i dati tra il database SQL di Azure e Archivio Data Lake
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 3f914b2a-83cc-4950-b3f7-69c921851683
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 53bf33f6027f1f365bd92251490d5c851fb83f8b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a><span data-ttu-id="bb782-103">Copiare i dati tra Archivio Data Lake e un database SQL di Azure tramite Sqoop</span><span class="sxs-lookup"><span data-stu-id="bb782-103">Copy data between Data Lake Store and Azure SQL database using Sqoop</span></span>
<span data-ttu-id="bb782-104">Informazioni su come usare Apache Sqoop per importare ed esportare dati tra un database SQL di Azure e Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="bb782-104">Learn how to use Apache Sqoop to import and export data between Azure SQL Database and Data Lake Store.</span></span>

## <a name="what-is-sqoop"></a><span data-ttu-id="bb782-105">Informazioni su Sqoop</span><span class="sxs-lookup"><span data-stu-id="bb782-105">What is Sqoop?</span></span>
<span data-ttu-id="bb782-106">Le applicazioni Big Data sono una scelta naturale per l'elaborazione di dati non strutturati e semi-strutturati, ad esempio log e file.</span><span class="sxs-lookup"><span data-stu-id="bb782-106">Big data applications are a natural choice for processing unstructured and semi-structured data, such as logs and files.</span></span> <span data-ttu-id="bb782-107">Tuttavia, potrebbe anche essere necessario elaborare i dati strutturati archiviati nei database relazionali.</span><span class="sxs-lookup"><span data-stu-id="bb782-107">However, there may also be a need to process structured data that is stored in relational databases.</span></span>

<span data-ttu-id="bb782-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) è uno strumento progettato per trasferire dati tra database relazionali e un repository Big Data, ad esempio Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="bb782-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) is a tool designed to transfer data between  relational databases and a big data repository, such as Data Lake Store.</span></span> <span data-ttu-id="bb782-109">È possibile usarlo per importare dati da un sistema di gestione di database relazionali (RDBMS), ad esempio un database SQL di Azure, in Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="bb782-109">You can use it to import data from a relational database management system (RDBMS) such as Azure SQL Database into Data Lake Store.</span></span> <span data-ttu-id="bb782-110">È quindi possibile trasformare e analizzare i dati mediante carichi di lavoro Big Data e quindi esportarli nuovamente in un sistema RDBMS.</span><span class="sxs-lookup"><span data-stu-id="bb782-110">You can then transform and analyze the data using big data workloads and then export the data back into an RDBMS.</span></span> <span data-ttu-id="bb782-111">In questa esercitazione viene usato un database SQL di Azure come database relazionale da cui importare/esportare dati.</span><span class="sxs-lookup"><span data-stu-id="bb782-111">In this tutorial, you use an Azure SQL Database as your relational database to import/export from.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb782-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bb782-112">Prerequisites</span></span>
<span data-ttu-id="bb782-113">Per eseguire le procedure descritte nell'articolo è necessario:</span><span class="sxs-lookup"><span data-stu-id="bb782-113">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="bb782-114">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="bb782-114">**An Azure subscription**.</span></span> <span data-ttu-id="bb782-115">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bb782-115">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="bb782-116">**Un account di Archivio Data Lake di Azure**.</span><span class="sxs-lookup"><span data-stu-id="bb782-116">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="bb782-117">Per istruzioni su come crearne uno, vedere [Introduzione ad Archivio Data Lake di Azure](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="bb782-117">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="bb782-118">**Cluster Azure HDInsight** con accesso a un account di Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="bb782-118">**Azure HDInsight cluster** with access to a Data Lake Store account.</span></span> <span data-ttu-id="bb782-119">Vedere [Creare un cluster HDInsight con Archivio Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bb782-119">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="bb782-120">Questo articolo presuppone che si abbia un cluster HDInsight Linux con accesso ad Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="bb782-120">This article assumes you have an HDInsight Linux cluster with Data Lake Store access.</span></span>
* <span data-ttu-id="bb782-121">**Database SQL di Azure**.</span><span class="sxs-lookup"><span data-stu-id="bb782-121">**Azure SQL Database**.</span></span> <span data-ttu-id="bb782-122">Per istruzioni su come crearne uno, vedere [Creare un database SQL di Azure](../sql-database/sql-database-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="bb782-122">For instructions on how to create one, see [Create an Azure SQL database](../sql-database/sql-database-get-started.md)</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="bb782-123">Apprendimento rapido con i video</span><span class="sxs-lookup"><span data-stu-id="bb782-123">Do you learn fast with videos?</span></span>
<span data-ttu-id="bb782-124">[Guardare questo video](https://mix.office.com/watch/1butcdjxmu114) su come copiare dati tra i BLOB di archiviazione di Azure e Archivio Data Lake con DistCp.</span><span class="sxs-lookup"><span data-stu-id="bb782-124">[Watch this video](https://mix.office.com/watch/1butcdjxmu114) on how to copy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="create-sample-tables-in-the-azure-sql-database"></a><span data-ttu-id="bb782-125">Creare tabelle di esempio nel database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="bb782-125">Create sample tables in the Azure SQL Database</span></span>
1. <span data-ttu-id="bb782-126">Per iniziare, creare due tabelle di esempio nel database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="bb782-126">To start with, create two sample tables in the Azure SQL Database.</span></span> <span data-ttu-id="bb782-127">Usare [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) o Visual Studio per connettersi al database SQL di Azure e quindi eseguire le query seguenti.</span><span class="sxs-lookup"><span data-stu-id="bb782-127">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio to connect to the Azure SQL Database and then run the following queries.</span></span>

    <span data-ttu-id="bb782-128">**Create Table1**</span><span class="sxs-lookup"><span data-stu-id="bb782-128">**Create Table1**</span></span>

        CREATE TABLE [dbo].[Table1](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO

    <span data-ttu-id="bb782-129">**Create Table2**</span><span class="sxs-lookup"><span data-stu-id="bb782-129">**Create Table2**</span></span>

        CREATE TABLE [dbo].[Table2](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO
2. <span data-ttu-id="bb782-130">In **Table1**aggiungere alcuni dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="bb782-130">In **Table1**, add some sample data.</span></span> <span data-ttu-id="bb782-131">Lasciare vuota **Table2** .</span><span class="sxs-lookup"><span data-stu-id="bb782-131">Leave **Table2** empty.</span></span> <span data-ttu-id="bb782-132">Verranno importati dati da **Table1** ad Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="bb782-132">We will import data from **Table1** into Data Lake Store.</span></span> <span data-ttu-id="bb782-133">Quindi, verranno esportati dati da Archivio Data Lake a **Table2**.</span><span class="sxs-lookup"><span data-stu-id="bb782-133">Then, we will export data from Data Lake Store into **Table2**.</span></span> <span data-ttu-id="bb782-134">Eseguire il frammento di codice seguente.</span><span class="sxs-lookup"><span data-stu-id="bb782-134">Run the following snippet.</span></span>

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-to-data-lake-store"></a><span data-ttu-id="bb782-135">Usare Sqoop da un cluster HDInsight con accesso ad Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="bb782-135">Use Sqoop from an HDInsight cluster with access to Data Lake Store</span></span>
<span data-ttu-id="bb782-136">In un cluster HDInsight sono già disponibili i pacchetti di Sqoop.</span><span class="sxs-lookup"><span data-stu-id="bb782-136">An HDInsight cluster already has the Sqoop packages available.</span></span> <span data-ttu-id="bb782-137">Se il cluster HDInsight è stato configurato per l'uso di Archivio Data Lake come archiviazione aggiuntiva, è possibile usare Sqoop (senza apportare modifiche alla configurazione) per importare o esportare dati tra un database relazionale (in questo esempio, un database SQL di Azure) e un account Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="bb782-137">If you have configured the HDInsight cluster to use Data Lake Store as an additional storage, you can use Sqoop (without any configuration changes) to import/export data between a relational database (in this example, Azure SQL Database) and a Data Lake Store account.</span></span>

1. <span data-ttu-id="bb782-138">Per questa esercitazione si presuppone che sia stato creato un cluster Linux, quindi è consigliabile usare SSH per connettersi al cluster.</span><span class="sxs-lookup"><span data-stu-id="bb782-138">For this tutorial, we assume you created a Linux cluster so you should use SSH to connect to the cluster.</span></span> <span data-ttu-id="bb782-139">Vedere [Connettersi a un cluster HDInsight basato su Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="bb782-139">See [Connect to a Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
2. <span data-ttu-id="bb782-140">Verificare se è possibile accedere all'account Archivio Data Lake dal cluster.</span><span class="sxs-lookup"><span data-stu-id="bb782-140">Verify whether you can access the Data Lake Store account from the cluster.</span></span> <span data-ttu-id="bb782-141">Eseguire il comando seguente dal prompt SSH:</span><span class="sxs-lookup"><span data-stu-id="bb782-141">Run the following command from the SSH prompt:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    <span data-ttu-id="bb782-142">Dovrebbe essere visualizzato un elenco di file/cartelle nell'account Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="bb782-142">This should provide a list of files/folders in the Data Lake Store account.</span></span>

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a><span data-ttu-id="bb782-143">Importare dati da un database SQL di Azure ad Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="bb782-143">Import data from Azure SQL Database into Data Lake Store</span></span>
1. <span data-ttu-id="bb782-144">Passare alla directory in cui sono disponibili i pacchetti di Sqoop.</span><span class="sxs-lookup"><span data-stu-id="bb782-144">Navigate to the directory where Sqoop packages are available.</span></span> <span data-ttu-id="bb782-145">In genere, questa corrisponde a `/usr/hdp/<version>/sqoop/bin`.</span><span class="sxs-lookup"><span data-stu-id="bb782-145">Typically, this will be at `/usr/hdp/<version>/sqoop/bin`.</span></span>
2. <span data-ttu-id="bb782-146">Importare i dati da **Table1** all'account di Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="bb782-146">Import the data from **Table1** into the Data Lake Store account.</span></span> <span data-ttu-id="bb782-147">Usare la sintassi seguente:</span><span class="sxs-lookup"><span data-stu-id="bb782-147">Use the following syntax:</span></span>

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    <span data-ttu-id="bb782-148">Si noti che il segnaposto **sql-database-server-name** rappresenta il nome del server in cui è in esecuzione il database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="bb782-148">Note that **sql-database-server-name** placeholder represents the name of the server where the Azure SQL database is running.</span></span> <span data-ttu-id="bb782-149">**sql-database-name** rappresenta il nome effettivo del database.</span><span class="sxs-lookup"><span data-stu-id="bb782-149">**sql-database-name** placeholder represents the actual database name.</span></span>

    <span data-ttu-id="bb782-150">Ad esempio,</span><span class="sxs-lookup"><span data-stu-id="bb782-150">For example,</span></span>


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. <span data-ttu-id="bb782-151">Verificare che i dati siano stati trasferiti all'account Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="bb782-151">Verify that the data has been transferred to the Data Lake Store account.</span></span> <span data-ttu-id="bb782-152">Eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="bb782-152">Run the following command:</span></span>

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    <span data-ttu-id="bb782-153">Viene visualizzato l'output seguente.</span><span class="sxs-lookup"><span data-stu-id="bb782-153">You should see the following output.</span></span>


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    <span data-ttu-id="bb782-154">Ogni file **part-m-*** corrisponde a una riga nella tabella di origine, **Table1**.</span><span class="sxs-lookup"><span data-stu-id="bb782-154">Each **part-m-*** file corresponds to a row in the source table, **Table1**.</span></span> <span data-ttu-id="bb782-155">È possibile visualizzare i contenuti dei file part-m-* per la verifica.</span><span class="sxs-lookup"><span data-stu-id="bb782-155">You can view the contents of the part-m-* files to verify.</span></span>


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a><span data-ttu-id="bb782-156">Esportare dati da Archivio Data Lake a un database SQL di Azure </span><span class="sxs-lookup"><span data-stu-id="bb782-156">Export data from Data Lake Store into Azure SQL Database</span></span>
1. <span data-ttu-id="bb782-157">Esportare i dati dall'account di Data Lake Store alla tabella vuota, **Table2**, nel database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="bb782-157">Export the data from Data Lake Store account to the empty table, **Table2**, in the Azure SQL Database.</span></span> <span data-ttu-id="bb782-158">Usare la sintassi seguente.</span><span class="sxs-lookup"><span data-stu-id="bb782-158">Use the following syntax.</span></span>

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    <span data-ttu-id="bb782-159">Ad esempio,</span><span class="sxs-lookup"><span data-stu-id="bb782-159">For example,</span></span>


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. <span data-ttu-id="bb782-160">Verificare che i dati siano stati caricati nella tabella del database SQL.</span><span class="sxs-lookup"><span data-stu-id="bb782-160">Verify that the data was uploaded to the SQL Database table.</span></span> <span data-ttu-id="bb782-161">Usare [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) o Visual Studio per connettersi al database SQL di Azure e quindi eseguire la query seguente.</span><span class="sxs-lookup"><span data-stu-id="bb782-161">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio to connect to the Azure SQL Database and then run the following query.</span></span>

        SELECT * FROM TABLE2

    <span data-ttu-id="bb782-162">L'output della query corrisponde al seguente.</span><span class="sxs-lookup"><span data-stu-id="bb782-162">This should have the following output.</span></span>

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a><span data-ttu-id="bb782-163">Considerazioni sulle prestazioni per l'uso di Sqoop</span><span class="sxs-lookup"><span data-stu-id="bb782-163">Performance considerations while using Sqoop</span></span>

<span data-ttu-id="bb782-164">Per ottimizzare le prestazioni del processo di Sqoop per copiare i dati in Data Lake Store, vedere il [documento sulle prestazioni di Sqoop](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span><span class="sxs-lookup"><span data-stu-id="bb782-164">For performance tuning your Sqoop job to copy data to Data Lake Store, see [Sqoop performance document](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span></span>

## <a name="see-also"></a><span data-ttu-id="bb782-165">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="bb782-165">See also</span></span>
* [<span data-ttu-id="bb782-166">Copiare i dati da BLOB di archiviazione di Azure ad Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="bb782-166">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="bb782-167">Proteggere i dati in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="bb782-167">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="bb782-168">Usare Azure Data Lake Analytics con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="bb782-168">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="bb782-169">Usare Azure HDInsight con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="bb782-169">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
