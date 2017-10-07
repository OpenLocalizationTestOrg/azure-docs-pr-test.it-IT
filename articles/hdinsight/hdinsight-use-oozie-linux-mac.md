---
title: i flussi di lavoro di aaaUse Oozie Hadoop in HDInsight basati su Linux | Documenti Microsoft
description: Usare Oozie di Hadoop in HDInsight basati su Linux. Informazioni su come un flusso di lavoro, Oozie toodefine e inviare un processo di Oozie.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d7603471-5076-43d1-8b9a-dbc4e366ce5d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: larryfr
ms.openlocfilehash: cb5682837543312621e3424b7a9341b5d2a00bf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-oozie-with-hadoop-toodefine-and-run-a-workflow-on-linux-based-hdinsight"></a>Utilizzare Oozie con Hadoop toodefine ed eseguire un flusso di lavoro in HDInsight basati su Linux

[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

Informazioni su come toouse Oozie Apache con Hadoop in HDInsight. Apache Oozie è un sistema di flusso di lavoro/coordinamento che consente di gestire i processi Hadoop. Oozie è integrato con lo stack di Hadoop hello e supporta hello seguenti processi:

* Apache MapReduce
* Apache Pig
* Apache Hive
* Apache Sqoop

Oozie può essere anche i processi utilizzati tooschedule sistema tooa specifico, ad esempio programmi Java o gli script della shell

> [!NOTE]
> Un'altra opzione per definire i flussi di lavoro con HDInsight è Azure Data Factory. toolearn ulteriori informazioni su Data Factory di Azure, vedere [usare Pig e Hive con Data Factory][azure-data-factory-pig-hive].

> [!IMPORTANT]
> Oozie non è abilitato su HDInsight appartenente al dominio.

## <a name="prerequisites"></a>Prerequisiti

* **Un cluster di HDInsight**: vedere [Introduzione all'uso di HDInsight in Linux](hdinsight-hadoop-linux-tutorial-get-started.md)

  > [!IMPORTANT]
  > passaggi di Hello in questo documento richiedono un cluster HDInsight che utilizza Linux. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="example-workflow"></a>Esempio di flusso di lavoro

flusso di lavoro Hello utilizzato in questo documento contiene due azioni. Le azioni sono definizioni per attività, ad esempio l'esecuzione di Hive, Sqoop, MapReduce o altri processi:

![Diagramma del flusso di lavoro][img-workflow-diagram]

1. Un'azione di Hive esegue uno script HiveQL tooextract record da hello **hivesampletable** incluso in HDInsight. Ogni riga di dati descrive una visita da un dispositivo mobile specifico. formato di record Hello viene visualizzato toohello simile, il testo seguente:

        8       18:54:20        en-US   Android Samsung SCH-i500        California     United States    13.9204007      0       0
        23      19:19:44        en-US   Android HTC     Incredible      Pennsylvania   United States    NULL    0       0
        23      19:19:46        en-US   Android HTC     Incredible      Pennsylvania   United States    1.4757422       0       1

    Hello script Hive utilizzato in questo documento conta le visite totale hello per ogni piattaforma (ad esempio Android o iPhone) e archivia i conteggi hello tooa nuova tabella Hive.

    Per altre informazioni su Hive, vedere [Usare Hive con HDInsight][hdinsight-use-hive].

2. Un'azione Sqoop Esporta contenuto hello di hello nuova tabella tooa tabella Hive in un database SQL di Azure. Per altre informazioni su Sqoop, vedere [Usare Sqoop con Hadoop in HDInsight][hdinsight-use-sqoop].

> [!NOTE]
> Per le versioni Oozie supportate nei cluster HDInsight, vedere [novità introdotta nelle versioni di cluster Hadoop hello fornite da HDInsight][hdinsight-versions].

## <a name="create-hello-working-directory"></a>Creare la directory di lavoro hello

Oozie prevede che le risorse necessarie per un processo toobe archiviate in hello stessa directory. Questo esempio usa **wasb:///tutorials/useoozie**. Directory e directory di dati hello che contiene una tabella Hive nuovo hello creata da questo flusso di lavoro, utilizzare hello toocreate di comando seguente:

```
hdfs dfs -mkdir -p /tutorials/useoozie/data
```

> [!NOTE]
> Hello `-p` parametro fa sì che tutte le directory in hello percorso toobe creato. Hello **dati** directory è toohold utilizzati dati utilizzati da hello **useooziewf.hql** script.

Eseguire inoltre hello seguente comando, che assicura che Oozie può rappresentare l'account utente quando si eseguono processi Hive e Sqoop. Sostituire **USERNAME** con il proprio nome di accesso:

```
sudo adduser USERNAME users
```

> [!NOTE]
> È possibile ignorare gli errori di tale utente hello è già membro di hello `users` gruppo.

## <a name="add-a-database-driver"></a>Aggiungere un driver di database

Poiché questo flusso di lavoro utilizza Sqoop tooexport dati tooSQL Database, è necessario fornire che una copia del driver JDBC hello utilizzato tootalk tooSQL Database. Utilizzare hello seguenti toocopy comando è la directory di lavoro toohello:

```
hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /tutorials/useoozie/
```

Se il flusso di lavoro utilizzato altre risorse, ad esempio un file jar contenente un'applicazione di MapReduce, sarà necessario tooadd anche queste risorse.

## <a name="define-hello-hive-query"></a>Definire query Hive hello

Utilizzare hello seguendo i passaggi toocreate uno script HiveQL che definisce una query, che viene utilizzata in un flusso di lavoro Oozie più avanti in questo documento.

1. Connettere il cluster toohello tramite SSH. il comando seguente Hello è riportato un esempio dell'utilizzo di hello `ssh` comando. Sostituire __USERNAME__ con utente SSH hello per cluster hello. Sostituire __CLUSTERNAME__ con nome hello del cluster HDInsight hello.

    ```
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Da hello connessione SSH, utilizzare hello successivo comando toocreate un file:

    ```
    nano useooziewf.hql
    ```

3. Una volta verrà aperto l'editor nano hello usare hello seguente query come contenuto di hello del file hello:

    ```hiveql
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(deviceplatform string, count string) ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName} SELECT deviceplatform, COUNT(*) as count FROM hivesampletable GROUP BY deviceplatform;
    ```

    Esistono due variabili utilizzate nello script hello:

    * **${hiveTableName}**: contiene il nome di hello di hello tabella toobe creato

    * **${hiveDataFolder}**: hello percorso toostore hello i file di dati per la tabella hello contiene

    file di definizione del flusso di lavoro Hello (workflow in questa esercitazione) passa i valori toothis script HiveQL in fase di esecuzione

4. tooexit hello editor, premere Ctrl + X. Quando richiesto, selezionare **Y** toosave hello file, quindi utilizzare **invio** toouse hello **useooziewf.hql** nome file.

5. Seguente hello utilizzare comandi toocopy **useooziewf.hql** troppo**wasb:///tutorials/useoozie/useooziewf.hql**:

    ```
    hdfs dfs -put useooziewf.hql /tutorials/useoozie/useooziewf.hql
    ```

    Questi comandi archiviano hello **useooziewf.hql** nel file per archiviazione hello HDFS compatibile con cluster hello.

## <a name="define-hello-workflow"></a>Definire hello flusso di lavoro

Le definizioni dei flussi di lavoro di Oozie sono scritte in linguaggio hPDL (XML Process Definition Language). Utilizzare hello flusso di lavoro hello toodefine i passaggi seguenti:

1. Dopo l'istruzione toocreate hello e modificare un nuovo file:

    ```
    nano workflow.xml
    ```

2. Una volta che viene aperto l'editor nano hello, immettere hello seguente XML come contenuto del file hello:

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start too= "RunHiveScript"/>
        <action name="RunHiveScript">
        <hive xmlns="uri:oozie:hive-action:0.2">
            <job-tracker>${jobTracker}</job-tracker>
            <name-node>${nameNode}</name-node>
            <configuration>
            <property>
                <name>mapred.job.queue.name</name>
                <value>${queueName}</value>
            </property>
            </configuration>
            <script>${hiveScript}</script>
            <param>hiveTableName=${hiveTableName}</param>
            <param>hiveDataFolder=${hiveDataFolder}</param>
        </hive>
        <ok to="RunSqoopExport"/>
        <error to="fail"/>
        </action>
        <action name="RunSqoopExport">
        <sqoop xmlns="uri:oozie:sqoop-action:0.2">
            <job-tracker>${jobTracker}</job-tracker>
            <name-node>${nameNode}</name-node>
            <configuration>
            <property>
                <name>mapred.compress.map.output</name>
                <value>true</value>
            </property>
            </configuration>
            <arg>export</arg>
            <arg>--connect</arg>
            <arg>${sqlDatabaseConnectionString}</arg>
            <arg>--table</arg>
            <arg>${sqlDatabaseTableName}</arg>
            <arg>--export-dir</arg>
            <arg>${hiveDataFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\t"</arg>
            <archive>sqljdbc41.jar</archive>
            </sqoop>
        <ok to="end"/>
        <error to="fail"/>
        </action>
        <kill name="fail">
        <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
        </kill>
        <end name="end"/>
    </workflow-app>
    ```

    Esistono due azioni definite nel flusso di lavoro hello:

   * **RunHiveScript**: questa azione è l'azione di avvio hello ed esegue hello **useooziewf.hql** lo script Hive

   * **RunSqoopExport**: questa azione Esporta dati hello creati da hello Hive script tooSQL utilizzando Sqoop del Database. Questa azione viene eseguita solo se hello **RunHiveScript** azione ha esito positivo.

     flusso di lavoro Hello ha diverse voci, ad esempio `${jobTracker}`. Queste voci vengono sostituite da valori utilizzati nella definizione di processo hello. definizione di processo Hello viene creata più avanti in questo documento.

     Anche i hello nota `<archive>sqljdbc4.jar</arcive>` voce nella sezione Sqoop hello. Questa voce indica Oozie toomake questo archivio disponibile per Sqoop quando si esegue questa azione.

3. Utilizzare Ctrl + X, quindi **Y** e **invio** file hello toosave.

4. Comando che segue di hello utilizzare hello toocopy **workflow** file troppo**/tutorials/useoozie/workflow.xml**:

    ```
    hdfs dfs -put workflow.xml /tutorials/useoozie/workflow.xml
    ```

## <a name="create-hello-database"></a>Creare database hello

toocreate un Database SQL di Azure, seguire i passaggi hello hello [creare un Database SQL](../sql-database/sql-database-get-started.md) documento. Quando si crea il database di hello, utilizzare `oozietest` come nome del database hello. Inoltre, prendere nota del nome hello hello del server di database.

### <a name="create-hello-table"></a>Creare la tabella hello

> [!NOTE]
> Esistono molti modi tooconnect tooSQL Database toocreate una tabella. Hello seguenti utilizzano [disporre di FreeTDS](http://www.freetds.org/) dal cluster HDInsight hello.


1. Utilizzare hello successivo comando tooinstall disporre di FreeTDS nel cluster HDInsight hello:

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

2. Una volta installato, disporre di FreeTDS seguente hello utilizzare comandi tooconnect toohello server di Database SQL creato in precedenza:

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <sqlLogin> -P <sqlPassword> -p 1433 -D oozietest
    ```

    Viene visualizzato toohello simili di output il testo seguente:

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toooozietest
        1>

3. In hello `1>` richiesto, immettere hello seguenti righe:

    ```
    CREATE TABLE [dbo].[mobiledata](
    [deviceplatform] [nvarchar](50),
    [count] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(deviceplatform)
    GO
    ```

    Quando hello `GO` istruzione viene immessa, le istruzioni precedenti hello vengono valutate. Le istruzioni seguenti creano una tabella denominata **mobiledata** utilizzato dal flusso di lavoro hello.

    Hello utilizzare tooverify che hello nella tabella seguente è stata creata:

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    Vedrai toohello simili di output il testo seguente:

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    oozietest       dbo     mobiledata      BASE TABLE
    ```

4. Immettere `exit` in hello `1>` richiedere utilità di tooexit hello tsql.

## <a name="create-hello-job-definition"></a>Crea definizione processo hello

definizione del processo Hello descrive dove toofind hello workflow. Viene inoltre descritto dove toofind altri file utilizzati dal flusso di lavoro di hello (ad esempio useooziewf.hql). Definisce inoltre i valori hello per le proprietà utilizzate all'interno del flusso di lavoro hello e i file associati.

1. Utilizzare hello seguente comando tooget hello indirizzo completo di spazio di archiviazione predefinito hello. Questo indirizzo viene utilizzato nel file di configurazione hello in proposito:

    ```
    sed -n '/<name>fs.default/,/<\/value>/p' /etc/hadoop/conf/core-site.xml
    ```

    Questo comando restituisce toohello simile di informazioni XML seguente:

    ```xml
    <name>fs.defaultFS</name>
    <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
    ```

    > [!NOTE]
    > Se il cluster di HDInsight hello utilizza l'archiviazione di Azure come spazio di archiviazione predefinito hello, hello `<value>` il contenuto degli elementi inizia con `wasb://`. Se, invece, viene usato Azure Data Lake Store, il contenuto inizia con `adl://`.

    Salvare il contenuto di hello di hello `<value>` elemento, perché viene utilizzato nei passaggi successivi hello.

2. Utilizzare hello successivo comando tooget FQDN del nodo head del cluster di hello. Queste informazioni vengono utilizzate per hello JobTracker indirizzo hello cluster:

    ```
    hostname -f
    ```

    Restituisce toohello di informazioni simili seguente testo:

    ```hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net```

    Hello porta usata per hello JobTracker è 8050, pertanto è hello indirizzo completo toouse per hello JobTracker `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.

3. Utilizzare hello toocreate hello Oozie processo di configurazione della definizione seguente:

    ```
    nano job.xml
    ```

4. Una volta verrà aperto l'editor nano hello usare hello seguente XML come contenuto di hello del file hello:

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
        <name>nameNode</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
        </property>

        <property>
        <name>jobTracker</name>
        <value>JOBTRACKERADDRESS</value>
        </property>

        <property>
        <name>queueName</name>
        <value>default</value>
        </property>

        <property>
        <name>oozie.use.system.libpath</name>
        <value>true</value>
        </property>

        <property>
        <name>hiveScript</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/useooziewf.hql</value>
        </property>

        <property>
        <name>hiveTableName</name>
        <value>mobilecount</value>
        </property>

        <property>
        <name>hiveDataFolder</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/data</value>
        </property>

        <property>
        <name>sqlDatabaseConnectionString</name>
        <value>"jdbc:sqlserver://serverName.database.windows.net;user=adminLogin;password=adminPassword;database=oozietest"</value>
        </property>

        <property>
        <name>sqlDatabaseTableName</name>
        <value>mobiledata</value>
        </property>

        <property>
        <name>user.name</name>
        <value>YourName</value>
        </property>

        <property>
        <name>oozie.wf.application.path</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
    </configuration>
    ```

   * Sostituire tutte le istanze di  **wasb://mycontainer@mystorageaccount.blob.core.windows.net**  con valore hello ricevuto in precedenza per l'archiviazione predefinita.

     > [!WARNING]
     > Se il percorso di hello è un `wasb` percorso, è necessario utilizzare il percorso completo di hello. Non usare la versione abbreviata toojust `wasb:///`.

   * Sostituire **JOBTRACKERADDRESS** con hello JobTracker/ResourceManager indirizzo è stato ricevuto in precedenza.
   * Sostituire **YourName** con il nome di accesso per il cluster HDInsight hello.
   * Sostituire **serverName**, **adminLogin**, e **adminPassword** con informazioni hello per Database SQL di Azure.

     La maggior parte delle informazioni presenti nel file hello è valori hello utilizzati toopopulate utilizzati nei file di workflow o ooziewf.hql hello (ad esempio ${nameNode}.)

     > [!NOTE]
     > Hello **oozie.wf.application.path** voce definisce dove i file di workflow hello di toofind, che contiene hello flusso di lavoro è stato eseguito da questo processo.

5. Utilizzare Ctrl + X, quindi **Y** e **invio** file hello toosave.

## <a name="submit-and-manage-hello-job"></a>Inviare e gestire il processo di hello

Hello passaggi seguenti utilizzano hello Oozie comando toosubmit e gestire i flussi di lavoro Oozie nel cluster hello. comando Oozie Hello è un'interfaccia intuitiva su hello [API REST di Oozie](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).

> [!IMPORTANT]
> Quando si utilizza il comando di Oozie hello, è necessario utilizzare hello FQDN per nodo head HDInsight hello. Questo nome di dominio completo è accessibile solo da cluster hello o se hello cluster si trova in una rete virtuale di Azure, da altre macchine su hello stessa rete.


1. Utilizzare hello tooobtain hello URL toohello Oozie servizio:

    ```
    sed -n '/<name>oozie.base.url/,/<\/value>/p' /etc/oozie/conf/oozie-site.xml
    ```

    Restituisce toohello simile di informazioni XML seguente:

    ```xml
    <name>oozie.base.url</name>
    <value>http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie</value>
    ```

    Hello `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` parte è hello URL toouse con hello comando Oozie.

2. Hello utilizzare seguente toocreate una variabile di ambiente per hello URL, non vi è tootype per ogni comando:

    ```
    export OOZIE_URL=http://HOSTNAMEt:11000/oozie
    ```

    Sostituire l'URL di hello con hello uno che è stato ricevuto in precedenza.
3. Utilizzare hello processo hello toosubmit seguenti:

    ```
    oozie job -config job.xml -submit
    ```

    Il comando Carica le informazioni sul processo di hello da **job.xml** e lo invia tooOozie, ma non viene eseguito il.

    Al termine del comando hello, dovrebbe restituire hello ID di processo hello. ad esempio `0000005-150622124850154-oozie-oozi-W`. Questo ID è il processo di hello toomanage utilizzato.

4. Visualizzare lo stato di hello del processo di hello utilizzando hello comando seguente:

    ```
    oozie job -info <JOBID>
    ```

    > [!NOTE]
    > Sostituire `<JOBID>` con hello ID restituito nel passaggio precedente hello.

    Restituisce toohello di informazioni simili seguente testo:

    ```
    Job ID : 0000005-150622124850154-oozie-oozi-W
    ------------------------------------------------------------------------------------------------------------------------------------
    Workflow Name : useooziewf
    App Path      : wasb:///tutorials/useoozie
    Status        : PREP
    Run           : 0
    User          : USERNAME
    Group         : -
    Created       : 2015-06-22 15:06 GMT
    Started       : -
    Last Modified : 2015-06-22 15:06 GMT
    Ended         : -
    CoordAction ID: -
    ------------------------------------------------------------------------------------------------------------------------------------
    ```

    Lo stato del processo è `PREP`. Questo stato indica che il processo di hello è stato creato, ma non è stato avviato.

5. Utilizzare hello processo hello toostart di comando seguente:

    ```
    oozie job -start JOBID
    ```

    > [!NOTE]
    > Sostituire `<JOBID>` con hello ID restituito in precedenza.

    Se si archivia lo stato di hello dopo questo comando, si trova in uno stato di esecuzione e vengono restituite informazioni per le azioni all'interno del processo di hello hello.

6. Dopo l'attività hello viene completato correttamente, è possibile verificare che i dati di hello è stati generati ed esportavano toohello tabella del Database SQL utilizzando i seguenti comandi hello:

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D oozietest
    ```

    In hello `1>` richiesto, immettere hello seguente query:

    ```
    SELECT * FROM mobiledata
    GO
    ```

    informazioni di Hello restituite sono simile toohello seguente testo:

        deviceplatform  count
        Android 31591
        iPhone OS       22731
        proprietary development 3
        RIM OS  3464
        Unknown 213
        Windows Phone   1791
        (6 rows affected)

Per ulteriori informazioni sul comando Oozie hello, vedere [strumento da riga di comando Oozie](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).

## <a name="oozie-rest-api"></a>API REST di Oozie

API REST Oozie Hello consente toobuild i propri strumenti che funzionano con Oozie. di seguito Hello sono HDInsight informazioni specifiche sull'utilizzo di API REST Oozie hello:

* **URI**: hello API REST sia accessibile dal cluster hello esterno`https://CLUSTERNAME.azurehdinsight.net/oozie`

* **Autenticazione**: l'API toohello utilizzando account cluster HTTP hello (amministratore) e la password di autenticazione. ad esempio:

    ```
    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/oozie/versions
    ```

Per ulteriori informazioni sull'utilizzo delle API REST Oozie hello, vedere [API per servizi Web Oozie](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).

## <a name="oozie-web-ui"></a>Interfaccia utente Web di Oozie

Hello dell'interfaccia utente Web Oozie fornisce una visualizzazione basata sul web in stato di hello dei processi di Oozie nel cluster hello. interfaccia utente web Hello consente hello tooview le seguenti informazioni:

* Stato processo
* Definizione del processo
* Configurazione
* Un grafico di azioni di hello nel processo di hello
* Log per il processo di hello

È anche possibile visualizzare i dettagli delle azioni all'interno di un processo.

tooaccess hello dell'interfaccia utente Web Oozie, usare hello alla procedura seguente:

1. Creare un cluster di HDInsight toohello tunnel SSH. Per informazioni, vedere hello [usare SSH Tunneling con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) documento.

2. Dopo aver creato un tunnel, aprire hello Ambari web dell'interfaccia utente nel web browser. Hello URI per il sito Ambari hello è **https://CLUSTERNAME.azurehdinsight.net**. Sostituire **CLUSTERNAME** con nome hello del cluster HDInsight basati su Linux.

3. Hello lato della pagina hello sinistro, selezionare **Oozie**, quindi **collegamenti rapidi**e infine **dell'interfaccia utente Web Oozie**.

    ![immagine del menu hello](./media/hdinsight-use-oozie-linux-mac/ooziewebuisteps.png)

4. Hello toodisplaying impostazioni predefinite dell'interfaccia utente Web Oozie processi del flusso di lavoro in esecuzione. Selezionare tutti i processi del flusso di lavoro, toosee **tutti i processi**.

    ![Tutti i processi visualizzati](./media/hdinsight-use-oozie-linux-mac/ooziejobs.png)

5. Selezionare un processo tooview ulteriori informazioni sul processo hello.

    ![Job Info](./media/hdinsight-use-oozie-linux-mac/jobinfo.png)

6. Dalla scheda informazioni hello, è possibile visualizzare informazioni sul processo di base e le azioni di singoli hello all'interno del processo di hello. Utilizzo hello delle schede nella parte superiore di hello che è possibile visualizzare hello definizione del processo, la configurazione del processo, hello accesso Log Job o visualizzare indirizzate aciclico Graph (DAG) del processo di hello.

   * **Processo di Log**: hello seleziona **GetLogs** pulsante tooget tutti i log per il processo di hello o utilizzare hello **filtro di ricerca immettere** campo toofilter log

       ![Log del processo](./media/hdinsight-use-oozie-linux-mac/joblog.png)

   * **JobDAG**: hello DAG è una rappresentazione grafica dei percorsi di dati hello eseguite tramite flusso di lavoro hello

       ![DAG del processo](./media/hdinsight-use-oozie-linux-mac/jobdag.png)

7. Selezionando una delle azioni hello hello **informazioni** scheda consente di visualizzare informazioni per l'azione di hello. Ad esempio, selezionare hello **RunHiveScript** azione.

    ![Informazioni sull'azione](./media/hdinsight-use-oozie-linux-mac/action.png)

8. È possibile visualizzare i dettagli per l'azione di hello, ad esempio un collegamento di toohello **URL della Console**. Questo collegamento può essere utilizzato tooview JobTracker informazioni per il processo di hello.

## <a name="scheduling-jobs"></a>Pianificazione di processi

coordinatore Hello consente toospecify una frequenza di occorrenza inizio e fine per i processi. toodefine una pianificazione per flusso di lavoro hello, utilizzare hello alla procedura seguente:

1. Hello utilizzare seguente toocreate un file denominato **coordinator.xml**:

    ```
    nano coordinator.xml
    ```

    Utilizzare hello seguente XML come contenuto di hello del file hello:

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
        <workflow>
            <app-path>${workflowPath}</app-path>
        </workflow>
        </action>
    </coordinator-app>
    ```

    > [!NOTE]
    > Hello `${...}` variabili vengono sostituite dai valori nella definizione di processo hello in fase di esecuzione. le variabili di Hello sono:
    >
    > * `${coordFrequency}`: Il tempo tra l'esecuzione di istanze del processo di hello.
    > ** `${coordStart}`: ora di inizio processo hello.
    > * `${coordEnd}`: ora di fine processo hello.
    > * `${coordTimezone}`: i processi del coordinatore si trovano in un fuso orario predefinito che non tiene conto dell'ora legale (in genere rappresentato dall'acronimo UTC). Il fuso orario viene definito come hello "Oozie elaborazione fuso orario."
    > * `${wfPath}`: hello percorso toohello workflow.

2. hello toosave, utilizzare Ctrl + X, **Y**, e **invio**.

3. Utilizzare hello comando toocopy hello toohello working directory del file per il processo seguente:

    ```
    hadoop fs -put coordinator.xml /tutorials/useoozie/coordinator.xml
    ```

4. Hello utilizzare seguente hello toomodify **job.xml** file:

    ```
    nano job.xml
    ```

    Apportare hello seguenti modifiche:

   * il file tooinstruct oozie toorun hello coordinator anziché hello flusso di lavoro modifica `<name>oozie.wf.application.path</name>` troppo`<name>oozie.coord.application.path</name>`.

   * hello tooset `workflowPath` variabile utilizzata dal coordinatore hello, aggiungere hello XML seguente:

        ```xml
        <property>
            <name>workflowPath</name>
            <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
        ```

       Sostituire hello `wasb://mycontainer@mystorageaccount.blob.core.windows` testo con il valore di hello utilizzato in altre voci nel file job.xml hello.

   * inizio hello toodefine, fine e la frequenza per coordinator hello, aggiungere hello XML seguente:

        ```xml
        <property>
            <name>coordStart</name>
            <value>2017-05-10T12:00Z</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>2017-05-12T12:00Z</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>1440</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>UTC</value>
        </property>
        ```

       Questi valori impostati too12 ora di inizio hello: 00 PM del 10 maggio 2017, hello tooMay ora fine 12, 2017. intervallo di Hello per l'esecuzione del processo ogni giorno. frequenza di Hello è espresso in minuti, quindi 24 ore x 60 minuti = 1440 minuti. Infine, fuso orario di hello è impostato tooUTC.

5. Utilizzare Ctrl + X, quindi **Y** e **invio** file hello toosave.

6. processo di hello toorun, utilizzare hello comando seguente:

    ```
    oozie job -config job.xml -run
    ```

    Questo comando Invia e avvia il processo di hello.

7. Se si visita dell'interfaccia utente Web Oozie hello e selezionare hello **processi coordinatore** scheda, viene visualizzato toohello di informazioni simili seguente immagine:

    ![scheda coordinator jobs](./media/hdinsight-use-oozie-linux-mac/coordinatorjob.png)

    Hello **materializzazione Avanti** voce contiene hello successivo hello esecuzione del processo.

8. Toohello simile precedente processo di flusso di lavoro, selezionando la voce di processi hello nell'interfaccia utente web hello Visualizza le informazioni sul processo hello:

    ![Informazioni sui processi coordinatore](./media/hdinsight-use-oozie-linux-mac/coordinatorjobinfo.png)

    > [!NOTE]
    > Questa immagine Mostra solo l'esecuzione ha esito positivo del processo di hello, non singole azioni all'interno del flusso di lavoro hello pianificata. toosee che, selezionare una delle hello **azione** voci.

    ![Informazioni sull'azione](./media/hdinsight-use-oozie-linux-mac/coordinatoractionjob.png)

## <a name="troubleshooting"></a>Risoluzione dei problemi

Hello Oozie UI consente tooview Oozie log. Contiene inoltre i registri tooJobTracker collegamenti per l'attività MapReduce avviate dal flusso di lavoro hello. deve essere modello Hello per la risoluzione dei problemi:

1. Visualizza processo hello nell'interfaccia utente Web Oozie.

2. Se è presente un errore per un'azione specifica, selezionare hello toosee azione se hello **messaggio di errore** campo fornisce altre informazioni sull'errore hello.

3. Se disponibile, utilizzare URL hello da hello azione tooview ulteriori dettagli (ad esempio, i log JobTracker) per l'azione di hello.

di seguito Hello sono specifici errori che possono verificarsi, e come tooresolve li.

### <a name="ja009-cannot-initialize-cluster"></a>JA009: Cannot initialize cluster

**Sintomi**: hello modifiche dello stato di processo troppo**SUSPENDED**. Dettagli per il processo di hello mostrano lo stato di RunHiveScript hello come **START_MANUAL**. Selezionando l'azione di hello Visualizza hello seguente messaggio di errore:

    JA009: Cannot initialize Cluster. Please check your configuration for map

**Causa**: hello indirizzi WASB utilizzati in hello **job.xml** file non contengono il contenitore di archiviazione hello o nome account di archiviazione. formato dell'indirizzo WASB Hello deve essere `wasb://containername@storageaccountname.blob.core.windows.net`.

**Risoluzione**: modificare gli indirizzi WASB hello utilizzati dal processo hello.

### <a name="ja002-oozie-is-not-allowed-tooimpersonate-ltuser"></a>JA002: Oozie non è consentito tooimpersonate &lt;utente >

**Sintomi**: hello modifiche dello stato di processo troppo**SUSPENDED**. Dettagli per il processo di hello mostrano lo stato di RunHiveScript hello come **START_MANUAL**. Selezionare l'azione hello visualizzare hello seguente messaggio di errore:

    JA002: User: oozie is not allowed tooimpersonate <USER>

**Causa**: impostazioni di autorizzazione correnti non consentono Oozie hello tooimpersonate l'account utente specificato.

**Risoluzione**: Oozie è consentito agli utenti di tooimpersonate in hello **utenti** gruppo. Hello utilizzare `groups USERNAME` gruppi hello toosee hello account utente è membro. Se l'utente hello non è un membro di hello **utenti** gruppo, utilizzare hello gruppo toohello utente hello tooadd dei comandi seguenti:

    sudo adduser USERNAME users

> [!NOTE]
> Potrebbe richiedere alcuni minuti prima di HDInsight riconosce che l'utente hello è stato aggiunto a un gruppo toohello.

### <a name="launcher-error-sqoop"></a>ERRORE dell'utilità di avvio (Sqoop)

**Sintomi**: hello modifiche dello stato di processo troppo**KILLED**. Dettagli per il processo di hello mostrano lo stato di RunSqoopExport hello come **errore**. Selezionare l'azione hello visualizzare hello seguente messaggio di errore:

    Launcher ERROR, reason: Main class [org.apache.oozie.action.hadoop.SqoopMain], exit code [1]

**Causa**: Sqoop è Impossibile tooload hello driver necessari tooaccess hello di database.

**Risoluzione**: quando si utilizza Sqoop da un processo Oozie, è necessario includere i driver di database hello con hello altre risorse (ad esempio workflow hello) utilizzate dal processo hello. Fare riferimento anche archivio hello contenente i driver di database hello da hello `<sqoop>...</sqoop>` sezione workflow hello.

Ad esempio, per il processo di hello in questo documento, utilizzare hello alla procedura seguente:

1. Copia hello sqljdbc4.1.jar toohello /tutorials/useoozie directory del file:

    ```
    hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc41.jar /tutorials/useoozie/sqljdbc41.jar
    ```

2. Modificare hello tooadd di workflow hello seguente XML in una nuova riga sopra `</sqoop>`:

    ```xml
    <archive>sqljdbc41.jar</archive>
    ```

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione, si è appreso come un flusso di lavoro Oozie toodefine e come toorun un processo di Oozie. toolearn più informazioni sull'utilizzo di HDInsight, vedere hello seguenti articoli:

* [Usare il coordinatore Oozie basato sul tempo con HDInsight][hdinsight-oozie-coordinator-time]
* [Caricare dati per processi Hadoop in HDInsight][hdinsight-upload-data]
* [Usare Sqoop con Hadoop in HDInsight][hdinsight-use-sqoop]
* [Usare Hive con Hadoop in HDInsight][hdinsight-use-hive]
* [Usare Pig con Hadoop in HDInsight][hdinsight-use-pig]
* [Sviluppare programmi MapReduce Java per HDInsight][hdinsight-develop-mapreduce]

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563
[azure-data-factory-pig-hive]: ../data-factory/data-factory-data-transformation-activities.md
[hdinsight-oozie-coordinator-time]: hdinsight-use-oozie-coordinator-time.md
[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started]: hdinsight-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop-mac-linux.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started-emulator]: hdinsight-get-started-emulator.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[sqldatabase-create-configue]: sql-database-create-configure.md
[sqldatabase-get-started]: sql-database-get-started.md

[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: https://technet.microsoft.com/en-us/library/ee176961.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.RunWF.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
