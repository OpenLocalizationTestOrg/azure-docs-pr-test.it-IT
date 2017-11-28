---
title: dati aaaCopy tra archivio Data Lake e database di SQL Azure mediante Sqoop | Documenti Microsoft
description: Utilizzare Sqoop toocopy dati tra Database SQL di Azure e archivio Data Lake
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
ms.openlocfilehash: f58483455f0ebe9544673a1d5c5884f2721c800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a><span data-ttu-id="a48b0-103">Copiare i dati tra Archivio Data Lake e un database SQL di Azure tramite Sqoop</span><span class="sxs-lookup"><span data-stu-id="a48b0-103">Copy data between Data Lake Store and Azure SQL database using Sqoop</span></span>
<span data-ttu-id="a48b0-104">Informazioni su come toouse Sqoop Apache tooimport ed esportare dati tra Database SQL di Azure e archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a48b0-104">Learn how toouse Apache Sqoop tooimport and export data between Azure SQL Database and Data Lake Store.</span></span>

## <a name="what-is-sqoop"></a><span data-ttu-id="a48b0-105">Informazioni su Sqoop</span><span class="sxs-lookup"><span data-stu-id="a48b0-105">What is Sqoop?</span></span>
<span data-ttu-id="a48b0-106">Le applicazioni Big Data sono una scelta naturale per l'elaborazione di dati non strutturati e semi-strutturati, ad esempio log e file.</span><span class="sxs-lookup"><span data-stu-id="a48b0-106">Big data applications are a natural choice for processing unstructured and semi-structured data, such as logs and files.</span></span> <span data-ttu-id="a48b0-107">Tuttavia, è inoltre possibile un necessità tooprocess strutturato i dati archiviati nei database relazionali.</span><span class="sxs-lookup"><span data-stu-id="a48b0-107">However, there may also be a need tooprocess structured data that is stored in relational databases.</span></span>

<span data-ttu-id="a48b0-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) è un tootransfer strumento progettato dati tra i database relazionali e di un repository di dati di grandi dimensioni, ad esempio archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a48b0-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) is a tool designed tootransfer data between  relational databases and a big data repository, such as Data Lake Store.</span></span> <span data-ttu-id="a48b0-109">È possibile utilizzare dati tooimport da un sistema di gestione di database relazionali (RDBMS), ad esempio Database SQL di Azure in archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a48b0-109">You can use it tooimport data from a relational database management system (RDBMS) such as Azure SQL Database into Data Lake Store.</span></span> <span data-ttu-id="a48b0-110">È possibile quindi trasformano e analizzare i dati di hello utilizzando i carichi di lavoro di big data e quindi esportare i dati di hello in un sistema RDBMS.</span><span class="sxs-lookup"><span data-stu-id="a48b0-110">You can then transform and analyze hello data using big data workloads and then export hello data back into an RDBMS.</span></span> <span data-ttu-id="a48b0-111">In questa esercitazione, si utilizza un Database di SQL Azure come tooimport/esportazione del database relazionale da.</span><span class="sxs-lookup"><span data-stu-id="a48b0-111">In this tutorial, you use an Azure SQL Database as your relational database tooimport/export from.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a48b0-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a48b0-112">Prerequisites</span></span>
<span data-ttu-id="a48b0-113">Prima di iniziare questo articolo, è necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="a48b0-113">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="a48b0-114">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="a48b0-114">**An Azure subscription**.</span></span> <span data-ttu-id="a48b0-115">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a48b0-115">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a48b0-116">**Un account Azure Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="a48b0-116">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="a48b0-117">Per istruzioni su come toocreate uno, vedere [introduzione archivio Azure Data Lake](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="a48b0-117">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="a48b0-118">**Cluster di Azure HDInsight** con accesso tooa account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a48b0-118">**Azure HDInsight cluster** with access tooa Data Lake Store account.</span></span> <span data-ttu-id="a48b0-119">Vedere [Creare un cluster HDInsight con Data Lake Store tramite il portale di Azure](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a48b0-119">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="a48b0-120">Questo articolo presuppone che si abbia un cluster HDInsight Linux con accesso ad Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a48b0-120">This article assumes you have an HDInsight Linux cluster with Data Lake Store access.</span></span>
* <span data-ttu-id="a48b0-121">**Database SQL di Azure**.</span><span class="sxs-lookup"><span data-stu-id="a48b0-121">**Azure SQL Database**.</span></span> <span data-ttu-id="a48b0-122">Per istruzioni su come toocreate uno, vedere [creare un database SQL di Azure](../sql-database/sql-database-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="a48b0-122">For instructions on how toocreate one, see [Create an Azure SQL database](../sql-database/sql-database-get-started.md)</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="a48b0-123">Apprendimento rapido con i video</span><span class="sxs-lookup"><span data-stu-id="a48b0-123">Do you learn fast with videos?</span></span>
<span data-ttu-id="a48b0-124">[Guardare questo video](https://mix.office.com/watch/1butcdjxmu114) sulla toocopy dati tra il BLOB di archiviazione di Azure e archivio Data Lake tramite DistCp.</span><span class="sxs-lookup"><span data-stu-id="a48b0-124">[Watch this video](https://mix.office.com/watch/1butcdjxmu114) on how toocopy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="create-sample-tables-in-hello-azure-sql-database"></a><span data-ttu-id="a48b0-125">Creare tabelle di esempio in hello Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="a48b0-125">Create sample tables in hello Azure SQL Database</span></span>
1. <span data-ttu-id="a48b0-126">toostart, creare due tabelle di esempio in hello Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="a48b0-126">toostart with, create two sample tables in hello Azure SQL Database.</span></span> <span data-ttu-id="a48b0-127">Utilizzare [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) o Visual Studio tooconnect toohello Database SQL di Azure e quindi eseguire hello seguendo le query.</span><span class="sxs-lookup"><span data-stu-id="a48b0-127">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio tooconnect toohello Azure SQL Database and then run hello following queries.</span></span>

    <span data-ttu-id="a48b0-128">**Create Table1**</span><span class="sxs-lookup"><span data-stu-id="a48b0-128">**Create Table1**</span></span>

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

    <span data-ttu-id="a48b0-129">**Create Table2**</span><span class="sxs-lookup"><span data-stu-id="a48b0-129">**Create Table2**</span></span>

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
2. <span data-ttu-id="a48b0-130">In **Table1**aggiungere alcuni dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="a48b0-130">In **Table1**, add some sample data.</span></span> <span data-ttu-id="a48b0-131">Lasciare vuota **Table2** .</span><span class="sxs-lookup"><span data-stu-id="a48b0-131">Leave **Table2** empty.</span></span> <span data-ttu-id="a48b0-132">Verranno importati dati da **Table1** ad Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a48b0-132">We will import data from **Table1** into Data Lake Store.</span></span> <span data-ttu-id="a48b0-133">Quindi, verranno esportati dati da Archivio Data Lake a **Table2**.</span><span class="sxs-lookup"><span data-stu-id="a48b0-133">Then, we will export data from Data Lake Store into **Table2**.</span></span> <span data-ttu-id="a48b0-134">Eseguire hello seguente frammento di codice.</span><span class="sxs-lookup"><span data-stu-id="a48b0-134">Run hello following snippet.</span></span>

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-toodata-lake-store"></a><span data-ttu-id="a48b0-135">Utilizzare Sqoop da un cluster di HDInsight con accesso tooData Lake archivio</span><span class="sxs-lookup"><span data-stu-id="a48b0-135">Use Sqoop from an HDInsight cluster with access tooData Lake Store</span></span>
<span data-ttu-id="a48b0-136">Un cluster HDInsight dispone già di pacchetti Sqoop hello disponibili.</span><span class="sxs-lookup"><span data-stu-id="a48b0-136">An HDInsight cluster already has hello Sqoop packages available.</span></span> <span data-ttu-id="a48b0-137">Se è stata configurata l'archivio Data Lake toouse cluster HDInsight hello come un'ulteriore spazio di archiviazione, è possibile utilizzare Sqoop (senza apportare modifiche di configurazione) tooimport ed esportare dati tra un database relazionale (in questo esempio, Database SQL di Azure) e un archivio Data Lake account.</span><span class="sxs-lookup"><span data-stu-id="a48b0-137">If you have configured hello HDInsight cluster toouse Data Lake Store as an additional storage, you can use Sqoop (without any configuration changes) tooimport/export data between a relational database (in this example, Azure SQL Database) and a Data Lake Store account.</span></span>

1. <span data-ttu-id="a48b0-138">Per questa esercitazione, si presuppone che un cluster Linux è stato creato è necessario utilizzare SSH tooconnect toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="a48b0-138">For this tutorial, we assume you created a Linux cluster so you should use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="a48b0-139">Vedere [cluster HDInsight basati su Linux di Connect tooa](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="a48b0-139">See [Connect tooa Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
2. <span data-ttu-id="a48b0-140">Verificare se sia possibile accedere hello account archivio Data Lake dal cluster hello.</span><span class="sxs-lookup"><span data-stu-id="a48b0-140">Verify whether you can access hello Data Lake Store account from hello cluster.</span></span> <span data-ttu-id="a48b0-141">Eseguire hello comando seguente dal prompt dei comandi di hello SSH:</span><span class="sxs-lookup"><span data-stu-id="a48b0-141">Run hello following command from hello SSH prompt:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    <span data-ttu-id="a48b0-142">Ciò dovrebbe fornire un elenco di file e cartelle in hello account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a48b0-142">This should provide a list of files/folders in hello Data Lake Store account.</span></span>

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a><span data-ttu-id="a48b0-143">Importare dati da un database SQL di Azure ad Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="a48b0-143">Import data from Azure SQL Database into Data Lake Store</span></span>
1. <span data-ttu-id="a48b0-144">Passare toohello directory in cui sono disponibili i pacchetti Sqoop.</span><span class="sxs-lookup"><span data-stu-id="a48b0-144">Navigate toohello directory where Sqoop packages are available.</span></span> <span data-ttu-id="a48b0-145">In genere, questa corrisponde a `/usr/hdp/<version>/sqoop/bin`.</span><span class="sxs-lookup"><span data-stu-id="a48b0-145">Typically, this will be at `/usr/hdp/<version>/sqoop/bin`.</span></span>
2. <span data-ttu-id="a48b0-146">Importare i dati hello **Table1** in hello account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a48b0-146">Import hello data from **Table1** into hello Data Lake Store account.</span></span> <span data-ttu-id="a48b0-147">Utilizzare la seguente sintassi hello:</span><span class="sxs-lookup"><span data-stu-id="a48b0-147">Use hello following syntax:</span></span>

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    <span data-ttu-id="a48b0-148">Si noti che **nome server di database sql** segnaposto rappresenta il nome di hello del server di hello in database SQL di Azure hello è in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a48b0-148">Note that **sql-database-server-name** placeholder represents hello name of hello server where hello Azure SQL database is running.</span></span> <span data-ttu-id="a48b0-149">**nome di database SQL** segnaposto rappresenta hello nome effettivo del database.</span><span class="sxs-lookup"><span data-stu-id="a48b0-149">**sql-database-name** placeholder represents hello actual database name.</span></span>

    <span data-ttu-id="a48b0-150">Ad esempio,</span><span class="sxs-lookup"><span data-stu-id="a48b0-150">For example,</span></span>


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. <span data-ttu-id="a48b0-151">Verificare che hello dati sono stati trasferiti account archivio Data Lake toohello.</span><span class="sxs-lookup"><span data-stu-id="a48b0-151">Verify that hello data has been transferred toohello Data Lake Store account.</span></span> <span data-ttu-id="a48b0-152">Eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a48b0-152">Run hello following command:</span></span>

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    <span data-ttu-id="a48b0-153">Verrà visualizzato dopo l'output di hello.</span><span class="sxs-lookup"><span data-stu-id="a48b0-153">You should see hello following output.</span></span>


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    <span data-ttu-id="a48b0-154">Ogni **parte-m -*** file corrisponde tooa riga nella tabella di origine, hello **Table1**.</span><span class="sxs-lookup"><span data-stu-id="a48b0-154">Each **part-m-*** file corresponds tooa row in hello source table, **Table1**.</span></span> <span data-ttu-id="a48b0-155">È possibile visualizzare il contenuto di hello parte hello - m-* file tooverify.</span><span class="sxs-lookup"><span data-stu-id="a48b0-155">You can view hello contents of hello part-m-* files tooverify.</span></span>


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a><span data-ttu-id="a48b0-156">Esportare dati da Archivio Data Lake a un database SQL di Azure </span><span class="sxs-lookup"><span data-stu-id="a48b0-156">Export data from Data Lake Store into Azure SQL Database</span></span>
1. <span data-ttu-id="a48b0-157">Esportare i dati di hello dalla tabella vuota toohello account archivio Data Lake, **Table2**, nel Database SQL di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a48b0-157">Export hello data from Data Lake Store account toohello empty table, **Table2**, in hello Azure SQL Database.</span></span> <span data-ttu-id="a48b0-158">Utilizzare la seguente sintassi hello.</span><span class="sxs-lookup"><span data-stu-id="a48b0-158">Use hello following syntax.</span></span>

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    <span data-ttu-id="a48b0-159">Ad esempio,</span><span class="sxs-lookup"><span data-stu-id="a48b0-159">For example,</span></span>


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. <span data-ttu-id="a48b0-160">Verificare che hello dati è stati caricata toohello tabella del Database SQL.</span><span class="sxs-lookup"><span data-stu-id="a48b0-160">Verify that hello data was uploaded toohello SQL Database table.</span></span> <span data-ttu-id="a48b0-161">Utilizzare [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) o Visual Studio tooconnect toohello Database SQL di Azure e quindi hello esecuzione eseguendo query.</span><span class="sxs-lookup"><span data-stu-id="a48b0-161">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio tooconnect toohello Azure SQL Database and then run hello following query.</span></span>

        SELECT * FROM TABLE2

    <span data-ttu-id="a48b0-162">Dovrebbe avere hello output seguente.</span><span class="sxs-lookup"><span data-stu-id="a48b0-162">This should have hello following output.</span></span>

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a><span data-ttu-id="a48b0-163">Considerazioni sulle prestazioni per l'uso di Sqoop</span><span class="sxs-lookup"><span data-stu-id="a48b0-163">Performance considerations while using Sqoop</span></span>

<span data-ttu-id="a48b0-164">Per l'ottimizzazione del Sqoop processo archivio toocopy data tooData Lake, vedere [documento prestazioni Sqoop](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span><span class="sxs-lookup"><span data-stu-id="a48b0-164">For performance tuning your Sqoop job toocopy data tooData Lake Store, see [Sqoop performance document](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span></span>

## <a name="see-also"></a><span data-ttu-id="a48b0-165">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="a48b0-165">See also</span></span>
* [<span data-ttu-id="a48b0-166">Copiare i dati da un archivio Azure archiviazione BLOB tooData Lake</span><span class="sxs-lookup"><span data-stu-id="a48b0-166">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="a48b0-167">Proteggere i dati in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a48b0-167">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="a48b0-168">Usare Azure Data Lake Analytics con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a48b0-168">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="a48b0-169">Usare Azure HDInsight con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a48b0-169">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
