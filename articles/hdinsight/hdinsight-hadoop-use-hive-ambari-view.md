---
title: aaaUse Ambari viste toowork con Hive in HDInsight (Hadoop) - Azure | Documenti Microsoft
description: Informazioni su come toouse hello Hive vista dalle query Hive toosubmit browser web. Hello Hive visualizzazione fa parte di hello che dell'interfaccia utente Web Ambari fornito con il cluster HDInsight basati su Linux.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1abe9104-f4b2-41b9-9161-abbc43de8294
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: f9a77b652e70d34a0ff9165fbb8c2e16d3401ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-hive-view-with-hadoop-in-hdinsight"></a>Utilizzare hello vista Hive con Hadoop in HDInsight

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Informazioni su come una query utilizza la visualizzazione Hive Ambari toorun Hive. Ambari è un'utilità per la gestione e il monitoraggio fornita con i cluster HDInsight basati su Linux. Una delle funzionalità di hello fornita tramite Ambari è un'interfaccia utente Web che può essere una query Hive toorun utilizzato.

> [!NOTE]
> Ambari include numerose funzionalità non illustrate in questo documento. Per ulteriori informazioni, vedere [HDInsight gestire cluster utilizzando l'interfaccia utente Web Ambari hello](hdinsight-hadoop-manage-ambari.md).

## <a name="prerequisites"></a>Prerequisiti

* Un cluster HDInsight basato su Linux. Per informazioni sulla creazione di un cluster, vedere [Introduzione all'uso di Hadoop con Hive in HDInsight in Linux](hdinsight-hadoop-linux-tutorial-get-started.md).

> [!IMPORTANT]
> passaggi di Hello in questo documento richiedono un cluster HDInsight che utilizza Linux. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="open-hello-hive-view"></a>Aprire la visualizzazione di Hive hello

È possibile Ambari viste dal portale di Azure; hello Selezionare il cluster HDInsight e quindi **Ambari viste** da hello **collegamenti rapidi** sezione.

![sezione collegamenti rapidi del portale hello](./media/hdinsight-hadoop-use-hive-ambari-view/quicklinks.png)

Hello l'elenco delle visualizzazioni, selezionare hello __Hive vista__.

![Hello Hive visualizzazione selezionata](./media/hdinsight-hadoop-use-hive-ambari-view/select-hive-view.png)

> [!NOTE]
> Quando si accede a Ambari, verrà richiesta tooauthenticate toohello sito. Immettere salve (impostazione predefinita `admin`) del cluster di hello nome e la password utilizzati per la creazione di account.

Verrà visualizzato un toohello simile pagina seguente immagine:

![Immagine di foglio di lavoro di query hello per Vista Hive hello](./media/hdinsight-hadoop-use-hive-ambari-view/ambari-hive-view.png)

## <a name="hivequery"></a>Eseguire una query

toorun una query hive, usare hello dalla visualizzazione Hive hello come segue.

1. Da hello __Query__ scheda, incollare hello seguendo le istruzioni HiveQL nel foglio di lavoro hello:

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS cnt FROM log4jLogs WHERE t4 = '[ERROR]' GROUP BY t4;
    ```

    Queste istruzioni consentono di eseguire hello seguenti azioni:

   * `DROP TABLE`: Elimina tabella hello e file di dati hello, nel caso in cui hello tabella esiste già.

   * `CREATE EXTERNAL TABLE`: crea una nuova tabella "esterna" in Hive.
   Le tabelle esterne archiviano solo definizione della tabella hello nell'Hive. dati Hello viene lasciati nella posizione originale hello.

   * `ROW FORMAT`-Modalità hello di formattazione. In questo caso, i campi di hello in ogni log sono separati da uno spazio.

   * `STORED AS TEXTFILE LOCATION`-Hello memorizzazione dei dati e che viene archiviato come testo.

   * `SELECT`-Seleziona un conteggio di tutte le righe in cui t4 colonna contiene il valore di hello [errore].

     > [!NOTE]
     > Le tabelle esterne da utilizzare quando si prevede di hello sottostante toobe dati aggiornati da un'origine esterna. Ad esempio, un processo di caricamento dati automatizzato o un'altra operazione MapReduce. Eliminazione di una tabella esterna *non* eliminare dati hello e definizione della tabella solo hello.

    > [!IMPORTANT]
    > Lasciare hello __Database__ selezione in __predefinito__. esempi di Hello in questo documento usano database predefinito hello incluso in HDInsight.

2. query hello toostart, utilizzare hello **Execute** pulsante foglio di lavoro hello. Le modifiche al testo arancione e hello diventa troppo**arrestare**.

3. Al termine di query hello, hello **risultati** scheda Visualizza risultati di hello dell'operazione di hello. Dopo il testo Hello è il risultato di hello di query hello:

        sev       cnt
        [ERROR]   3

    Hello **registri** scheda può essere utilizzato tooview informazioni di registrazione di hello create dal processo di hello.

   > [!TIP]
   > Hello **salvare i risultati** finestra di dialogo di riepilogo a discesa in hello superiore sinistra del hello **risultati della Query processo** sezione permette toodownload o salvare i risultati.

4. Selezionare hello prime quattro righe di questa query, quindi selezionare **Execute**. Si noti che non sono presenti risultati al termine il processo di hello. Utilizzo di hello **Execute** pulsante se fa parte di query hello è selezionata solo esecuzioni hello istruzioni selezionate. In questo caso, selezione hello non include l'istruzione finale hello che recupera le righe dalla tabella hello. Se si seleziona solo tale riga e utilizzare **Execute**, si otterranno risultati hello previsto.

5. tooadd un foglio di lavoro, utilizzare hello **nuovo foglio di lavoro** pulsante nella parte inferiore di hello di hello **Editor di Query**. In hello nuovo foglio di lavoro, immettere hello seguendo le istruzioni HiveQL:

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';
    ```

  Queste istruzioni consentono di eseguire hello seguenti azioni:

   * **CREATE TABLE IF NOT EXISTS** : crea una tabella, se non esiste già. Poiché hello **esterno** parola chiave non viene utilizzato, viene creata una tabella interna. Una tabella interna verrà archiviata nel data warehouse di hello Hive e completamente gestita da Hive. A differenza delle tabelle esterne, eliminazione di una tabella interna Elimina hello anche i dati sottostanti.

   * **ARCHIVIATI AS ORC** -archivia i dati di hello in formato con ottimizzazione per la riga a colonne (ORC). ORC è un formato altamente ottimizzato ed efficiente per l'archiviazione di dati Hive.

   * **INSERT OVERWRITE ... Selezionare** -seleziona le righe da hello **log4jLogs** tabella contenenti `[ERROR]`, e quindi inserisce hello dati in hello **degli errori** tabella.

     Hello utilizzare **Execute** pulsante toorun questa query. Hello **risultati** scheda non contiene alcuna informazione hello query restituisce zero righe. deve essere stato Hello **SUCCEEDED** una volta completata la query hello.

### <a name="visual-explain"></a>Visual Explain

una visualizzazione del piano di query hello, seleziona hello toodisplay **spiegare Visual** scheda di sotto del foglio di lavoro di hello.

Hello **spiegare Visual** visualizzazione di query hello può essere utili per capire il flusso di hello di query complesse. È possibile visualizzare un equivalente testuale di questa vista utilizzando hello **esplicativo** pulsante hello Editor di Query.

### <a name="tez-ui"></a>Interfaccia utente di Tez

toodisplay hello Tez UI per query hello, seleziona hello **Tez** scheda di sotto del foglio di lavoro di hello.

> [!IMPORTANT]
> Tez è tooresolve non in uso tutte le query. Molte query possono essere risolte senza usare Tez. 

Se Tez query hello tooresolve usato, viene visualizzato hello descritto grafico aciclico diretto (DAG). Se si desidera tooview hello DAG per query è stato eseguito in hello precedente o eseguire il debug hello Tez processo, utilizzare hello [Tez vista](hdinsight-debug-ambari-tez-view.md) invece.

## <a name="view-job-history"></a>Visualizzare la cronologia processo

Hello __processi__ scheda Visualizza una cronologia delle query Hive.

![Immagine di cronologia processo hello](./media/hdinsight-hadoop-use-hive-ambari-view/job-history.png)

## <a name="database-tables"></a>Tabelle di database

È possibile utilizzare hello __tabelle__ scheda toowork con le tabelle all'interno di un database Hive.

![Immagine della scheda tabelle hello](./media/hdinsight-hadoop-use-hive-ambari-view/tables.png)

## <a name="saved-queries"></a>Query salvate

Dalla scheda Query hello, è possibile salvare le query. Dopo il salvataggio, è possibile riutilizzare query hello da hello __query salvate__ scheda.

![Immagine della scheda delle query salvate](./media/hdinsight-hadoop-use-hive-ambari-view/saved-queries.png)

## <a name="user-defined-functions"></a>Funzioni definite dall'utente

Hive può anche essere esteso tramite funzioni definite dall'utente, Una funzione definita dall'utente consente a funzionalità tooimplement o logica che non è facilmente modellata in HiveQL.

scheda definita dall'utente nella parte superiore di hello di hello Hive vista Hello consente toodeclare e salvare un set di funzioni definite dall'utente. Queste funzioni definite dall'utente può essere utilizzato con hello **Editor di Query**.

![Immagine della scheda delle funzioni definite dall'utente](./media/hdinsight-hadoop-use-hive-ambari-view/user-defined-functions.png)

Dopo aver aggiunto un toohello funzione definita dall'utente, vista Hive, un **inserire funzioni definite dall'utente** pulsante viene visualizzato nella parte inferiore di hello di hello **Editor di Query**. Selezionando questa voce visualizza un elenco di riepilogo a discesa di funzioni definite dall'utente definito nella vista Hive hello hello. Selezione di una funzione definita dall'utente aggiunge HiveQL istruzioni tooyour query tooenable hello funzione definita dall'utente.

Ad esempio, se è stata definita una funzione definita dall'utente con hello le proprietà seguenti:

* Nome della risorsa: myudfs

* Percorso della risorsa: /myudfs.jar

* Nome della funzione definita dall'utente: myawesomeudf

* Nome della classe per la funzione definita dall'utente: com.myudfs.Awesome

Utilizzando hello **inserire funzioni definite dall'utente** pulsante Visualizza una voce denominata **myudfs**, con un altro elenco a discesa per ogni funzione definita dall'utente definito per tale risorsa. In questo caso, **myawesomeudf**. Selezionando questa voce aggiunge hello toohello inizio della query hello seguenti:

```hiveql
add jar /myudfs.jar;
create temporary function myawesomeudf as 'com.myudfs.Awesome';
```

È quindi possibile utilizzare hello funzione definita dall'utente nella query. ad esempio `SELECT myawesomeudf(name) FROM people;`.

Per ulteriori informazioni sull'utilizzo di funzioni definite dall'utente con Hive in HDInsight, vedere hello seguenti documenti:

* [Usare Python con Hive e Pig in HDInsight](hdinsight-python.md)
* [Come tooadd un tooHDInsight Hive definita dall'utente personalizzato](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

## <a name="hive-settings"></a>Settings di Hive

Le impostazioni possono essere utilizzati toochange varie impostazioni di Hive. Modifica, ad esempio, il motore di esecuzione hello per Hive da tooMapReduce Tez (impostazione predefinita hello).

## <a id="nextsteps"></a>Passaggi successivi

Per informazioni generali su Hive in HDInsight:

* [Usare Hive con Hadoop in HDInsight](hdinsight-use-hive.md)

Per informazioni su altre modalità d'uso di Hadoop in HDInsight:

* [Usare Pig con Hadoop in HDInsight](hdinsight-use-pig.md)
* [Usare MapReduce con Hadoop in HDInsight](hdinsight-use-mapreduce.md)
