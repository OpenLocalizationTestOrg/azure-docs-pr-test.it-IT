---
title: aaaQuery Hive tramite driver JDBC hello - HDInsight di Azure | Documenti Microsoft
description: Utilizzare il driver JDBC hello da una query tooHadoop di Java applicazione toosubmit Hive in HDInsight. Connettersi a livello di codice e dal client di SQL esce hello.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 928f8d2a-684d-48cb-894c-11c59a5599ae
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 93178da3b8d497faa4c788e91dba89c4e45d3fff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="query-hive-through-hello-jdbc-driver-in-hdinsight"></a>Eseguire una query Hive tramite il driver JDBC hello in HDInsight

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

Informazioni su come driver JDBC di hello toouse da un toosubmit applicazione Java Hive query tooHadoop in Azure HDInsight. informazioni di Hello in questo documento viene illustrato come tooconnect a livello di codice e da hello esce SQL client.

Per ulteriori informazioni su hello Hive interfaccia JDBC, vedere [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).

## <a name="prerequisites"></a>Prerequisiti

* Un cluster Hadoop in HDInsight. Sono adatti i cluster basati su Linux o su Windows.

  > [!IMPORTANT]
  > Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere [Ritiro di HDInsight 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* [SQuirreL SQL](http://squirrel-sql.sourceforge.net/). SQuirreL è un'applicazione client JDBC.

* Hello [Java Developer Kit (JDK) versione 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) o versione successiva.

* [Apache Maven](https://maven.apache.org). Maven è un progetto di compilare il sistema per i progetti di linguaggio che viene utilizzato dal progetto hello associata a questo articolo.

## <a name="jdbc-connection-string"></a>Stringa di connessione JDBC

Cluster di HDInsight tooan connessioni JDBC in Azure vengono eseguite su 443, e il traffico di hello viene protetto mediante SSL. gateway pubblica Hello cluster hello protette da reindirizza la porta toohello di traffico hello HiveServer2 è effettivamente in ascolto. di seguito Hello è una stringa di connessione di esempio:

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

Sostituire `CLUSTERNAME` con nome hello del cluster HDInsight.

## <a name="authentication"></a>Autenticazione

Quando si stabilisce la connessione hello, è necessario utilizzare hello HDInsight cluster admin nome e la password tooauthenticate toohello cluster gateway. Durante la connessione dal client JDBC, ad esempio esce SQL, è necessario immettere il nome di amministratore hello e una password nelle impostazioni client.

Da un'applicazione Java, è necessario utilizzare nome hello e una password per stabilire una connessione. Ad esempio, hello codice Java seguente apre una nuova connessione utilizzando la stringa di connessione hello Nome amministratore e la password:

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a>Connettersi con il client SQuirreL SQL

Esce SQL è un client JDBC che può essere utilizzati tooremotely eseguire Hive query con il cluster HDInsight. Hello passaggi seguenti presuppongono che è già stato installato SQL esce.

1. Copiare i driver JDBC Hive hello dal cluster HDInsight.

    * Per **HDInsight basati su Linux**, utilizzare hello seguenti passaggi viene file jar di toodownload hello necessario.

        1. Creare una directory che contiene file hello. ad esempio `mkdir hivedriver`.

        2. Dalla riga di comando, seguito hello utilizzare comandi file hello toocopy dal cluster HDInsight hello:

            ```bash
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-jdbc*standalone.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
            ```

            Sostituire `USERNAME` con nome dell'account utente SSH hello per cluster hello. Sostituire `CLUSTERNAME` con nome del cluster HDInsight hello.

    * Per **HDInsight basati su Windows**, i file jar di hello toodownload i passaggi seguenti di hello di utilizzo.

        1. Dal portale di Azure hello, selezionare il cluster HDInsight, quindi hello **Desktop remoto** icona.

            ![Icona Desktop remoto](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. Nel Pannello di hello Desktop remoto, utilizzare hello **Connetti** cluster toohello tooconnect di pulsante. Se non è abilitato hello Desktop remoto, usare hello modulo tooprovide un nome utente e password, quindi selezionare **abilitare** tooenable Desktop remoto per il cluster hello.

            ![Pannello Desktop remoto](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopblade.png)

            Dopo avere selezionato **Connetti** verrà scaricato un file con estensione rdp. Utilizzare il client Desktop remoto hello toolaunch questo file. Quando richiesto, utilizzare il nome di utente hello e la password che immessa per l'accesso Desktop remoto.

        3. Una volta connessi, copiare i seguenti file dal computer locale tooyour sessione Desktop remoto hello hello. Inserirli in una directory locale denominata `hivedriver`.

            * C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar
            * C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar
            * C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar

            > [!NOTE]
            > versione di Hello numeri inclusi in hello percorsi e nomi file potrebbero essere diversi per il cluster.

        4. Disconnettere la sessione di Desktop remoto hello dopo aver completato la copia dei file hello.

2. Avviare un'applicazione hello esce SQL. Da sinistra hello hello finestra, selezionare **driver**.

    ![Scheda driver hello a sinistra della finestra hello](./media/hdinsight-connect-hive-jdbc-driver/squirreldrivers.png)

3. Dalle icone hello nella parte superiore di hello di hello **driver** finestra di dialogo, seleziona hello  **+**  toocreate icona un driver.

    ![Icone Drivers](./media/hdinsight-connect-hive-jdbc-driver/driversicons.png)

4. Nella finestra di dialogo Aggiungi Driver hello aggiungere hello le seguenti informazioni:

    * **Name** (Nome): Hive
    * **Example URL** (URL di esempio): `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`
    * **Percorso di classe aggiuntivo**: file jar utilizzare hello Aggiungi pulsante tooadd hello scaricato in precedenza
    * **Class Name** (Nome classe): org.apache.hive.jdbc.HiveDriver

   ![finestra di dialogo add driver](./media/hdinsight-connect-hive-jdbc-driver/adddriver.png)

   Fare clic su **OK** toosave queste impostazioni.

5. A sinistra hello della finestra SQL esce hello, selezionare **alias**. Quindi fare clic su hello  **+**  toocreate icona un alias di connessione.

    ![aggiungere un nuovo alias](./media/hdinsight-connect-hive-jdbc-driver/aliases.png)

6. I valori seguenti di hello di utilizzo per hello **aggiungere Alias** finestra di dialogo.

    * **Name** (Nome): Hive on HDInsight

    * **Driver**: hello tooselect elenco a discesa di utilizzare hello **Hive** driver

    * **URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

        Sostituire **CLUSTERNAME** con nome hello del cluster HDInsight.

    * **Nome utente**: nome di account di accesso hello cluster per il cluster HDInsight. valore predefinito di Hello è `admin`.

    * **Password**: password hello per account di accesso cluster hello.

 ![finestra di dialogo add alias](./media/hdinsight-connect-hive-jdbc-driver/addalias.png)

    Hello utilizzare **Test** tooverify pulsante che hello connessione funzioni. Quando **connettersi: Hive in HDInsight** viene visualizzata la finestra, selezionare **Connetti** test hello tooperform. Se il test di hello ha esito positivo, viene visualizzato un **connessione riuscita** finestra di dialogo.

    connessione hello toosave utilizzare alias, hello **Ok** pulsante nella parte inferiore di hello di hello **aggiungere Alias** finestra di dialogo.

7. Da hello **connettersi** elenco a discesa in cima a hello esce SQL, selezionare **Hive in HDInsight**. Quando richiesto, selezionare **Connect** (Connetti).

    ![finestra di dialogo di connessione](./media/hdinsight-connect-hive-jdbc-driver/connect.png)

8. Una volta connessi, immettere hello eseguire una query nella finestra di dialogo query SQL hello seguenti e quindi selezionare hello **eseguire** icona. area risultati Hello deve visualizzare i risultati di hello di hello query.

        select * from hivesampletable limit 10;

    ![finestra della query sql, con i risultati](./media/hdinsight-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a>Connettersi da un'applicazione Java di esempio

Un esempio di utilizzo di un tooquery client Java Hive in HDInsight è disponibile all'indirizzo [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc). Seguire le istruzioni hello hello repository toobuild ed eseguire l'esempio hello.

## <a name="troubleshooting"></a>Risoluzione dei problemi

### <a name="unexpected-error-occurred-attempting-tooopen-an-sql-connection"></a>Errore imprevisto durante il tentativo di tooopen una connessione SQL

**Sintomi**: durante la connessione cluster HDInsight tooan versione 3.3 o 3.4, si potrebbe ricevere un errore che si è verificato un errore imprevisto. analisi dello stack dell'errore Hello inizia con hello seguenti righe:

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

**Causa**: questo errore è causato da una mancata corrispondenza nella versione di hello hello commons codec.jar del file di utilizzato esce e hello uno necessario per i componenti Hive JDBC hello.

**Risoluzione**: toofix questo errore, utilizzare hello seguendo i passaggi:

1. Scaricare il file jar commons codec hello dal cluster HDInsight.

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. Chiudere esce e quindi passare toohello directory in cui esce è installato nel sistema. Nella directory esce hello in hello `lib` directory, sostituire hello esistente commons-codec.jar con download di uno dal cluster HDInsight hello hello.

3. Riavviare SQuirreL. Errore di Hello non deve verificarsi quando ci si connette tooHive in HDInsight.

## <a name="next-steps"></a>Passaggi successivi

Ora che si è appreso come toouse JDBC toowork con Hive, utilizzare hello seguendo i collegamenti tooexplore toowork altri modi con Azure HDInsight.

* [Caricare dati tooHDInsight](hdinsight-upload-data.md)
* [Usare Hive con HDInsight](hdinsight-use-hive.md)
* [Usare Pig con HDInsight](hdinsight-use-pig.md)
* [Usare processi MapReduce con HDInsight](hdinsight-use-mapreduce.md)
