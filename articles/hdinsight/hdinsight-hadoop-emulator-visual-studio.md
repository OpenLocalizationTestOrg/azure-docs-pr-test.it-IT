---
title: strumenti di aaaData Lake per Visual Studio con Hortonworks Sandbox - HDInsight di Azure | Documenti Microsoft
description: "Informazioni su come toouse hello strumenti di Azure Data Lake per Visual Studio con sandbox Hortonworks hello in esecuzione in una macchina virtuale locale. Con questi strumenti, è possibile creare ed eseguire i processi Hive e Pig sandbox hello e visualizzare l'output processo e della cronologia."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e3434c45-95d1-4b96-ad4c-fb59870e2ff0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: 7a3406b28d87d953e9b5be387faa86268f47b935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-data-lake-tools-for-visual-studio-with-hello-hortonworks-sandbox"></a>Utilizzare gli strumenti di Azure Data Lake hello per Visual Studio con hello Hortonworks Sandbox

Azure Data Lake include strumenti per l'uso di cluster Hadoop generici. Questo documento vengono illustrate operazioni di hello necessari gli strumenti di Data Lake hello toouse con hello Hortonworks Sandbox in esecuzione in una macchina virtuale locale.

Utilizzo di hello Hortonworks Sandbox consente toowork con Hadoop in ambiente di sviluppo locale. Dopo aver sviluppato una soluzione e si desidera toodeploy è su larga scala, è quindi possibile spostare il cluster di HDInsight tooan.

## <a name="prerequisites"></a>Prerequisiti

* Hello Hortonworks Sandbox, in esecuzione in una macchina virtuale in un ambiente di sviluppo. Questo documento è stato scritto e testato con sandbox hello in esecuzione in Oracle VirtualBox. Per informazioni sull'impostazione della sandbox hello, vedere hello [introduzione sandbox Hortonworks hello.](hdinsight-hadoop-emulator-get-started.md) nel relativo documento.

* Visual Studio 2013, Visual Studio 2015 o Visual Studio 2017 (qualsiasi edizione).

* Hello [Azure SDK per .NET](https://azure.microsoft.com/downloads/) 2.7.1 o versione successiva.

* Hello [di strumenti di Azure Data Lake per Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).

## <a name="configure-passwords-for-hello-sandbox"></a>Configurare le password per il sandbox hello

Verificare che tale hello che hortonworks Sandbox è in esecuzione. Seguire i passaggi di hello in hello [iniziare a utilizzare hello Hortonworks Sandbox](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) documento. Questi passaggi configurare password hello per hello SSH `root` account e hello Ambari `admin` account. Le password vengono utilizzate quando ci si connette toohello sandbox da Visual Studio.

## <a name="connect-hello-tools-toohello-sandbox"></a>Connettersi sandbox di hello strumenti toohello

1. Aprire Visual Studio, selezionare **Visualizza** e quindi **Esplora server**.

2. Da **Esplora Server**, hello rapida **HDInsight** voce e quindi selezionare **connettersi tooHDInsight emulatore**.

    ![Schermata di Esplora Server con connessione tooHDInsight emulatore evidenziato](./media/hdinsight-hadoop-emulator-visual-studio/connect-emulator.png)

3. Da hello **connettersi tooHDInsight emulatore** finestra di dialogo immettere hello password configurata per Ambari.

    ![Schermata della finestra di dialogo, con casella di testo della password evidenziata](./media/hdinsight-hadoop-emulator-visual-studio/enter-ambari-password.png)

    Selezionare **Avanti** toocontinue.

4. Hello utilizzare **Password** password di hello tooenter campo configurati per hello `root` account. Lasciare hello altri campi al valore predefinito di hello.

    ![Schermata della finestra di dialogo, con casella di testo della password evidenziata](./media/hdinsight-hadoop-emulator-visual-studio/enter-root-password.png)

    Selezionare **Avanti** toocontinue.

5. Attesa per la convalida di hello servizi toofinish. In alcuni casi, la convalida potrebbe avere esito negativo e viene configurazione hello tooupdate. Se la convalida non riesce, selezionare **aggiornamento**e attendere la verifica per toofinish servizio hello e configurazione di hello.

    ![Schermata della finestra di dialogo, con il pulsante Aggiorna evidenziato](./media/hdinsight-hadoop-emulator-visual-studio/fail-and-update.png)

    > [!NOTE]
    > il processo di aggiornamento di Hello utilizza hello toomodify Ambari toowhat configurazione Hortonworks Sandbox previsto dagli strumenti di Data Lake hello per Visual Studio.

6. Al termine della convalida, selezionare **fine** toocomplete configurazione.
    ![Schermata della finestra di dialogo, con il pulsante Fine evidenziato](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)

     >[!NOTE]
     > A seconda della velocità di hello dell'ambiente di sviluppo e hello quantità di memoria allocata macchina virtuale toohello, può richiedere diversi minuti tooconfigure e convalidare i servizi di hello.

Dopo aver completato questi passaggi, è ora un **cluster locale di HDInsight** voce in Esplora Server, hello **HDInsight** sezione.

## <a name="write-a-hive-query"></a>Scrivere una query Hive

Hive fornisce un linguaggio di query simile a SQL (HiveQL) per la gestione dei dati strutturati. Utilizzare hello seguendo i passaggi toolearn come una query sul cluster locale hello toorun su richiesta.

1. In **Esplora Server**, fare clic sulla voce hello per cluster locale hello aggiunto in precedenza e quindi selezionare **scrivere una Query Hive**.

    ![Schermata di Esplora server, con Scrivi una query Hive evidenziato](./media/hdinsight-hadoop-emulator-visual-studio/write-hive-query.png)

    Verrà visualizzata una nuova finestra di query, Qui è possibile scrivere e inviare un cluster locale toohello di query.

2. Nella nuova finestra query di hello, immettere hello comando seguente:

        select count(*) from sample_08;

    la query toorun hello, seleziona **Invia** nella parte superiore di hello della finestra hello. Lasciare gli altri valori di hello (**Batch** e nome del server) in valori predefiniti di hello.

    ![Schermata della finestra di query, con il pulsante di invio hello evidenziato](./media/hdinsight-hadoop-emulator-visual-studio/submit-hive.png)

    È inoltre possibile utilizzare il menu di scelta rapida hello accanto troppo**Invia** tooselect **avanzate**. Le opzioni avanzate consentono di opzioni aggiuntive tooprovide quando si invia il processo di hello.

    ![Schermata della finestra di dialogo Invia Script](./media/hdinsight-hadoop-emulator-visual-studio/advanced-hive.png)

3. Dopo aver inviato query hello, viene visualizzato lo stato del processo hello. lo stato del processo Hello Visualizza informazioni sul processo hello viene elaborato da Hadoop. **Lo stato del processo** fornisce hello lo stato del processo di hello. lo stato di Hello viene aggiornato periodicamente oppure è possibile utilizzare hello aggiornare icona toorefresh hello lo stato manualmente.

    ![Schermata della finestra di dialogo Vista processi con Stato processo evidenziato](./media/hdinsight-hadoop-emulator-visual-studio/job-state.png)

    Dopo hello **lo stato del processo** cambia troppo**completato**, viene visualizzato un indirizzate aciclico Graph (DAG). Questo diagramma illustra percorso di esecuzione hello che è stato determinato dal Tez durante l'elaborazione di query Hive hello. Tez è di tipo motore di esecuzione predefinito hello per Hive nel cluster locale hello.

    > [!NOTE]
    > Tez è predefinito hello quando si utilizza il cluster HDInsight basati su Linux. Non è predefinita hello in HDInsight basati su Windows. toouse è disponibile, è necessario aggiungere la riga hello `set hive.execution.engine = tez;` toohello inizio della query Hive.

    Hello utilizzare **Output processo** collegamento di output di hello tooview. In questo caso, è 823, numero hello di righe nella tabella sample_08 hello. È possibile visualizzare informazioni diagnostiche sul processo hello utilizzando hello **Log processo** e **Scarica Log di YARN** collegamenti.

4. È anche possibile eseguire in modo interattivo i processi Hive modificando hello **Batch** campo troppo**Interactive**. quindi selezionando **Esegui**.

    ![Schermata dei pulsanti Interattivo ed Esecuzione evidenziati](./media/hdinsight-hadoop-emulator-visual-studio/interactive-query.png)

    Una query interattiva flussi hello log di output generato durante l'elaborazione toohello **HiveServer2 Output** finestra.

    > [!NOTE]
    > Hello informazioni è hello uguale a quello disponibile dalla hello **Log processo** termine un processo di collegamento.

    ![Schermata del log di output](./media/hdinsight-hadoop-emulator-visual-studio/hiveserver2-output.png)

## <a name="create-a-hive-project"></a>Creare un progetto Hive

Inoltre, è possibile creare un progetto che contiene più script Hive. Utilizzare un progetto quando si dispone di script correlati o gli script toostore in un sistema di controllo della versione.

1. In Visual Studio selezionare **File**, **Nuovo** e quindi **Progetto**.

2. Elenco di progetti hello espandere **modelli**, espandere **Azure Data Lake**, quindi selezionare **HIVE (HDInsight)**. Selezionare nell'elenco dei modelli di hello **esempio Hive**. Immettere un nome e un percorso e quindi selezionare **OK**.

    ![Screenshot della finestra Nuovo progetto, con Azure Data Lake, HIVE, Hive Sample e OK evidenziati](./media/hdinsight-hadoop-emulator-visual-studio/new-hive-project.png)

Hello **esempio Hive** progetto contiene due script, **WebLogAnalysis.hql** e **SensorDataAnalysis.hql**. È possibile inviare questi script utilizzando hello stesso **Invia** pulsante nella parte superiore di hello della finestra hello.

## <a name="create-a-pig-project"></a>Creare un progetto Pig

Mentre Hive offre un linguaggio simile a SQL per la gestione dei dati strutturati, Pig esegue trasformazioni sui dati. Pig fornisce un linguaggio (alfabeto latino Pig) che consente di toodevelop una pipeline di trasformazioni. toouse Pig con cluster locale hello, seguire questi passaggi:

1. Aprire Visual Studio e selezionare **File** **Nuovo** e quindi **Progetto**. Elenco di progetti hello espandere **modelli**, espandere **Azure Data Lake**, quindi selezionare **Pig (HDInsight)**. Selezionare nell'elenco dei modelli di hello **Pig applicazione**. Immettere un nome e un percorso e quindi selezionare **OK**.

    ![Screenshot della finestra Nuovo progetto, con Azure Data Lake, Pig, Pig Application e OK evidenziati](./media/hdinsight-hadoop-emulator-visual-studio/new-pig.png)

2. Immettere di seguito il testo come contenuto di hello di hello hello **script.pig** file che è stato creato con questo progetto.

        a = LOAD '/demo/data/Website/Website-Logs' AS (
            log_id:int,
            ip_address:chararray,
            date:chararray,
            time:chararray,
            landing_page:chararray,
            source:chararray);
        b = FILTER a BY (log_id > 100);
        c = GROUP b BY ip_address;
        DUMP c;

    Sebbene di Hive, Pig utilizza una lingua diversa, le modalità di esecuzione di processi di hello è coerente tra entrambi i linguaggi, tramite hello **Invia** pulsante. Hello Seleziona elenco a discesa accanto a **Invia** consente di visualizzare la finestra di dialogo di invio avanzate per Pig.

    ![Schermata della finestra di dialogo Invia Script](./media/hdinsight-hadoop-emulator-visual-studio/advanced-pig.png)

3. Hello lo stato del processo e viene anche visualizzato l'output di hello stesso come una query Hive.

    ![Screenshot di un processo Pig completato](./media/hdinsight-hadoop-emulator-visual-studio/completed-pig.png)

## <a name="view-jobs"></a>Visualizzare i processi

Data Lake consentono inoltre tooeasily Visualizza informazioni sui processi che sono state eseguite in Hadoop. Utilizzare hello seguendo i processi di hello toosee passaggi che sono stati eseguiti nel cluster locale hello.

1. Da **Esplora Server**, cluster locale hello e quindi scegliere **Visualizza processi**. Viene visualizzato un elenco di processi che sono stati inviati toohello cluster.

    ![Schermata di Esplora Server, con Visualizza processi evidenziato](./media/hdinsight-hadoop-emulator-visual-studio/view-jobs.png)

2. Elenco di hello dei processi, selezionare una tooview i dettagli dei processi hello.

    ![Schermata di processo Browser, con uno dei processi di hello evidenziati](./media/hdinsight-hadoop-emulator-visual-studio/view-job-details.png)

    informazioni di Hello visualizzate sono simili toowhat che vengono visualizzati dopo l'esecuzione di una query Hive o Pig, inclusi i collegamenti tooview hello output e informazioni di registrazione.

3. È inoltre possibile modificare e quindi inviare nuovamente il processo di hello da qui.

## <a name="view-hive-databases"></a>Visualizzare i database Hive

1. In **Esplora Server**, espandere hello **cluster locale di HDInsight** voce, quindi espandere **database Hive**. Hello **predefinito** e **xademo** i database nel cluster locale hello vengono visualizzati. Espansione di un database Mostra tabelle hello hello database.

    ![Schermata di Esplora server, con i database espansi](./media/hdinsight-hadoop-emulator-visual-studio/expanded-databases.png)

2. Espandendo una tabella consente di visualizzare le colonne di hello per la tabella. tooquickly visualizzare i dati hello, una tabella e scegliere **Visualizza le prime 100 righe**.

    ![Schermata di Esplora server con tabella espansa e opzione Visualizza prime 100 righe selezionata](./media/hdinsight-hadoop-emulator-visual-studio/view-100.png)

### <a name="database-and-table-properties"></a>Proprietà del database e della tabella

È possibile visualizzare le proprietà di hello del database o tabella. Selezione **proprietà** consente di visualizzare i dettagli per l'elemento hello selezionato nella finestra Proprietà hello. Ad esempio, vedere informazioni hello mostrate nella seguente schermata hello:

![Schermata della finestra Proprietà](./media/hdinsight-hadoop-emulator-visual-studio/properties.png)

### <a name="create-a-table"></a>Creare una tabella

toocreate una tabella, fare doppio clic su un database e quindi selezionare **Create Table**.

![Schermata di Esplora Server, con Crea tabella evidenziato](./media/hdinsight-hadoop-emulator-visual-studio/create-table.png)

È quindi possibile creare una tabella di hello tramite un modulo. Nella parte inferiore di hello di hello seguente schermata, è possibile visualizzare hello HiveQL non elaborate che è usato toocreate hello tabella.

![Schermata di form hello utilizzato toocreate una tabella](./media/hdinsight-hadoop-emulator-visual-studio/create-table-form.png)

## <a name="next-steps"></a>Passaggi successivi

* [Cavi hello di apprendimento di hello Hortonworks Sandbox](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [Esercitazione di Hadoop: introduzione a HDP](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)
