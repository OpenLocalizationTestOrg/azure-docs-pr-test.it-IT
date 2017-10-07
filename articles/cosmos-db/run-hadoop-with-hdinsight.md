---
title: aaaRun un Hadoop processo utilizzando Azure Cosmos DB e HDInsight | Documenti Microsoft
description: Informazioni su come toorun un semplice Hive, Pig e MapReduce processo con DB Cosmos Azure e Azure HDInsight.
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 06f0ea9d-07cb-4593-a9c5-ab912b62ac42
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 06/08/2017
ms.author: denlee
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2e27499f2c4ba951af9a1ade1bcc9c1b6d298fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="Azure Cosmos DB-HDInsight"></a>Eseguire un processo Apache Hive, Pig o Hadoop usando Azure Cosmos DB e HDInsight
In questa esercitazione illustra come toorun [Apache Hive][apache-hive], [Pig Apache][apache-pig], e [Apache Hadoop] [ apache-hadoop] Processi MapReduce in Azure HDInsight con connettore Hadoop Cosmos DB. Connettore Hadoop COSMOS DB consente tooact DB Cosmos come origine e sink per i processi Hive, Pig e MapReduce. In questa esercitazione verrà utilizzato DB Cosmos come origine dati hello e di destinazione per i processi di Hadoop.

Dopo aver completato questa esercitazione, sarà in grado di tooanswer hello seguenti domande:

* Come si caricano i dati da Cosmos DB usando un processo Hive, Pig o MapReduce?
* Come si archiviano i dati in Cosmos DB usando un processo Hive, Pig o MapReduce?

Si consiglia di iniziare, è possibile guardare hello seguente video, in cui è eseguito tramite un processo Hive usando DB Cosmos e HDInsight.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

Tornare quindi toothis articolo, in cui si riceverà i dettagli completi hello su come eseguire processi analitica sui dati Cosmos DB.

> [!TIP]
> Questa esercitazione presume che l'utente abbia una precedente esperienza nell'uso di Apache Hadoop, Hive e/o Pig. Se si tooApache nuova Hadoop, Hive e Pig, si consiglia di visitare hello [documentazione di Apache Hadoop][apache-hadoop-doc]. Questa esercitazione presuppone che si abbia esperienza con Cosmos DB e che sia disponibile un account Cosmos DB. Se si è tooCosmos nuovo database o non è un account Cosmos DB, estrarre il nostro [Introduzione] [ getting-started] pagina.
>
>

Non si dispone ora toocomplete hello esercitazione e visualizzare solo gli script di PowerShell per un esempio completo di hello tooget per Hive, Pig e MapReduce? È possibile ottenerli [qui][hdinsight-samples]. download di Hello contiene anche file hql, pig e java di hello per questi esempi.

## <a name="NewestVersion"></a>Versione più recente
<table border='1'>
    <tr><th>Versione di Hadoop Connector</th>
        <td>1.2.0</td></tr>
    <tr><th>URI script</th>
        <td>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</td></tr>
    <tr><th>Data ultima modifica</th>
        <td>26/04/2016</td></tr>
    <tr><th>Versioni supportate di HDInsight</th>
        <td>3.1, 3.2.</td></tr>
    <tr><th>Registro modifiche</th>
        <td>Aggiornare Azure Cosmos DB Java SDK too1.6.0</br>
            Aggiunta del supporto per le raccolte partizionate come origine e sink</br>
        </td></tr>
</table>

## <a name="Prerequisites"></a>Prerequisiti
Prima di seguire le istruzioni di hello in questa esercitazione, assicurarsi di aver seguito hello:

* Un account Cosmos DB, un database e una raccolta di documenti all'interno. Per altre informazioni, vedere l'[introduzione a Cosmos DB][getting-started]. Importare i dati di esempio al tuo account DB Cosmos con hello [lo strumento di importazione Cosmos DB][import-data].
* Velocità effettiva. Le letture e le scritture da HDInsight verranno conteggiate rispetto alle unità di richiesta dell'unità di capacità.
* Capacità di una stored procedure aggiuntiva all'interno di ciascun insieme di output. Hello stored procedure vengono utilizzate per il trasferimento di documenti risultanti.
* Capacità per i documenti risultante hello dai processi di hello Hive, Pig e MapReduce.
* *Facoltativo*Capacità per una raccolta aggiuntiva.

> [!WARNING]
> Ordine tooavoid hello creazione di una nuova raccolta durante uno dei processi di hello, è possibile stampare hello risultati toostdout, salvare contenitore WASB tooyour output di hello oppure specificare una raccolta già esistente. In caso hello della specifica di una raccolta esistente, verranno creati nuovi documenti all'interno di hello e documenti già esistenti saranno interessati solo se si verifica un conflitto in *ID*. **connettore Hello sovrascrive automaticamente i documenti esistenti con conflitti tra id**. È possibile disattivare questa funzionalità impostando hello upsert opzione toofalse. Se si verifica un conflitto upsert è false, avrà esito negativo del processo Hadoop hello; viene rilevato un errore di conflitto di id.
>
>

## <a name="ProvisionHDInsight"></a>Passaggio 1: Creare un nuovo cluster HDInsight
Questa esercitazione Usa genera Script azione da hello Azure Portal toocustomize cluster HDInsight. In questa esercitazione si utilizzerà hello Azure Portal toocreate cluster HDInsight. Per istruzioni su come i cmdlet di PowerShell toouse o hello HDInsight .NET SDK, vedere il [HDInsight personalizzare cluster tramite Script azione] [ hdinsight-custom-provision] articolo.

1. Accedi toohello [portale Azure][azure-portal].
2. Fare clic su **+ nuovo** nella parte superiore di hello del riquadro di spostamento sinistro hello, Cerca **HDInsight** sulla barra di ricerca principale hello nuovo pannello hello.
3. **HDInsight** pubblicati da **Microsoft** verrà visualizzato nella parte superiore di hello dei risultati di hello. Fare clic sulla voce e selezionare **Crea**.
4. Nel nuovo HDInsight Cluster hello creare pannello, immettere il **nome Cluster** e seleziona hello **sottoscrizione** desiderato tooprovision questa risorsa in.

    <table border='1'>
        <tr><td>Nome del cluster</td><td>Cluster hello nome.<br/>
Il nome DNS deve iniziare e finire con un carattere alfanumerico e può contenere trattini.<br/>
campo Hello deve essere una stringa di lunghezza compresa tra 3 e 63 caratteri.</td></tr>
        <tr><td>Nome sottoscrizione</td>
            <td>Se si dispone di più di una sottoscrizione di Azure, selezionare una sottoscrizione di hello che ospiterà il cluster HDInsight. </td></tr>
    </table>
5.Fare clic su **Seleziona tipo di Cluster** e hello set seguenti toohello di proprietà specificati.

    <table border='1'>
        <tr><td>Tipo di cluster</td><td><strong>Hadoop</strong></td></tr>
        <tr><td>Livello cluster</td><td><strong>Standard</strong></td></tr>
        <tr><td>Sistema operativo</td><td><strong>Windows</strong></td></tr>
        <tr><td>Versione</td><td>versione più recente</td></tr>
    </table>

    A questo punto fare clic su **SELEZIONA**.

    ![Fornire i dettagli di iniziale del cluster Hadoop HDInsight][image-customprovision-page1]
6. Fare clic su **credenziali** tooset le credenziali di accesso remoto e l'account di accesso. Scegliere il **nome utente dell'account di accesso del cluster** e la **password dell'account di accesso del cluster**.

    Se si desidera tooremote in cluster, selezionare *Sì* nella parte inferiore di hello del pannello hello e fornire un nome utente e password.
7. Fare clic su **origine dati** tooset la posizione principale per i dati di accesso. Scegliere hello **Selezione metodo** e specificare un account di archiviazione già esistente o crearne uno nuovo.
8. In hello pannello stesso, specificare un **contenitore predefinito** e **percorso**. Fare quindi clic su **SELEZIONA**.

   > [!NOTE]
   > Selezionare un tooyour Chiudi percorso area dell'account DB Cosmos per migliorare le prestazioni
   >
   >
9. Fare clic su **prezzi** tooselect hello numero e tipo di nodi. È possibile mantenere configurazione predefinita di hello e scala hello numero di nodi di lavoro in un secondo momento.
10. Fare clic su **configurazione facoltativa**, quindi **azioni Script** in hello pannello configurazione facoltativa.

     Nel riquadro azioni Script immettere hello toocustomize informazioni seguendo il cluster HDInsight.

     <table border='1'>
         <tr><th>Proprietà</th><th>Valore</th></tr>
         <tr><td>Nome</td>
             <td>Specificare un nome per l'azione script hello.</td></tr>
         <tr><td>URI script</td>
             <td>Specificare hello URI toohello script che è richiamato toocustomize hello cluster.</br></br>
Immettere: </br> <strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</td></tr>
         <tr><td>Head</td>
             <td>Fare clic sulla casella di controllo di prova toorun prova script di PowerShell nel nodo Head hello.</br></br>
             <strong>Selezionare questa casella di controllo</strong>.</td></tr>
         <tr><td>Worker</td>
             <td>Fare clic su script PowerShell hello hello casella di controllo toorun nel nodo lavoro hello.</br></br>
             <strong>Selezionare questa casella di controllo</strong>.</td></tr>
         <tr><td>Zookeeper</td>
             <td>Fare clic su script PowerShell su hello Zookeeper hello casella di controllo toorun hello.</br></br>
             <strong>Non necessario</strong>.
             </td></tr>
         <tr><td>parameters</td>
             <td>Specificare i parametri di hello, se richiesti dallo script hello.</br></br>
             <strong>Nessun parametro necessario</strong>.</td></tr>
     </table>
11. Creare un nuovo **gruppo di risorse** o usarne uno esistente nella sottoscrizione di Azure.
12. A questo punto, controllare **Pin toodashboard** tootrack la distribuzione e fare clic su **crea**!

## <a name="InstallCmdlets"></a>Passaggio 2: Installare e configurare Azure PowerShell
1. Installare Azure PowerShell. Le istruzioni sono consultabili [qui][powershell-install-configure].

   > [!NOTE]
   > In alternativa, solo per le query Hive, è possibile usare l'Editor Hive online di HDInsight. toodo accedere in tal caso, toohello [portale Azure][azure-portal], fare clic su **HDInsight** tooview riquadro sinistro di hello in un elenco dei cluster HDInsight. Fare clic su cluster hello si desidera che le query Hive toorun su e quindi fare clic su **Console Query**.
   >
   >
2. Aprire Azure PowerShell Integrated Scripting Environment hello:

   * In un computer che eseguono Windows 8 o Windows Server 2012 o versioni successive, è possibile utilizzare predefinito di hello ricerca. Dalla schermata Start hello digitare **powershell ise** e fare clic su **invio**.
   * In un computer che eseguono una versione precedente a Windows 8 o Windows Server 2012, utilizzare il menu di avvio hello. Dal menu di avvio hello, digitare **prompt dei comandi** nella casella di ricerca hello, quindi nell'elenco di hello dei risultati, fare clic su **prompt dei comandi**. In hello prompt dei comandi, digitare **powershell_ise** e fare clic su **invio**.
3. Aggiungere il proprio Account Azure.

   1. Nel riquadro della Console hello, digitare **Add-AzureAccount** e fare clic su **invio**.
   2. Digitare l'indirizzo di posta elettronica hello associati alla sottoscrizione Azure e fare clic su **continua**.
   3. Digitare la password hello per la sottoscrizione di Azure.
   4. Fare clic su **Accedi**.
4. Hello diagramma seguente identifica le parti importanti di hello dell'ambiente di Scripting PowerShell Azure.

    ![Diagramma per Azure PowerShell][azure-powershell-diagram]

## <a name="RunHive"></a>Passaggio 3: Eseguire un processo Hive usando Cosmos DB e HDInsight
> [!IMPORTANT]
> Tutte le variabili indicate da < > devono essere compilate usando le proprie impostazioni di configurazione.
>
>

1. Impostare hello seguenti variabili nel riquadro di Script di PowerShell.

        # Provide Azure subscription name, hello Azure Storage account and container that is used for hello default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide hello HDInsight cluster name where you want toorun hello Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p>Si inizia a costruire la stringa di query. Da scrivere una query Hive che accetta i timestamp generati dal sistema ( TS) e un ID univoco ( RID) da una raccolta di Azure Cosmos DB tutti i documenti, conta tutti i documenti di minuto hello e quindi Archivia i risultati di hello in una nuova raccolta di Azure Cosmos DB.</p>

    <p>Creare prima di tutto una tabella Hive dalla raccolta Azure Cosmos DB. Aggiungere hello seguente frammento di codice toohello riquadro di Script PowerShell <strong>dopo</strong> frammento di codice hello #1. Assicurarsi di includere hello facoltativo DocumentDB.query parametro t trim nostri TS toojust di documenti e RID.</p>

   > [!NOTE]
   > **La denominazione DocumentDB.inputCollections non è stata un errore.** È effettivamente possibile aggiungere più raccolte come input: </br>
   >
   >

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> hello collection names are separated without spaces, using only a single comma.

        # Create a Hive table using data from DocumentDB. Pass DocumentDB hello query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

1. Successivamente, creare una tabella Hive per la raccolta di output di hello. proprietà del documento di output di Hello sarà mese hello, giorno, ora, minuti e il numero totale di hello di occorrenze.

   > [!NOTE]
   > **Ancora una volta, la denominazione di DocumentDB.outputCollections non è un errore.** È effettivamente possibile aggiungere più raccolte come output: </br>
   > '*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*' </br> i nomi di raccolta Hello sono separati senza spazi, utilizzare solo una singola virgola. </br></br>
   > Verrà eseguita la distribuzione round robin dei documenti tra più raccolte. Un batch di documenti verrà archiviato in una raccolta, quindi un secondo batch dei documenti verrà archiviato nella raccolta di hello successivo e così via.
   >
   >

       # Create a Hive table for hello output data tooDocumentDB.
       $queryStringPart2 = "drop table DocumentDB_analytics; " +
                             "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                             "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                             "tblproperties ( " +
                                 "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                 "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                 "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                 "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "
2. Infine, si conteggio hello documenti per mese, giorno, ora e minuto e all'inserimento risultati hello in hello output tabella Hive.

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. Aggiungere hello seguente frammento di script toocreate la definizione di un processo Hive dalla query precedente hello.

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    È inoltre possibile utilizzare hello - File passare toospecify un file di script HiveQL in HDFS.
4. Aggiungere hello dopo l'ora di inizio hello toosave frammento di codice e inviare il processo Hive hello.

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. Aggiungere i seguenti toowait per hello Hive processo toocomplete hello.

        # Wait for hello Hive job toocomplete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. Aggiungere hello segue tooprint hello standard hello e output inizio e ora di fine.

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. **Eseguire** il nuovo script. **Fare clic su** verde hello pulsante Esegui.
8. Controllare i risultati di hello. Sign in hello [portale Azure][azure-portal].

   1. Fare clic su <strong>Sfoglia</strong> nel Pannello di sinistra hello. </br>
   2. Fare clic su <strong>tutto</strong> in alto a destra di hello del pannello Sfoglia hello. </br>
   3. Trovare e fare clic su <strong>Account Azure Cosmos DB</strong>. </br>
   4. Successivamente, individuare il <strong>Azure Cosmos DB Account</strong>, quindi <strong>Azure Cosmos DB Database</strong> e <strong>Azure Cosmos DB raccolta</strong> associato specificato nella raccolta di output di hello la query Hive.</br>
   5. Infine, fare clic su <strong>Esplora documenti</strong> sotto <strong>Strumenti di sviluppo</strong>.</br></p>

   Vengono visualizzati hello risultati della query Hive.

   ![Risultati della query relativa alla tabella][image-hive-query-results]

## <a name="RunPig"></a>Passaggio 4: Eseguire un processo Pig usando Cosmos DB e HDInsight
> [!IMPORTANT]
> Tutte le variabili indicate da < > devono essere compilate usando le proprie impostazioni di configurazione.
>
>

1. Impostare hello seguenti variabili nel riquadro di Script di PowerShell.

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want toorun hello Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p>Si inizia a costruire la stringa di query. Da scrivere una query Pig che accetta i timestamp generati dal sistema ( TS) e un ID univoco ( RID) da una raccolta di Azure Cosmos DB tutti i documenti, conta tutti i documenti di minuto hello e quindi Archivia i risultati di hello in una nuova raccolta di Azure Cosmos DB.</p>
    <p>In primo luogo, caricare i documenti da Cosmos DB in HDInsight. Aggiungere hello seguente frammento di codice toohello riquadro di Script PowerShell <strong>dopo</strong> frammento di codice hello #1. Assicurarsi che tooadd un DocumentDB query toohello facoltativo DocumentDB query parametro tootrim nostri TS toojust di documenti e RID.</p>

   > [!NOTE]
   > È effettivamente possibile aggiungere più raccolte come input: </br>
   > '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</br> i nomi di raccolta Hello sono separati senza spazi, utilizzare solo una singola virgola. </b>
   >
   >

    Verrà eseguita la distribuzione round robin dei documenti tra più raccolte. Un batch di documenti verrà archiviato in una raccolta, quindi un secondo batch dei documenti verrà archiviato nella raccolta di hello successivo e così via.

        # Load data from Cosmos DB. Pass DocumentDB query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. Successivamente, consente di calcolare documenti hello dal mese di hello, giorno, ora, minuti e il numero totale di hello di occorrenze.

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. Infine, si archiviare i risultati di hello nella nuova raccolta di output.

   > [!NOTE]
   > È effettivamente possibile aggiungere più raccolte come output: </br>
   > '\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</br> i nomi di raccolta Hello sono separati senza spazi, utilizzare solo una singola virgola.</br>
   > Documenti verrà essere distribuito round robin tra hello più raccolte. Un batch di documenti verrà archiviato in una raccolta, quindi un secondo batch dei documenti verrà archiviato nella raccolta di hello successivo e così via.
   >
   >

        # Store output data tooCosmos DB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. Aggiungere hello seguente frammento di script toocreate la definizione di un processo Pig dalla query precedente hello.

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    È inoltre possibile utilizzare hello - File passare toospecify un file di script Pig in HDFS.
6. Aggiungere hello dopo l'ora di inizio hello toosave frammento di codice e inviare il processo Pig hello.

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. Aggiungere i seguenti toowait per hello Pig processo toocomplete hello.

        # Wait for hello Pig job toocomplete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. Aggiungere hello segue tooprint hello standard hello e output inizio e ora di fine.

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. **Eseguire** il nuovo script. **Fare clic su** verde hello pulsante Esegui.
10. Controllare i risultati di hello. Sign in hello [portale Azure][azure-portal].

    1. Fare clic su <strong>Sfoglia</strong> nel Pannello di sinistra hello. </br>
    2. Fare clic su <strong>tutto</strong> in alto a destra di hello del pannello Sfoglia hello. </br>
    3. Trovare e fare clic su <strong>Account Azure Cosmos DB</strong>. </br>
    4. Successivamente, individuare il <strong>Azure Cosmos DB Account</strong>, quindi <strong>Azure Cosmos DB Database</strong> e <strong>Azure Cosmos DB raccolta</strong> associato specificato nella raccolta di output di hello la query Pig.</br>
    5. Infine, fare clic su <strong>Esplora documenti</strong> sotto <strong>Strumenti di sviluppo</strong>.</br></p>

    Vengono visualizzati hello risultati della query Pig.

    ![Risultati della query SQL][image-pig-query-results]

## <a name="RunMapReduce"></a>Passaggio 5: Eseguire un processo MapReduce usando Azure Cosmos DB e HDInsight
1. Impostare hello seguenti variabili nel riquadro di Script di PowerShell.

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. Verrà verrà eseguito un processo MapReduce che conta il numero di hello di occorrenze per ogni proprietà di documento dalla raccolta di Azure Cosmos DB. Aggiungere questo frammento di script **dopo** frammento hello precedente.

        # Define hello MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > TallyProperties v01.jar viene fornito con installazione personalizzata di hello di hello connettore Hadoop di DB Cosmos.
   >
   >
3. Aggiungere hello processo MapReduce hello toosubmit il comando seguente.

        # Save hello start time and submit hello job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    Inoltre toohello definizione processo MapReduce, è inoltre fornire nome del cluster HDInsight hello in cui si desidera il processo MapReduce toorun hello e le credenziali di hello. Start-AzureHDInsightJob Hello è una chiamata asincrona. completamento di hello toocheck del processo di hello, utilizzare hello *Wait-AzureHDInsightJob* cmdlet.
4. Aggiungere hello successivo comando toocheck tutti gli errori con il processo MapReduce hello in esecuzione.

        # Get hello job output and print hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. **Eseguire** il nuovo script. **Fare clic su** verde hello pulsante Esegui.
6. Controllare i risultati di hello. Sign in hello [portale Azure][azure-portal].

   1. Fare clic su <strong>Sfoglia</strong> nel Pannello di sinistra hello.
   2. Fare clic su <strong>tutto</strong> in alto a destra di hello del pannello Sfoglia hello.
   3. Trovare e fare clic su <strong>Account Azure Cosmos DB</strong>.
   4. Successivamente, individuare il <strong>Azure Cosmos DB Account</strong>, quindi <strong>Azure Cosmos DB Database</strong> e <strong>Azure Cosmos DB raccolta</strong> associato specificato nella raccolta di output di hello il processo MapReduce.
   5. Infine, fare clic su <strong>Esplora documenti</strong> sotto <strong>Strumenti di sviluppo</strong>.

      Vengono visualizzati risultati hello del processo MapReduce.

      ![Risultati della query MapReduce][image-mapreduce-query-results]

## <a name="NextSteps"></a>Passaggi successivi
Congratulazioni. Sono stati eseguiti i primi processi Hive, Pig e MapReduce usando Azure Cosmos DB e HDInsight.

Abbiamo reso Open Source il connettore Hadoop. Se si è interessati, è possibile contribuire in [GitHub][github].

toolearn informazioni, vedere hello seguenti articoli:

* [Sviluppare un'applicazione Java con Documentdb][documentdb-java-application]
* [Sviluppare programmi MapReduce Java per Hadoop in HDInsight][hdinsight-develop-deploy-java-mapreduce]
* [Introduzione all'uso di Hadoop con Hive in uso di HDInsight tooanalyze palmari mobili][hdinsight-get-started]
* [Usare MapReduce con HDInsight][hdinsight-use-mapreduce]
* [Usare Hive con HDInsight][hdinsight-use-hive]
* [Usare Pig con HDInsight][hdinsight-use-pig]
* [Personalizzare cluster HDInsight mediante l'azione script][hdinsight-hadoop-customize-cluster]

[apache-hadoop]: http://hadoop.apache.org/
[apache-hadoop-doc]: http://hadoop.apache.org/docs/current/
[apache-hive]: http://hive.apache.org/
[apache-pig]: http://pig.apache.org/
[getting-started]: documentdb-get-started.md

[azure-portal]: https://portal.azure.com/
[azure-powershell-diagram]: ./media/run-hadoop-with-hdinsight/azurepowershell-diagram-med.png

[hdinsight-samples]: http://portalcontent.blob.core.windows.net/samples/documentdb-hdinsight-samples.zip
[github]: https://github.com/Azure/azure-documentdb-hadoop
[documentdb-java-application]: documentdb-java-application.md
[import-data]: import-data.md

[hdinsight-custom-provision]: ../hdinsight/hdinsight-provision-clusters.md
[hdinsight-develop-deploy-java-mapreduce]: ../hdinsight/hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-hadoop-customize-cluster]: ../hdinsight/hdinsight-hadoop-customize-cluster.md
[hdinsight-get-started]: ../hdinsight/hdinsight-hadoop-tutorial-get-started-windows.md
[hdinsight-storage]: ../hdinsight/hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: ../hdinsight/hdinsight-use-hive.md
[hdinsight-use-mapreduce]: ../hdinsight/hdinsight-use-mapreduce.md
[hdinsight-use-pig]: ../hdinsight/hdinsight-use-pig.md

[image-customprovision-page1]: ./media/run-hadoop-with-hdinsight/customprovision-page1.png
[image-hive-query-results]: ./media/run-hadoop-with-hdinsight/hivequeryresults.PNG
[image-mapreduce-query-results]: ./media/run-hadoop-with-hdinsight/mapreducequeryresults.PNG
[image-pig-query-results]: ./media/run-hadoop-with-hdinsight/pigqueryresults.PNG

[powershell-install-configure]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0
