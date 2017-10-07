---
title: aaaCreate Hive tabelle e caricare i dati dall'archiviazione Blob di Azure | Documenti Microsoft
description: Creare tabelle Hive e caricare i dati nelle tabelle toohive blob
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: cff9280d-18ce-4b66-a54f-19f358d1ad90
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 09622972bcac31c2971858393a8340f24e4b7390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a>Creare tabelle Hive e caricare i dati dall'archiviazione BLOB di Azure
Questo argomento presenta le query Hive generiche che consentono di creare tabelle Hive e di caricare i dati dall'archiviazione BLOB di Azure. Vengono inoltre forniti alcune indicazioni sul partizionamento di tabelle Hive e sull'utilizzo di hello con ottimizzazione per la riga a colonne (ORC) formattazione tooimprove le prestazioni delle query.

Questo **menu** collegamenti tootopics che descrivono come dati tooingest in ambienti di destinazione in cui i dati hello possono essere archiviati ed elaborati durante hello Team Data Science processo (TDSP).

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a>Prerequisiti
Questo articolo presuppone che l'utente abbia:

* Creato un account di archiviazione di Azure. Per istruzioni, vedere [Informazioni sugli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md).
* Il provisioning di un cluster Hadoop personalizzato con hello servizio HDInsight.  Per istruzioni, vedere [Personalizzazione di cluster Hadoop di Azure HDInsight per l'analisi scientifica dei dati](machine-learning-data-science-customize-hadoop-cluster.md).
* Cluster toohello di accesso remoto abilitato, effettuato l'accesso, aprire console della riga di comando di hello Hadoop. Se sono necessarie istruzioni, vedere [hello accesso nodo Head del Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).

## <a name="upload-data-tooazure-blob-storage"></a>Carica l'archiviazione blob di dati tooAzure
Se una macchina virtuale di Azure è stato creato tramite istruzioni hello fornite [configurare una macchina virtuale di Azure per analitica avanzate](machine-learning-data-science-setup-virtual-machine.md), questo script dovrebbe essere stato scaricato toohello *c:\\ Gli utenti\\\<nome utente\>\\documenti\\gli script di analisi scientifica dei dati* directory sulla macchina virtuale hello. Queste query Hive richiedono soltanto che si collega la propria schema dei dati e la configurazione dell'archiviazione blob di Azure in hello campi appropriati toobe pronto per l'invio.

Si supponga che i dati di hello per le tabelle Hive siano un **non compresso** formato tabulare e che i dati di hello sono stati caricati toohello predefinita (o tooan aggiuntive) contenitore hello dell'account di archiviazione utilizzato da un cluster Hadoop hello.

Se si desidera toopractice su hello **NYC Taxi viaggi dati**, è necessario:

* **scaricare** hello 24 [NYC Taxi viaggi dati](http://www.andresmh.com/nyctaxitrips) file (12 di andata e ritorno e file file tariffa 12)
* **decomprimere** tutti i file in file con estensione .csv;
* **caricare** li toohello predefinito o il contenitore appropriato di hello account di archiviazione di Azure che è stato creato da hello procedura hello [cluster personalizzare Azure HDInsight Hadoop per il processo di Analitica avanzate e tecnologia ](machine-learning-data-science-customize-hadoop-cluster.md) argomento. Hello processo tooupload hello CSV file toohello predefinito contenitore nell'account di archiviazione hello è disponibile su questo [pagina](machine-learning-data-science-process-hive-walkthrough.md#upload).

## <a name="submit"></a>La modalità query Hive toosubmit
È possibile inviare query Hive mediante:

1. [Inviare le query Hive attraverso la riga di comando di Hadoop nel nodo head del cluster Hadoop](#headnode)
2. [Inviare query Hive con hello Editor Hive](#hive-editor)
3. [Inviare le query Hive con i comandi di Azure PowerShell](#ps)

Le query Hive sono simili a SQL. Se si ha familiarità con SQL, è possibile hello [Hive per SQL utenti irregolarità foglio](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) utile.

Quando si invia una query Hive, è inoltre possibile controllare destinazione hello dell'output di hello dalle query Hive, sia su hello schermata o tooa file locale nel nodo head hello o tooan blob di Azure.

### <a name="headnode"></a> 1. Inviare le query Hive attraverso la riga di comando di Hadoop nel nodo head del cluster Hadoop
Se l'Hive hello query è complessa, invio che direttamente nel nodo head di hello del cluster Hadoop hello in genere comporta toofaster inversione di inviarla con un Editor Hive o gli script di PowerShell di Azure.

Accedi toohello nodo head del cluster Hadoop hello, aprire hello riga di comando di Hadoop nel desktop di hello del nodo head hello e immettere comando `cd %hive_home%\bin`.

Sono presenti query Hive di tre modi toosubmit hello Hadoop della riga di comando:

* Direttamente
* Mediante i file con estensione hql
* con hello Hive console dei comandi

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a>Inviare query Hive direttamente nella riga di comando di Hadoop
È possibile eseguire comandi come `hive -e "<your hive query>;` toosubmit query Hive semplici direttamente in Hadoop riga di comando. Di seguito è riportato un esempio, in strutture di casella rossa hello hello comando che invia query Hive hello e hello casella verde contorni hello output dalla query Hive hello.

![Creare un'area di lavoro](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a>Inviare query nei file con estensione hql
Quando query Hive hello è più complicato e dispone di più righe, la modifica delle query nella riga di comando o la console di Hive comando non è pratica. In alternativa è toouse un editor di testo nel nodo head hello hello Hadoop cluster toosave hello le query Hive in un file .hql in una directory locale del nodo head hello. Quindi query Hive hello nel file .hql hello possono essere inviate utilizzando hello `-f` argomento come indicato di seguito:

    hive -f "<path toohello .hql file>"

![Creare un'area di lavoro](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

**Eliminare la visualizzazione relativa allo stato di avanzamento delle query Hive sullo schermo**

Per impostazione predefinita, dopo l'invio query Hive nella riga di comando di Hadoop, lo stato di avanzamento hello del processo MapReduce hello viene stampato nella schermata. toosuppress hello stampa schermata di avanzamento del processo MapReduce hello, è possibile usare un argomento `-S` ("S" in lettere maiuscole) in hello riga di comando come segue:

    hive -S -f "<path toohello .hql file>"
.    hive -S -e "<Hive queries>"

#### <a name="submit-hive-queries-in-hive-command-console"></a>Inviare query Hive nella console dei comandi di Hive
È possibile immettere anche prima console dei comandi Hive hello eseguendo comando `hive` nella riga di comando di Hadoop e quindi inviare le query Hive nel Hive console dei comandi. Di seguito è fornito un esempio. In questo esempio hello due caselle rosse evidenziazione hello comandi utilizzati tooenter hello console dei comandi di Hive e hello query Hive inviato nella console di comando Hive, rispettivamente. casella Hello verde evidenzia l'output di hello dalla query Hive hello.

![Creare un'area di lavoro](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

Negli esempi precedenti Hello output direttamente risultati della query Hive hello sullo schermo. È anche possibile scrivere file locale tooa output di hello nel nodo head hello o tooan blob di Azure. È quindi possibile utilizzare altri strumenti toofurther analizzare l'output di hello di query Hive.

**L'output di file locale tooa risultati query Hive.**
toooutput Hive query risultati tooa directory locale nel nodo head hello, sono presenti query Hive di hello toosubmit hello Hadoop della riga di comando come segue:

    hive -e "<hive query>" > <local path in hello head node>

Nell'esempio seguente di hello, output di hello di query Hive viene scritto in un file `hivequeryoutput.txt` nella directory `C:\apps\temp`.

![Creare un'area di lavoro](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

**Tooan risultati di query Hive output blob di Azure**

È anche possibile produrre tooan risultati di query Hive hello blob di Azure, all'interno del contenitore predefinito hello del cluster Hadoop hello. query Hive Hello per questo è il seguente:

    insert overwrite directory wasb:///<directory within hello default container> <select clause from ...>

Nell'esempio seguente di hello, output di hello di query Hive viene scritto directory blob tooa `queryoutputdir` all'interno del contenitore predefinito hello del cluster Hadoop hello. In questo caso, è necessario solo nome di directory hello tooprovide, senza nome blob hello. Viene generato un errore se si specificano i nomi della directory e del BLOB, ad esempio `wasb:///queryoutputdir/queryoutput.txt`.

![Creare un'area di lavoro](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

Se si apre il contenitore predefinito hello del cluster Hadoop hello tramite Esplora archivi Azure, è possibile visualizzare l'output di hello della query Hive hello come illustrato nella seguente illustrazione hello. È possibile applicare hello filtro (evidenziato in casella rossa) tooonly recuperare hello blob con le lettere nei nomi specificate.

![Creare un'area di lavoro](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <a name="hive-editor"></a> 2. Inviare query Hive con hello Editor Hive
È inoltre possibile utilizzare la Console di Query (Editor Hive) hello immettendo un URL di form hello *https://&#60; Nome del cluster Hadoop >.azurehdinsight.net/Home/HiveEditor* in un web browser. È necessario essere registrati in hello vedere questa console e pertanto è necessario qui le credenziali del cluster Hadoop.

### <a name="ps"></a> 3. Inviare le query Hive con i comandi di Azure PowerShell
È anche possibile utilizzare le query Hive toosubmit di PowerShell. Per istruzioni, vedere [Invio di processi Hive tramite PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).

## <a name="create-tables"></a>Creare il database e le tabelle Hive
Hello query Hive vengono condivisi in hello [repository GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) e può essere scaricato da qui.

Ecco query Hive hello che crea una tabella Hive.

    create database if not exists <database name>;
    CREATE EXTERNAL TABLE if not exists <database name>.<table name>
    (
        field1 string,
        field2 int,
        field3 float,
        field4 double,
        ...,
        fieldN string
    )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' lines terminated by '<line separator>'
    STORED AS TEXTFILE LOCATION '<storage location>' TBLPROPERTIES("skip.header.line.count"="1");

Ecco le descrizioni di hello dei campi hello tooplug in necessari e altre configurazioni:

* **&#60; nome database >**: nome hello del database di hello che si desidera toocreate. Se si desidera database predefinito di hello toouse, hello query *creare database...*  può essere omesso.
* **&#60; nome tabella >**: nome hello della tabella di hello che si desidera toocreate all'interno del database specificato hello. Se si desidera toouse hello predefinito database, tabella hello può fare riferimento direttamente *&#60; nome tabella >* senza &#60; nome database >.
* **&#60; separatore di campo >**: separatore hello che delimita i campi in hello dati file toobe caricato tabella Hive toohello.
* **&#60; il separatore di riga >**: separatore hello che delimita le righe nel file di dati hello.
* **&#60; percorso di archiviazione >**: hello dati toosave hello percorso di archiviazione di Azure di tabelle Hive. Se non si specifica *posizione &#60; percorso di archiviazione >*, hello database e hello tabelle vengono archiviate in *hive/warehouse/* directory nel contenitore predefinito hello del cluster di Hive hello per impostazione predefinita. Se si desidera una posizione di archiviazione hello toospecify, hello percorso di archiviazione toobe all'interno del contenitore predefinito hello per le tabelle e database hello. Questa posizione è definito come contenitore predefinito di toohello relativo percorso di cluster hello in formato hello del toobe *' wasb: / / / &#60; directory 1 > /'* o *' wasb: / / / &#60; directory 1 > / &#60; Directory 2 > /'*e così via. Dopo l'esecuzione di query hello, le relative directory hello vengono create all'interno del contenitore predefinito hello.
* **TBLPROPERTIES("Skip.Header.Line.Count"="1")**: se il file di dati hello dispone di una riga di intestazione, questa proprietà è necessario tooadd **alla fine di hello** di hello *Crea tabella* query. In caso contrario, la riga di intestazione hello viene caricata come una tabella di record toohello. Se il file di dati di hello non dispone di una riga di intestazione, questa configurazione può essere omesso nella query hello.

## <a name="load-data"></a>Caricare dati tooHive tabelle
Ecco query Hive hello che carica i dati in una tabella Hive.

    LOAD DATA INPATH '<path tooblob data>' INTO TABLE <database name>.<table name>;

* **&#60; i dati del percorso tooblob >**: hello se tabella Hive toohello di hello blob file toobe caricato nel contenitore predefinito hello di hello cluster HDInsight Hadoop, *&#60; i dati del percorso tooblob >* deve essere nel formato hello *' wasb: / / / &#60; directory in questo contenitore > / &#60; il nome di file blob >'*. file blob Hello può anche essere in un contenitore aggiuntivo del cluster HDInsight Hadoop hello. In questo caso, *&#60; i dati del percorso tooblob >* deve essere nel formato hello *' wasb: / / &#60; nome contenitore > @&#60; nome account di archiviazione >.blob.core.windows.net/ &#60; il nome di file blob >'*.

  > [!NOTE]
  > Hello blob caricato toobe tooHive tabella dati dispone di toobe predefinito hello o contenitori hello dell'account di archiviazione per cluster Hadoop hello. In caso contrario, hello *Carica dati* query si verifica un errore che segnala che l'impossibilità di accedere dati hello.
  >
  >

## <a name="partition-orc"></a>Argomenti avanzati: Tabella partizionata e archiviazione dei dati Hive in formato ORC
Se i dati di hello sono grandi, partizionamento tabella hello è utile per le query che richiedono solo tooscan alcune partizioni della tabella hello. È ad esempio, dati del log hello toopartition ragionevole di un sito web per le date.

In aggiunta toopartitioning Hive tabelle, è inoltre utile toostore hello Hive dati di formato con ottimizzazione per la riga a colonne (ORC) hello. Per altre informazioni sulla formattazione ORC, vedere l’<a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">uso dei file ORC per migliorare le prestazioni quando Hive legge, scrive ed elabora dati</a>.

### <a name="partitioned-table"></a>Tabella partizionata
Ecco query Hive hello che crea una tabella partizionata e caricare i dati.

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

Quando una query su tabelle partizionate, è consigliabile tooadd hello partizione condizione hello **inizio** di hello `where` clausola come ciò migliora l'efficacia hello di ricerca in modo significativo.

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <a name="orc"></a>Archiviare i dati Hive in formato ORC
È possibile caricare direttamente dati dall'archiviazione blob in tabelle Hive archiviati in formato ORC hello. Ecco i passaggi di hello che hello sono necessari dati tooload tootake da Azure BLOB tooHive tabelle archiviate in formato ORC.

Creare una tabella esterna **ARCHIVIATI file di testo AS** e caricare i dati dalla tabella toohello di archiviazione blob.

        CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<external textfile table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
            lines terminated by '<line separator>' STORED AS TEXTFILE
            LOCATION 'wasb:///<directory in Azure blob>' TBLPROPERTIES("skip.header.line.count"="1");

        LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<table name>;

Creare una tabella interna con hello stesso schema della tabella esterna hello nel passaggio 1, con hello stesso delimitatore di campo e archiviare hello Hive dati in formato ORC hello.

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

Selezionare i dati dalla tabella esterna di hello nel passaggio 1 e inserire nella tabella ORC hello

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> Se nella tabella file di testo hello *&#60; nome database >. &#60; nome della tabella file di testo esterna >* contiene partizioni, nel passaggio 3, hello `SELECT * FROM <database name>.<external textfile table name>` comando Seleziona hello variabile partizione come un campo in hello restituiti set di dati. Inserirlo nell'hello *&#60; nome database >. &#60; il nome di tabella ORC >* ha esito negativo poiché *&#60; nome database >. &#60; il nome di tabella ORC >* non dispone di una variabile di partizione hello come un campo nello schema di tabella hello. In questo caso, è necessario toospecifically hello selezionare campi toobe inserito troppo*&#60; nome database >. &#60; il nome di tabella ORC >* come indicato di seguito:
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

È sicuro toodrop hello *&#60; nome della tabella file di testo esterna >* quando hello seguente query dopo che tutti i dati di utilizzo è stato inserito in *&#60; nome database >. &#60; il nome di tabella ORC >*:

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

Dopo aver seguito questa procedura, è necessario utilizzare una tabella con dati in hello ORC formato pronto toouse.  
