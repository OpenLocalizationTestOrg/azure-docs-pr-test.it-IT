---
title: aaaConnect tooAzure HDInsight utilizzando Data Lake Tools per Visual Studio | Documenti Microsoft
description: Informazioni su come tooinstall e utilizzare Data Lake Tools per Visual Studio tooconnect tooHadoop cluster Azure HDInsight e l'esecuzione di query Hive.
keywords: strumenti Hadoop, query Hive, Visual Studio, Hadoop in Visual Studio
services: HDInsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: ce9c572a-1e98-46bf-9581-13a9767f1fa5
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: jgao
ms.openlocfilehash: ff5819a64bebe5f4ab3cf763ce6c45c81aa34b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-hdinsight-and-run-hive-queries-using-data-lake-tools-for-visual-studio"></a>Connettersi tooAzure HDInsight ed eseguire query Hive con Data Lake Tools per Visual Studio

Informazioni su come toouse Data Lake Tools per Visual Studio tooconnect tooHadoop cluster in [Azure HDInsight](hdinsight-hadoop-introduction.md) e inviare query Hive. Per ulteriori informazioni sull'uso di HDInsight, vedere [introduzione tooHDInsight](hdinsight-hadoop-introduction.md) e [iniziare a usare HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md). Per ulteriori informazioni sui cluster di Storm tooa connessione, vedere [c# sviluppare topologie per Apache Storm in HDInsight con Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

Data Lake Tools per Visual Studio può essere utilizzato tooaccess Data Lake Analitica sia HDInsight.  Per informazioni di hello su Data Lake Tools, vedere [esercitazione: sviluppare script U-SQL utilizzando Data Lake Tools per Visual Studio](../data-lake-analytics/data-lake-analytics-data-lake-tools-get-started.md).

**Prerequisiti**

toocomplete questo hello Data Lake di esercitazione e utilizzare gli strumenti in Visual Studio, è necessario disporre delle seguenti hello:

* Un cluster Azure HDInsight: toocreate uno, vedere [iniziare a usare HDInsight basati su Linux](hdinsight-hadoop-linux-tutorial-get-started.md)
* Una workstation con hello seguente software:
  
  * Windows 10, Windows 8.1, Windows 8 o Windows 7.
  * Visual Studio 2013/2015/2017.
    
    > [!NOTE]
    > Attualmente, hello Data Lake Tools per Visual Studio sono disponibili solo con la versione in lingua inglese di hello.
    > 
    > 

## <a name="install-data-lake-tools-for-visual-studio"></a>Installare Data Lake Tools per Visual Studio

Gli strumenti Data Lake Tools vengono installati per impostazione predefinita per Visual Studio 2017. Per le versioni precedenti, è possibile installarlo tramite hello [installazione guidata piattaforma Web](https://www.microsoft.com/web/downloads/). È necessario scegliere hello uno che corrisponde alla versione di Visual Studio. Se non è installato Visual Studio, è possibile installare hello Community di Visual Studio e Azure SDK più recenti utilizzando hello [installazione guidata piattaforma Web](https://www.microsoft.com/web/downloads/):

![Data Lake Tools per programma di installazione della piattaforma Web di Visual Studio. ] (./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.wpi.png "Tooinstall installazione guidata piattaforma Web di utilizzare Data Lake Tools per Visual Studio")

## <a name="connect-tooazure-subscriptions"></a>Connettersi tooAzure sottoscrizioni
Data Lake Tools per Visual Studio consente di cluster di HDInsight tooyour tooconnect, eseguire alcune operazioni di gestione di base ed eseguire query Hive.

> [!NOTE]
> Per informazioni sulla connessione i cluster Hadoop generico tooa, vedere [scrivere e inviare query Hive con Visual Studio](http://blogs.msdn.com/b/xiaoyong/archive/2015/05/04/how-to-write-and-submit-hive-queries-using-visual-studio.aspx).
> 
> 

**tooconnect tooyour sottoscrizione di Azure**

1. Aprire Visual Studio.
2. Da hello **vista** menu, fare clic su **Esplora Server** tooopen hello Esplora Server.
3. Espandere **Azure** e quindi **HDInsight**.
   
   > [!NOTE]
   > Hello preavviso **elenco attività HDInsight** finestra dovrebbe essere aperta. Se non è visualizzata, fare clic su **altre finestre** da hello **vista** menu e quindi fare clic su **finestra Elenco attività di HDInsight**.  
   > 
   > 
4. Immettere le credenziali della sottoscrizione di Azure e fare clic su **Accedi**. Questo è solo necessario se non si è mai connessi toohello sottoscrizione di Azure da Visual Studio nella workstation.
5. In Esplora server verrà visualizzato un elenco di cluster HDInsight esistenti. Se non si dispone di tutti i cluster, è possibile crearne uno utilizzando hello portale di Azure, Azure PowerShell o hello HDInsight SDK. Per altre informazioni, vedere [Creare cluster Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
   
   ![Elenco di cluster in Esplora server di Strumenti Data Lake per Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.server.explorer.png "Esplora server di Strumenti Data Lake per Visual Studio")
6. Espandere un cluster HDInsight. Verranno visualizzati i **database Hive**, un account di archiviazione predefinito, gli account di archiviazione collegati e il **log del servizio Hadoop**. È inoltre possibile espandere le entità hello.

Dopo aver collegato tooyour sottoscrizione di Azure, sarà seguito hello toodo in grado di:

**tooconnect toohello portale di Azure da Visual Studio**

* In Esplora server espandere **Azure** > **HDInsight**, fare clic con il pulsante destro del mouse su un cluster HDInsight e quindi scegliere **Manage Cluster in Azure portal** (Gestisci cluster nel portale di Azure).

**tooask domande e fornire commenti e suggerimenti da Visual Studio**

* Da hello **strumenti** menu, fare clic su **HDInsight**, quindi fare clic su **Forum MSDN** tooask domande, oppure fare clic su **lascia un commento**.

## <a name="navigate-hello-linked-resources"></a>Passare alle risorse di hello collegato
Da Esplora Server, è possibile visualizzare l'account di archiviazione predefinito hello e qualsiasi account di archiviazione collegato. Se si espande l'account di archiviazione predefinito hello, è possibile visualizzare i contenitori di hello in account di archiviazione hello. account di archiviazione predefinito Hello e contenitore predefinito hello sono contrassegnate. È anche possibile fare clic sulla parte del contenuto di hello contenitori tooview hello.

![Elenco di risorse collegate in Esplora server di Strumenti Data Lake per Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.linked.resources.png "Elenco di risorse collegate")

Dopo l'apertura di un contenitore, è possibile utilizzare hello seguente tooupload pulsanti, eliminazione e download BLOB:

![Operazioni sui BLOB in Esplora Server per Data Lake Tools per Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.blob.operations.png "Caricare, eliminare e scaricare BLOB")

## <a name="run-a-hive-query"></a>Eseguire una query Hive
[Apache Hive](http://hive.apache.org) è un'infrastruttura di data warehouse basata su Hadoop che consente di fornire funzionalità di riepilogo, query e analisi di dati. Data Lake Tools per Visual Studio supporta l'esecuzione di query Hive da Visual Studio. Per altre informazioni su Hive, vedere [Usare Hive con HDInsight](hdinsight-use-hive.md).

Si tratta di script Hive tootest molto tempo su un cluster HDInsight. ad esempio alcuni minuti. Data Lake Tools per Visual Studio è in grado di convalidare script Hive in locale senza connessione cluster in tempo reale di tooa.

Data Lake Tools per Visual Studio consente inoltre di toosee gli utenti che cos'è all'interno di processo Hive hello raccogliendo e superfici registri YARN hello di determinati processi Hive.

### <a name="view-hello-hivesampletable"></a>Hello vista **hivesampletable**
I cluster HDInsight includono una tabella Hive di esempio denominata *hivesampletable*. Si userà tooshow questa tabella come tabelle Hive toolist, visualizzare gli schemi di tabella hello ed elenco righe hello hello Hive tabella.

**tabelle Hive toolist e visualizzazione schema della tabella Hive**

1. Da **Esplora Server**, espandere **Azure** > **HDInsight** > cluster hello prescelto > **database Hive**  >  **Predefinito** > **hivesampletable** toosee schema della tabella hello.
2. Fare doppio clic su **hivesampletable**, quindi fare clic su **Visualizza le prime 100 righe** righe hello toolist. È equivalente toorunning hello seguente query Hive tramite driver ODBC Hive:
   
     SELECT * FROM hivesampletable LIMIT 100
   
   È possibile personalizzare il numero di righe hello.
   
   ![Strumenti Data Lake: query sullo schema Hive HDInsight in Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.hive.schema.png "risultati delle query Hive")

### <a name="create-hive-tables"></a>Creare tabelle Hive
È possibile utilizzare GUI di hello toocreate una tabella Hive o utilizzare le query Hive. Per informazioni sull'uso di query Hive, vedere [Eseguire query Hive](#run.queries).

**una tabella Hive toocreate**

1. In **Esplora server** espandere **Azure** > **Cluster HDInsight** > un cluster HDInsight > **Hive Databases** (Database Hive) e quindi fare clic con il pulsante destro del mouse su **default** (predefinito) e scegliere **Crea tabella**.
2. Configurare la tabella hello.
3. Fare clic su **Create Table** toosubmit hello processo toocreate hello nuova tabella Hive.
   
    ![Strumenti Data Lake: creazione di una tabella Hive con gli strumenti di HDInsight per Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.create.hive.table.png "Creare una tabella Hive")

### <a name="run.queries"></a>Convalidare ed eseguire query Hive
Esistono due modi toocreate ed esecuzione di query Hive:

* Creare query ad hoc
* Creare un'applicazione Hive

**toocreate, convalidare ed eseguire query ad hoc**

1. In **Esplora server** espandere **Azure** e quindi **Cluster HDInsight**.
2. Cluster di hello rapida in cui si desidera toorun hello query e quindi fare clic su **scrivere una Query Hive**.
3. Immettere le query Hive hello. Editor dell'Hive hello avviso supporta IntelliSense. Data Lake Tools per Visual Studio supporta il caricamento di hello metadati remoti quando si modifica lo script Hive. Ad esempio, quando si digita "SELECT * FROM", IntelliSense Elenca hello tutti hello i nomi delle tabelle consigliate. Quando viene specificato un nome di tabella, sono elencati i nomi di colonna hello da hello IntelliSense. strumenti di Hello supportano quasi tutte le istruzioni DML Hive, sottoquery e hello incorporato funzioni definite dall'utente.
   
    ![Strumenti Data Lake: IntelliSense negli strumenti di HDInsight per Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.intellisense.table.names.png "IntelliSense in U-SQL")
   
    ![Strumenti Data Lake: IntelliSense negli strumenti di HDInsight per Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.intellisense.column.names.png "IntelliSense in U-SQL")
   
   > [!NOTE]
   > Verranno elencati solo hello i metadati dei cluster hello selezionato nella barra degli strumenti di HDInsight.
   > 
   > 
4. (Facoltativo): fare clic su **convalidare Script** gli errori di sintassi toocheck hello script.
   
    ![Strumenti Data Lake: convalida locale in Strumenti Data Lake per Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.validate.hive.script.png "Convalidare uno script")
5. Fare clic su **Submit** (Invio) o **Submit (Advanced)** (Invio - Avanzato). Con hello Invia opzioni avanzate, sarà necessario configurare **nome del processo**, **argomenti**, **configurazioni aggiuntive**, e **stato Directory**per script hello:
   
    ![Query Hive Hadoop HDInsight](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.submit.jobs.advanced.png "Inviare query")
   
    Dopo aver inviato il processo di hello, vedrai un **riepilogo Hive** finestra.
   
    ![Riepilogo di una query Hive di Hadoop di HDInsight](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.run.hive.job.summary.png "Riepilogo processo Hive")
6. Hello utilizzare **aggiornamento** pulsante stato hello tooupdate finché le modifiche di stato processo hello troppo**completato**.
7. Fare clic sui collegamenti hello negli argomenti seguenti di hello hello inferiore toosee: **processo Query**, **Output processo**, **log processo**, o **log Yarn**.

**toocreate ed eseguire una soluzione di Hive**

1. Da hello **FILE** menu, fare clic su **New**, quindi fare clic su **progetto**.
2. Selezionare **HDInsight** hello riquadro sinistro selezionare **applicazione Hive** nel riquadro centrale hello, immettere le proprietà di hello e quindi fare clic su **OK**.
   
    ![Strumenti Data Lake: nuovo progetto Hive in Strumenti di Visual Studio per HDInsight](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.new.hive.project.png "Creare applicazioni Hive da Visual Studio")
3. Da **Esplora**, fare doppio clic su **Script.hql** tooopen è.
4. script di toovalidate hello Hive, è possibile fare clic su hello **convalidare Script** pulsante o script hello nell'editor Hive hello e quindi fare clic su **convalidare Script** dal menu di scelta rapida hello.

### <a name="view-hive-jobs"></a>Visualizzare processi Hive
È possibile visualizzare query di processo, output di processo, log di processo e log Yarn per i processi Hive. Per ulteriori informazioni, vedere la figura precedente hello.

versione più recente di Hello degli strumenti di hello consente toosee che cos'è all'interno di processi di Hive raccogliendo e superfici YARN log. Un log YARN consente di analizzare eventuali problemi di prestazioni. Per altre informazioni su come HDInsight raccoglie i log YARN, vedere [Accedere ai log dell'applicazione HDInsight a livello di codice](hdinsight-hadoop-access-yarn-app-logs.md).

**processi Hive tooview**

1. In **Esplora server** espandere **Azure** e quindi **HDInsight**.
2. Fare clic con il pulsante destro del mouse su un cluster HDInsight, quindi scegliere **Visualizza processi**. Verrà visualizzato un elenco di hello Hive i processi eseguiti nel cluster hello.
3. Fare clic su un processo in hello processo elenco tooselect e quindi utilizzare hello **riepilogo Hive** tooopen finestra **processo Query**, **Output processo**, **Log processo**, o **log Yarn**.
   
    ![Strumenti Data Lake: visualizzazione dei processi Hive negli strumenti di HDInsight per Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.view.hive.jobs.png "Visualizzare processi Hive")

### <a name="faster-path-hive-execution-via-hiveserver2"></a>Esecuzione di processi Hive più veloce tramite HiveServer2
> [!NOTE]
> Questa funzionalità è disponibile solo per i cluster HDInsight versione 3.2 e successive.
> 
> 

Hello Data Lake Tools utilizzata processi Hive toosubmit tramite [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (noto anche come Templeton). Impiegato un tempo tooreturn i dettagli dei processi e informazioni sull'errore.
Nell'ordine toosolve questo problema di prestazioni, hello Data Lake Tools esegue Hive processi direttamente nel cluster hello tramite HiveServer2, in modo che ignori RDP/SSH.
Prestazioni toobetter inoltre, gli utenti possono anche visualizzare Hive sui grafici Tez e hello dettagli attività.

Per cluster HDInsight versione 3.2 o successiva, è disponibile un pulsante **Execute via HiveServer2** (Esegui tramite HiveServer2):

![Esecuzione tramite HiveServer2 in Strumenti Data Lake per Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.execute.via.hiveserver2.png "Eseguire query Hive usando HiveServer2")

Ed è possibile vedere i registri di hello streaming in tempo reale e vedere i grafici di processo hello se query Hive hello viene eseguita in Tez.

![Esecuzione di processi Hive più veloce in Strumenti Data Lake per Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.fast.path.hive.execution.png "Visualizzare i grafici dei processi")

**Differenza tra l'esecuzione di query tramite HiveServer2 e l'invio di query tramite WebHCat**

L'esecuzione di query tramite HiveServer2 presenta numerosi vantaggi in termini di prestazioni, ma anche diverse limitazioni. Alcune delle limitazioni di hello non sono adatti per l'utilizzo di produzione. Hello nella tabella seguente illustra le differenze di hello:

|  | Esecuzione tramite HiveServer2 | Invio tramite WebHCat |
| --- | --- | --- |
| Eseguire query |Elimina l'overhead di hello in WebHCat (che avvia un MapReduce Job denominato "TempletonControllerJob"). |Se la query viene eseguita tramite WebHCat, WebHCat avvierà un processo MapReduce con il quale viene introdotta latenza aggiuntiva. |
| Trasmettere log |Quasi in tempo reale. |i log di esecuzione processo Hello sono disponibili solo quando il processo di hello è completato. |
| Visualizzare la cronologia processo |Se una query viene eseguita tramite HiveServer2, la relativa cronologia processo (log del processo e output del processo) non viene mantenuta. un'applicazione Hello può essere visualizzata nell'interfaccia utente di YARN con informazioni limitate. |Se una query viene eseguita tramite WebHCat, la relativa cronologia processo (il log del processo, l'output del processo) viene mantenuta e può essere visualizzata tramite Visual Studio, HDInsight SDK o PowerShell. |
| Chiudere la finestra |L'esecuzione tramite HiveServer2 è un modo "sincrono" in modo da lasciare hello aprire windows; Se vengono chiuse windows hello verrà annullata l'esecuzione di query hello. |Invio tramite WebHCat è un modo "asincrono" per poter inviare la query tramite WebHCat hello e chiudere Visual Studio. È possibile tornare e visualizzare i risultati di hello in qualsiasi momento. |

### <a name="tez-hive-job-performance-graph"></a>Grafico delle prestazioni del processo Hive Tez
supporto Data Lake Tools Hello visualizzazione grafici delle prestazioni per hello Hive processi è stata eseguita dal motore di esecuzione Tez hello. Per informazioni su come abilitare Tez, vedere l'articolo relativo all'[uso di Hive in HDInsight](hdinsight-use-hive.md). Dopo aver inviato un Hive Mostra processi in Visual Studio, Visual Studio hello grafico quando viene completato il processo di hello.  Potrebbe essere necessario hello tooclick **aggiornamento** pulsante tooget stato hello del modello di processo più recente.

> [!NOTE]
> Questa funzionalità è disponibile solo per le versioni del cluster HDInsight successive alla 3.2.4.593 e funzionano solo per i processi completati, se il processo è stato inviato tramite WebHCat. Questo grafico viene visualizzato quando si esegue la query tramite HiveServer2. Si possono usare cluster basati sia su Windows che su Linux.
> 
> 

![Grafico delle prestazioni di Tez in Hive in Hadoop](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.hive.tez.performance.graph.png "Stato del processo")

comprendere l'Hive toohelp query migliori, strumenti hello aggiungono Visualizza operatore Hive hello in questa versione. È sufficiente fare clic sui vertici hello del grafico processi hello toodouble ed è possibile visualizzare tutti gli operatori di hello all'interno di hello vertice. È anche possibile posizionare in un particolare operatore tooview ulteriori dettagli di questo operatore.

### <a name="task-execution-view-for-hive-on-tez-jobs"></a>Visualizzazione dell'esecuzione dell'attività per i processi Hive in Tez
Hello visualizzazione esecuzione di attività per Hive sui processi Tez può essere utilizzato tooget strutturato e visualizzare informazioni relative ai processi Hive e ottenere più dettagli processo. Quando sono presenti problemi di prestazioni, è possibile utilizzare hello tooget ulteriori dettagli. Ad esempio, come ogni attività viene eseguita e hello informazioni dettagliate su ogni attività (lettura/scrittura di dati, ora di inizio/pianificazione/fine e così via), in modo che è possibile ottimizzare le configurazioni di processo o l'architettura del sistema in base alle informazioni di hello visualizzato.

![Visualizzazione dell'esecuzione dell'attività in Strumenti Data Lake per Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.task.execution.view.png "Visualizzazione dell'esecuzione dell'attività")

## <a name="run-pig-scripts"></a>Eseguire script Pig
Data Lake Tools per Visual Studio supporta la creazione e inviare i cluster tooHDInsight script Pig. Gli utenti possono creare un progetto Pig dal modello e quindi inviare i cluster tooHDInsight script hello.

## <a name="feedbacks--known-issues"></a>Commenti e suggerimenti e problemi noti
* Attualmente i risultati di HiveServer2 vengono visualizzati in modalità solo testo, che non è ideale. La correzione del problema è attualmente in corso.
* Se i risultati di hello vengono avviati con valori NULL, attualmente risultati hello non vengono visualizzati. Si have risolto questo problema e se sono bloccate su questo problema, è possibile toodrop gratuito a un messaggio di posta elettronica o un contatto di supporto tecnico.
* script HQL Hello creato da Visual Studio viene codificato in base alle impostazioni area locale dell'utente. Potrebbe non essere eseguito correttamente se l'utente carica toocluster script hello in formato binario.

## <a name="next-steps"></a>Passaggi successivi
In questo articolo, si è appreso come tooconnect tooHDInsight cluster da Visual Studio, hello Data Lake (HDInsight) utilizzando il pacchetto di strumenti e come toorun una query Hive. Per altre informazioni, vedere:

* [Usare Hive di Hadoop in HDInsight](hdinsight-use-hive.md)
* [Introduzione all'uso di Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Inviare processi Hadoop in HDInsight](hdinsight-submit-hadoop-jobs-programmatically.md)
* [Analizzare i dati di Twitter con Hadoop in HDInsight](hdinsight-analyze-twitter-data.md)

