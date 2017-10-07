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
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a>Copiare i dati tra Archivio Data Lake e un database SQL di Azure tramite Sqoop
Informazioni su come toouse Sqoop Apache tooimport ed esportare dati tra Database SQL di Azure e archivio Data Lake.

## <a name="what-is-sqoop"></a>Informazioni su Sqoop
Le applicazioni Big Data sono una scelta naturale per l'elaborazione di dati non strutturati e semi-strutturati, ad esempio log e file. Tuttavia, è inoltre possibile un necessità tooprocess strutturato i dati archiviati nei database relazionali.

[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) è un tootransfer strumento progettato dati tra i database relazionali e di un repository di dati di grandi dimensioni, ad esempio archivio Data Lake. È possibile utilizzare dati tooimport da un sistema di gestione di database relazionali (RDBMS), ad esempio Database SQL di Azure in archivio Data Lake. È possibile quindi trasformano e analizzare i dati di hello utilizzando i carichi di lavoro di big data e quindi esportare i dati di hello in un sistema RDBMS. In questa esercitazione, si utilizza un Database di SQL Azure come tooimport/esportazione del database relazionale da.

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questo articolo, è necessario disporre delle seguenti hello:

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Un account Azure Data Lake Store**. Per istruzioni su come toocreate uno, vedere [introduzione archivio Azure Data Lake](data-lake-store-get-started-portal.md)
* **Cluster di Azure HDInsight** con accesso tooa account archivio Data Lake. Vedere [Creare un cluster HDInsight con Data Lake Store tramite il portale di Azure](data-lake-store-hdinsight-hadoop-use-portal.md). Questo articolo presuppone che si abbia un cluster HDInsight Linux con accesso ad Archivio Data Lake.
* **Database SQL di Azure**. Per istruzioni su come toocreate uno, vedere [creare un database SQL di Azure](../sql-database/sql-database-get-started.md)

## <a name="do-you-learn-fast-with-videos"></a>Apprendimento rapido con i video
[Guardare questo video](https://mix.office.com/watch/1butcdjxmu114) sulla toocopy dati tra il BLOB di archiviazione di Azure e archivio Data Lake tramite DistCp.

## <a name="create-sample-tables-in-hello-azure-sql-database"></a>Creare tabelle di esempio in hello Database SQL di Azure
1. toostart, creare due tabelle di esempio in hello Database SQL di Azure. Utilizzare [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) o Visual Studio tooconnect toohello Database SQL di Azure e quindi eseguire hello seguendo le query.

    **Create Table1**

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

    **Create Table2**

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
2. In **Table1**aggiungere alcuni dati di esempio. Lasciare vuota **Table2** . Verranno importati dati da **Table1** ad Archivio Data Lake. Quindi, verranno esportati dati da Archivio Data Lake a **Table2**. Eseguire hello seguente frammento di codice.

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-toodata-lake-store"></a>Utilizzare Sqoop da un cluster di HDInsight con accesso tooData Lake archivio
Un cluster HDInsight dispone già di pacchetti Sqoop hello disponibili. Se è stata configurata l'archivio Data Lake toouse cluster HDInsight hello come un'ulteriore spazio di archiviazione, è possibile utilizzare Sqoop (senza apportare modifiche di configurazione) tooimport ed esportare dati tra un database relazionale (in questo esempio, Database SQL di Azure) e un archivio Data Lake account.

1. Per questa esercitazione, si presuppone che un cluster Linux è stato creato è necessario utilizzare SSH tooconnect toohello cluster. Vedere [cluster HDInsight basati su Linux di Connect tooa](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).
2. Verificare se sia possibile accedere hello account archivio Data Lake dal cluster hello. Eseguire hello comando seguente dal prompt dei comandi di hello SSH:

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    Ciò dovrebbe fornire un elenco di file e cartelle in hello account archivio Data Lake.

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a>Importare dati da un database SQL di Azure ad Archivio Data Lake
1. Passare toohello directory in cui sono disponibili i pacchetti Sqoop. In genere, questa corrisponde a `/usr/hdp/<version>/sqoop/bin`.
2. Importare i dati hello **Table1** in hello account archivio Data Lake. Utilizzare la seguente sintassi hello:

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    Si noti che **nome server di database sql** segnaposto rappresenta il nome di hello del server di hello in database SQL di Azure hello è in fase di esecuzione. **nome di database SQL** segnaposto rappresenta hello nome effettivo del database.

    Ad esempio,


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. Verificare che hello dati sono stati trasferiti account archivio Data Lake toohello. Eseguire hello comando seguente:

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    Verrà visualizzato dopo l'output di hello.


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    Ogni **parte-m -*** file corrisponde tooa riga nella tabella di origine, hello **Table1**. È possibile visualizzare il contenuto di hello parte hello - m-* file tooverify.


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a>Esportare dati da Archivio Data Lake a un database SQL di Azure 
1. Esportare i dati di hello dalla tabella vuota toohello account archivio Data Lake, **Table2**, nel Database SQL di Azure hello. Utilizzare la seguente sintassi hello.

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    Ad esempio,


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. Verificare che hello dati è stati caricata toohello tabella del Database SQL. Utilizzare [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) o Visual Studio tooconnect toohello Database SQL di Azure e quindi hello esecuzione eseguendo query.

        SELECT * FROM TABLE2

    Dovrebbe avere hello output seguente.

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a>Considerazioni sulle prestazioni per l'uso di Sqoop

Per l'ottimizzazione del Sqoop processo archivio toocopy data tooData Lake, vedere [documento prestazioni Sqoop](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).

## <a name="see-also"></a>Vedere anche
* [Copiare i dati da un archivio Azure archiviazione BLOB tooData Lake](data-lake-store-copy-data-azure-storage-blob.md)
* [Proteggere i dati in Data Lake Store](data-lake-store-secure-data.md)
* [Usare Azure Data Lake Analytics con Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Usare Azure HDInsight con Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
