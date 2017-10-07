---
title: aaaGet avviato con il Server di R in HDInsight - Azure | Documenti Microsoft
description: Informazioni su come toocreate un Apache nascita nel cluster HDInsight che include i Server di R e inviare uno script R in cluster hello.
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b5e111f3-c029-436c-ba22-c54a4a3016e3
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/14/2017
ms.author: bradsev
ms.openlocfilehash: f7e418bbac48eee080a4b4cfbb33e246324ea5c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-using-r-server-on-hdinsight"></a>Introduzione all'uso di R Server su HDInsight

HDInsight include un toobe opzione R Server integrato nel cluster HDInsight. Questa opzione consente agli script R toouse Spark e MapReduce toorun distribuiti i calcoli. In questo documento, viene illustrato come un Server di R in cluster HDInsight e quindi Esegui una R script che illustra l'uso di Spark per toocreate distribuiti calcoli R.


## <a name="prerequisites"></a>Prerequisiti

* **Una sottoscrizione di Azure**: prima di iniziare questa esercitazione è necessario avere una sottoscrizione di Azure. Articolo passare toohello [versione di valutazione gratuita di Microsoft Azure ottenere](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) per ulteriori informazioni.
* **Un client Secure Shell (SSH)**: viene usato un SSH client tooremotely cluster HDInsight toohello connettersi ed eseguire comandi direttamente nel cluster hello. Per altre informazioni, vedere l'articolo su come [usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).
* **Le chiavi SSH (facoltative)**: È possibile proteggere hello SSH account utilizzato tooconnect toohello cluster tramite una password o una chiave pubblica. Utilizzando una password è più semplice e consente di tooget avviato senza toocreate una coppia di chiavi pubblica/privata. Tuttavia, usare una chiave è più sicuro.

> [!NOTE]
> passaggi di Hello in questo documento si presuppongono che si sta utilizzando una password.


## <a name="automated-cluster-creation"></a>Creazione automatizzata di cluster

È possibile automatizzare la creazione di hello di HDInsight R Servers tramite Gestione risorse di Azure modelli, hello SDK e anche PowerShell.

* toocreate un Server di R usando un modello di gestione delle risorse di Azure, vedere [distribuire un cluster di HDInsight R server](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).
* toocreate un Server di R usando hello .NET SDK, vedere [creare cluster basati su Linux in HDInsight mediante hello .NET SDK.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)
* R Server toodeploy tramite powershell, vedere l'articolo hello in [creazione di un Server di R in HDInsight con PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).


<a name="create-hdi-custer-with-aure-portal"></a>
## <a name="create-hello-cluster-using-hello-azure-portal"></a>Creare il cluster di hello utilizzando hello portale di Azure

1. Accedi toohello [portale di Azure](https://portal.azure.com).

2. Selezionare **Nuovo** -> **Intelligence e analisi** -> **HDInsight**.

    ![Immagine della creazione di un nuovo cluster](./media/hdinsight-hadoop-r-server-get-started/newcluster.png)

3. In hello **creazione rapida** esperienza, immettere un nome per il cluster hello in hello **nome Cluster** campo. Se si dispone di più sottoscrizioni di Azure, utilizzare hello **sottoscrizione** voce tooselect hello uno desiderato toouse.

    ![Selezione del nome del cluster e della sottoscrizione](./media/hdinsight-hadoop-r-server-get-started/clustername.png)

4. Selezionare **Cluster tipo** tooopen hello **configurazione Cluster** blade. In hello **configurazione Cluster** pannello hello seleziona le opzioni seguenti:

    * **Tipo di cluster**: R Server
    * **Versione**: versione di hello selezionare tooinstall R Server nel cluster hello. versione di Hello attualmente disponibile è ***R Server 9.1 (HDI 3.6)***. Sono disponibili note sulla versione per le versioni disponibili di hello del Server di R [qui](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).
    * **Edizione community R Studio per R Server**: questo IDE basate su browser viene installato per impostazione predefinita nel nodo edge hello. Se si preferisce toonot è installato, quindi deselezionare la casella di controllo hello. Se si sceglie toohave è installato, hello URL per l'accesso a hello accesso RStudio Server si trova in un pannello dell'applicazione del portale per il cluster dopo averla creata.
    * Lasciare le altre opzioni hello i valori predefiniti di hello e utilizzare hello **selezionare** toosave hello cluster tipo di pulsante.

        ![Schermata del pannello del tipo di cluster](./media/hdinsight-hadoop-r-server-get-started/clustertypeconfig.png)

5. Immettere il **nome utente dell'account di accesso del cluster** e la **password dell'account di accesso del cluster**.

    Specificare un **nome utente SSH**. SSH è usato tooremotely connettersi toohello cluster utilizzando un **Secure Shell (SSH)** client. È possibile specificare utente SSH hello in questa finestra di dialogo oppure dopo la creazione del cluster hello (nella scheda Configurazione di hello per cluster hello). R Server è configurato tooexpect un **nome utente SSH** di "remoteuser".  **Se si utilizza un nome utente diverso, è necessario eseguire un passaggio aggiuntivo dopo la creazione di cluster hello.**

    La casella di hello lasciare per **usare stessa password account di accesso cluster** toouse **PASSWORD** come hello l'autenticazione di tipo a meno che non si preferisce l'utilizzo di una chiave pubblica.  È necessario tooaccess una coppia di chiavi pubblica/privata R Server nel cluster hello tramite un client come, ad esempio, RTVS, RStudio o altri IDE desktop remoto. Se si installa hello edizione community RStudio Server, è necessario toochoose una password SSH.     

    toocreate e utilizzare una coppia di chiavi pubblica/privata, deselezionare **usare stessa password account di accesso cluster** e quindi selezionare **chiave pubblica** e procedere come segue. Queste istruzioni presuppongono che Cygwin con ssh-keygen o equivalente sia già installato.

    * Generare una coppia di chiavi pubblica/privata dal prompt dei comandi di hello in un computer portatile:

        ssh-keygen -t rsa -b 2048

    * Seguire hello prompt tooname un file di chiave, quindi immettere una passphrase per una maggiore sicurezza. La schermata dovrebbe essere simile al seguente hello seguente immagine:

        ![Riga di comando SSH in Windows](./media/hdinsight-hadoop-r-server-get-started/sshcmdline.png)

    * Questo comando crea un file di chiave privata e un file di chiave pubblica in hello < privato-key-filename > nome pub, ad esempio furiosa e furiosa.pub.

        ![Dir SSH](./media/hdinsight-hadoop-r-server-get-started/dir.png)

    * Specificare quindi il file di chiave pubblica hello (&#42;. pub) quando l'assegnazione HDI le credenziali del cluster e infine verificare il gruppo di risorse, area e selezionare **Avanti**.

        ![Pannello Credenziali](./media/hdinsight-hadoop-r-server-get-started/publickeyfile.png)  

   * Modificare le autorizzazioni per file di chiave privata hello in un computer portatile:

        chmod 600 <private-key-filename>

   * Utilizzare il file di chiave privata di hello con SSH per l'accesso remoto:

        ssh –i <private-key-filename> remoteuser@<hostname public ip>

      In alternativa, come definizione di hello parte di Spark il Hadoop contesto di calcolo per il Server di R nel client hello. Vedere hello **utilizzando Microsoft R Server come Hadoop Client** sottosezione [creare un contesto di calcolo per Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).

6. Creazione rapida di Hello si esegue la transizione toohello **archiviazione** account archiviazione hello tooselect pannello impostazioni toobe hello al percorso principale di hello HDFS file system utilizzato dal cluster hello. Selezionare un account di archiviazione di Azure nuovo o esistente oppure un account di archiviazione di Data Lake esistente.

    - Se si seleziona un account di archiviazione di Azure, è selezionato un account di archiviazione esistente scegliendo **selezionare un account di archiviazione** e quindi selezionando conto hello. Creare un nuovo account tramite hello **Crea nuovo** collegamento hello **selezionare un account di archiviazione** sezione.

      > [!NOTE]
      > Se si seleziona **New** è necessario immettere un nome per il nuovo account di archiviazione hello. Se il nome di hello è accettato, viene visualizzato un segno di spunta verde.

      Hello **contenitore predefinito** nome toohello impostazioni predefinite del cluster di hello. Lasciare l'impostazione predefinita come valore di hello.

      Se una nuova opzione di account di archiviazione è stata selezionata un prompt dei comandi tooselect **percorso** è specificato tooselect toocreate quale area hello account di archiviazione.  

         ![Pannello di origine dati](./media/hdinsight-getting-started-with-r/datastore.png)  

      > [!IMPORTANT]
      > Selezionando il percorso di hello per l'origine dei dati predefinita hello imposta anche percorso hello del cluster HDInsight hello. Hello predefinito e cluster di origine dati deve essere in hello stessa area.

    - Se si desidera toouse un archivio Data Lake esistente, quindi selezionare hello toouse account di archiviazione ADLS e aggiungere il cluster hello *Aggiungi* archivio identità di tooyour cluster tooallow accesso toohello. Per altre informazioni su questo processo, vedere [Creare cluster HDInsight con Data Lake Store tramite il portale di Azure](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).

    Hello utilizzare **selezionare** configurazione dell'origine dati hello toosave pulsante.


7. Hello **riepilogo** pannello visualizza quindi toovalidate tutte le impostazioni. Qui è possibile modificare il **dimensioni del Cluster** toomodify hello numero di server nel cluster e specificare le **Script azioni** desiderato toorun. A meno che non si conosce la necessità di un cluster di dimensioni maggiore, lasciare il numero di hello di nodi di lavoro predefinito hello `4`. Hello stimato costo del cluster hello viene visualizzato all'interno di blade hello.

    ![riepilogo cluster](./media/hdinsight-hadoop-r-server-get-started/clustersummary.png)

   > [!NOTE]
   > Se necessario, è possibile ridimensionare il cluster in un secondo momento tramite hello portale (**Cluster** -> **impostazioni** -> **scala Cluster**) tooincrease o ridurre il numero di hello di nodi di lavoro.  Il ridimensionamento può essere utile per minimo verso il basso cluster hello quando non è in uso o per l'aggiunta di dimensionamento hello toomeet attività più grandi.
   >
   >

   Tookeep alcuni fattori presente quando il cluster, nodi dati hello e nodo di hello del bordo di ridimensionamento sono:  

   * prestazioni Hello di analisi di R Server distribuite in Spark sono proporzionale toohello numero di nodi di lavoro se dati hello sono grandi.  

   * prestazioni Hello di analisi di R Server sono lineare nella dimensione di hello dei dati da analizzare. ad esempio:  

     * Per i dati di piccole toomodest, delle prestazioni sono consigliabile quando analizzato in un contesto di calcolo locale nel nodo edge hello.  Per altre informazioni sugli scenari di hello in cui hello locale e Spark contesti di calcolo funzionano meglio, vedere le opzioni di contesto di calcolo per il Server di R in HDInsight.<br>
     * Se si accedere nodo edge toohello ed esegue lo script R, quindi vengono eseguiti tutti ma hello rx-funzioni ScaleR <strong>localmente</strong> nel nodo edge hello. Pertanto hello memoria e numero di core del nodo perimetrale hello deve essere ridimensionata di conseguenza. Hello che ciò vale anche se si utilizza Server R come contesto di calcolo remoto HDI dal portatile.

     ![Pannello livelli dei prezzi di nodo](./media/hdinsight-hadoop-r-server-get-started/pricingtier.png)

     Hello utilizzare **selezionare** nodo hello del pulsante toosave dei prezzi di configurazione.

   È presente anche un collegamento **Scarica modello e parametri**. Fare clic su questo script toodisplay collegamento che possono essere utilizzati tooautomate hello creazione di un cluster con configurazione selezionata hello. Questi script sono disponibili da hello voce portale Azure per il cluster anche dopo che è stato creato.

   > [!NOTE]
   > Comporta un tempo per hello cluster toobe creato, in genere circa 20 minuti. Utilizzare il riquadro hello su hello schermata iniziale oppure hello **notifiche** voce hello a sinistra della hello pagina toocheck nel processo di creazione hello.
   >
   >

<a name="connect-to-rstudio-server"></a>
## <a name="connect-toorstudio-server"></a>Connettersi tooRStudio Server

Se si è scelto tooinclude edizione community RStudio Server dell'installazione, è possibile accedere accesso RStudio hello tramite due metodi diversi.

1. Passare toohello URL seguente (dove **CLUSTERNAME** hello nome del cluster di hello creato):

    https://**CLUSTERNAME**.azurehdinsight.net/rstudio/

2. Aprire la voce hello per il cluster in hello portale di Azure seleziona hello **R Server dashboard** collegamento rapido e quindi selezionando hello **R Studio Dashboard**:

     ![Dashboard di accesso hello R studio](./media/hdinsight-getting-started-with-r/rstudiodashboard1.png)

     ![Dashboard di accesso hello R studio](./media/hdinsight-getting-started-with-r/rstudiodashboard2.png)

   > [!IMPORTANT]
   > Indipendentemente dal metodo hello utilizzato, hello primo tentativo di accesso è necessario tooauthenticate due volte.  Fornire l'autenticazione prima di hello, hello *ID utente di amministrazione del cluster* e *password*. Al prompt dei comandi secondo hello fornire hello *SSH userid* e *password*. Log successivi aggiuntivi richiedono solo hello *password SSH* e *userid*.

<a name="connect-to-edge-node"></a>
## <a name="connect-toohello-r-server-edge-node"></a>Connettere toohello R Server edge nodo

Connettersi tooR nodo del lato Server del cluster HDInsight hello tramite SSH con il comando hello:

   `ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`

> [!NOTE]
> È possibile trovare hello `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` indirizzo nel portale di Azure selezionando il cluster, quindi hello **tutte le impostazioni** -> **app** -> **RServer**. Consente di visualizzare informazioni sull'Endpoint SSH per il nodo di edge hello hello.
>
> ![Immagine di hello SSH Endpoint per il nodo di edge hello](./media/hdinsight-hadoop-r-server-get-started/sshendpoint.png)
>
>

Se si utilizza un toosecure password account utente SSH, si è tooenter richiesto è. Se si utilizza una chiave pubblica, è possibile hello toouse `-i` toospecify parametro hello chiave privata corrispondente. ad esempio:

    ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

Per ulteriori informazioni, vedere [connettersi tooHDInsight (Hadoop) tramite SSH](hdinsight-hadoop-linux-use-ssh-unix.md).

Una volta connessi, verrà visualizzato un prompt dei comandi seguenti toohello simile:

    sername@ed00-myrser:~$

<a name="enable-concurrent-users"></a>
## <a name="enable-multiple-concurrent-users"></a>Abilitare più utenti simultanei

L'aggiunta di più utenti per il nodo di edge hello in cui hello community RStudio viene eseguita la versione, è possibile abilitare più utenti simultanei.

Quando si crea un cluster HDInsight, è necessario specificare due utenti: un utente HTTP e un utente SSH.

![Utenti simultanei 1](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-1.png)

- **Nome utente account di accesso del cluster**: un utente HTTP per l'autenticazione tramite gateway HDInsight hello che viene utilizzato tooprotect hello HDInsight cluster creato. Questo utente HTTP è utilizzato tooaccess hello Ambari UI, interfaccia utente di YARN, nonché altri componenti dell'interfaccia utente.
- **Nome utente della Shell (SSH) protetta**: un cluster di hello tooaccess utente SSH tramite shell protetta. Questo utente è un utente nel sistema Linux per tutti i nodi head hello, nodi di lavoro e i nodi periferici hello. È possibile utilizzare shell protetta tooaccess uno qualsiasi dei nodi hello in un cluster remoto.

versione di R Studio Server Community Hello utilizzata in hello Microsoft R Server nel cluster di HDInsight tipo accetta solo nome utente di Linux e la password come un meccanismo di accesso. Non supporta il passaggio di token. Pertanto, se è stato creato un nuovo cluster e si desidera toouse R Studio tooaccess, è necessario toolog in due volte.

- Primo accesso con le credenziali utente hello HTTP tramite hello HDInsight Gateway: 

    ![Utenti simultanei 2a](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2a.png)

- Utilizzare quindi hello SSH utente credenziali toolog in tooRStudio:
  
    ![Utenti simultanei 2b](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2b.png)

Attualmente, durante il provisioning di un cluster HDInsight è possibile creare un solo account utente SSH. In modo tooenable cluster più utenti tooaccess Microsoft R Server in HDInsight, è necessario toocreate altri utenti nel sistema Linux hello.

Poiché RStudio Server Community è in esecuzione sul nodo del bordo del cluster di hello, vi sono alcuni passaggi di seguito:

1. Utilizzare hello creato SSH utente toolog nel nodo di edge toohello
2. Aggiungere altri utenti Linux nel nodo perimetrale
3. Utilizzare la versione RStudio Community con utente hello creato

### <a name="step-1-use-hello-created-ssh-user-toolog-in-toohello-edge-node"></a>Passaggio 1: Utilizzare hello creato SSH utente toolog nel nodo di edge toohello

Scaricare uno strumento SSH (ad esempio Putty) e utilizzare hello esistente SSH utente toolog in. Segui hello istruzioni fornite in [connettersi tooHDInsight (Hadoop) tramite SSH](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess hello nodo del bordo. indirizzo del nodo perimetrale Hello per R Server nel cluster HDInsight è: *clustername-ed-ssh.azurehdinsight.net*


### <a name="step-2-add-more-linux-users-in-edge-node"></a>Passaggio 2: Aggiungere altri utenti Linux nel nodo perimetrale

tooadd un nodo di edge toohello utente, eseguire i comandi di hello:

    sudo useradd yournewusername -m
    sudo passwd yourusername

È necessario visualizzare hello elementi restituiti: 

![Utenti simultanei 3](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-3.png)

Quando viene richiesto di "password Kerberos corrente:", è sufficiente premere **invio** tooignore è. Hello `-m` opzione `useradd` comando indica che il sistema hello creerà una home directory utente hello, che è obbligatorio per la versione RStudio Community.


### <a name="step-3-use-rstudio-community-version-with-hello-user-created"></a>Passaggio 3: Versione usare RStudio Community con utente hello creato

Utilizzare hello creati dall'utente toolog tooRStudio:

![Utenti simultanei 4](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-4.png)

Si noti che RStudio indica che si sta utilizzando un nuovo utente hello (qui, ad esempio, *sshuser6*) toolog cluster hello: 

![Utenti simultanei 5](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-5.png)

È anche possibile accedere con credenziali originale hello (per impostazione predefinita è *sshuser*) contemporaneamente da un'altra finestra del browser.

È possibile inviare un processo usando funzioni ScaleR. Ecco un esempio di hello comandi utilizzati toorun un processo:

    # Set hello HDFS (WASB) location of example data.
    bigDataDirRoot <- "/example/data"

    # Create a local folder for storaging data temporarily.
    source <- "/tmp/AirOnTimeCSV2012"
    dir.create(source)

    # Download data toohello tmp folder.
    remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
    download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
    download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
    download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
    download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
    download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
    download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
    download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
    download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
    download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
    download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
    download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
    download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

    # Set directory in bigDataDirRoot tooload hello data.
    inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

    # Create hello directory.
    rxHadoopMakeDir(inputDir)

    # Copy hello data from source tooinput.
    rxHadoopCopyFromLocal(source, bigDataDirRoot)

    # Define hello HDFS (WASB) file system.
    hdfsFS <- RxHdfsFileSystem()

    # Create info list for hello airline data.
    airlineColInfo <- list(
    DAY_OF_WEEK = list(type = "factor"),
    ORIGIN = list(type = "factor"),
    DEST = list(type = "factor"),
    DEP_TIME = list(type = "integer"),
    ARR_DEL15 = list(type = "logical"))

    # Get all hello column names.
    varNames <- names(airlineColInfo)

    # Define hello text data source in HDFS.
    airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

    # Define hello text data source in local system.
    airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

    # Specify hello formula toouse.
    formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

    # Define hello Spark compute context.
    mySparkCluster <- RxSpark()

    # Set hello compute context.
    rxSetComputeContext(mySparkCluster)

    # Run a logistic regression.
    system.time(
        modelSpark <- rxLogit(formula, data = airOnTimeData)
    )

    # Display a summary.
    summary(modelSpark)


Si noti che i processi di hello inviati in diversi nomi utente nell'interfaccia utente di YARN:

![Utenti simultanei 6](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-6.png)

Si noti inoltre che hello appena aggiunti utenti non dispongono di privilegi radice nel sistema di Linux, ma hanno hello stesso di accedere ai file di hello tooall hello HDFS e WASB archiviazione.


<a name="use-r-console"></a>
## <a name="use-hello-r-console"></a>Usare la console di hello R

1. Dalla sessione SSH hello, utilizzare hello console hello R toostart dei comandi seguenti:  

        R

2. Verrà visualizzato il seguente toohello simili di output:
    
    R versione 3.2.2 (2015-08-14): "Incendio" Copyright (C) 2015 hello R Foundation per la piattaforma di elaborazione statistica: x86_64-pc-linux-gnu (64 bit)

    R is free software and comes with ABSOLUTELY NO WARRANTY.
    Si è tooredistribute iniziale in determinate condizioni.
    Type "license()" or "licence()" for distribution details.

    Natural language support but running in an English locale

    R is a collaborative project with many contributors.
    Digitare 'contributors()' per ulteriori informazioni e 'citation()' in modalità toocite R o R pacchetti nelle pubblicazioni.

    Digitare 'demo ()' per alcuni demo, 'help()' per la Guida in linea o 'help.start()' per un toohelp di interfaccia browser HTML.
    Digitare 'OcxQmail' tooquit R.

    Microsoft R Server version 8.0: an enhanced distribution of R  Microsoft packages Copyright (C) 2016 Microsoft Corporation

    Type "readme()" for release notes.
    >

3. Da hello `>` prompt dei comandi, è possibile immettere il codice R. Server R include i pacchetti che consentono di tooeasily interagire con Hadoop ed eseguire calcoli distribuiti. Ad esempio, utilizzare hello comando tooview hello radice hello predefiniti del file system per il cluster HDInsight hello seguenti:

    rxHadoopListFiles("/")

4. È inoltre possibile utilizzare hello WASB stile addressing.

    rxHadoopListFiles("wasb:///")


## <a name="using-r-server-on-hdi-from-a-remote-instance-of-microsoft-r-server-or-microsoft-r-client"></a>Utilizzare R Server in HDI da un'istanza remota di Microsoft R Server o Microsoft R Client

È possibile tooset il contesto di calcolo Hadoop Spark HDI toohello accesso da un'istanza remota di Microsoft R Server o Microsoft R Client in esecuzione in un computer desktop o portatile. Vedere **utilizzando Microsoft R Server come Hadoop Client** sottosezione hello [creazione di un contesto di calcolo per Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md). toodo in tal caso, è necessario hello toospecify le opzioni seguenti quando si definisce il contesto di calcolo di hello RxSpark in un computer portatile: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches e sshProfileScript. ad esempio:


    myNameNode <- "default"
    myPort <- 0

    mySshHostname  <- 'rkrrehdi1-ed-ssh.azurehdinsight.net'  # HDI secure shell hostname
    mySshUsername  <- 'remoteuser'# HDI SSH username
    mySshSwitches  <- '-i /cygdrive/c/Data/R/davec'   # HDI SSH private key

    myhdfsShareDir <- paste("/user/RevoShare", mySshUsername, sep="/")
    myShareDir <- paste("/var/RevoShare" , mySshUsername, sep="/")

    mySparkCluster <- RxSpark(
      hdfsShareDir = myhdfsShareDir,
      shareDir     = myShareDir,
      sshUsername  = mySshUsername,
      sshHostname  = mySshHostname,
      sshSwitches  = mySshSwitches,
      sshProfileScript = '/etc/profile',
      nameNode     = myNameNode,
      port         = myPort,
      consoleOutput= TRUE
    )


## <a name="use-a-compute-context"></a>Usare un contesto di calcolo

Un contesto di calcolo consente toocontrol se calcolo viene eseguito localmente sul nodo del bordo hello o distribuito tra i nodi nel cluster HDInsight hello hello.

1. Dalla console di hello R (in una sessione SSH) o il RStudio Server, utilizzare hello segue i dati di esempio di codice tooload nell'account di archiviazione predefinito hello per HDInsight:

        # Set hello HDFS (WASB) location of example data
        bigDataDirRoot <- "/example/data"

        # create a local folder for storaging data temporarily
        source <- "/tmp/AirOnTimeCSV2012"
        dir.create(source)

        # Download data toohello tmp folder
        remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
        download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
        download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
        download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
        download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
        download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
        download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
        download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
        download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
        download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
        download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
        download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
        download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

        # Set directory in bigDataDirRoot tooload hello data into
        inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

        # Make hello directory
        rxHadoopMakeDir(inputDir)

        # Copy hello data from source tooinput
        rxHadoopCopyFromLocal(source, bigDataDirRoot)

2. Successivamente, si creare alcune informazioni di dati e definire due origini dati in modo che è possibile utilizzare i dati di hello.

        # Define hello HDFS (WASB) file system
        hdfsFS <- RxHdfsFileSystem()

        # Create info list for hello airline data
        airlineColInfo <- list(
             DAY_OF_WEEK = list(type = "factor"),
             ORIGIN = list(type = "factor"),
             DEST = list(type = "factor"),
             DEP_TIME = list(type = "integer"),
             ARR_DEL15 = list(type = "logical"))

        # get all hello column names
        varNames <- names(airlineColInfo)

        # Define hello text data source in hdfs
        airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

        # Define hello text data source in local system
        airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

        # formula toouse
        formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

3. Eseguire una regressione logistica sui dati hello utilizzando il contesto di calcolo locale hello.

        # Set a local compute context
        rxSetComputeContext("local")

        # Run a logistic regression
        system.time(
           modelLocal <- rxLogit(formula, data = airOnTimeDataLocal)
        )

        # Display a summary
        summary(modelLocal)

    È necessario visualizzare l'output che termina con toohello simile di righe seguenti:

        Data: airOnTimeDataLocal (RxTextData Data Source)
        File name: /tmp/AirOnTimeCSV2012
        Dependent variable(s): ARR_DEL15
        Total independent variables: 634 (Including number dropped: 3)
        Number of valid observations: 6005381
        Number of missing observations: 91381
        -2*LogLikelihood: 5143814.1504 (Residual deviance on 6004750 degrees of freedom)

        Coefficients:
                         Estimate Std. Error z value Pr(>|z|)
         (Intercept)   -3.370e+00  1.051e+00  -3.208  0.00134 **
         ORIGIN=JFK     4.549e-01  7.915e-01   0.575  0.56548
         ORIGIN=LAX     5.265e-01  7.915e-01   0.665  0.50590
         ......
         DEST=SHD       5.975e-01  9.371e-01   0.638  0.52377
         DEST=TTN       4.563e-01  9.520e-01   0.479  0.63172
         DEST=LAR      -1.270e+00  7.575e-01  -1.676  0.09364 .
         DEST=BPT         Dropped    Dropped Dropped  Dropped

         ---

         Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

         Condition number of final variance-covariance matrix: 11904202
         Number of iterations: 7

4. Successivamente, eseguire la regressione logistica stesso utilizzando il contesto di Spark hello hello. contesto di Spark Hello distribuisce l'elaborazione di tutti i nodi di lavoro di hello in cluster di HDInsight hello hello.

        # Define hello Spark compute context
        mySparkCluster <- RxSpark()

        # Set hello compute context
        rxSetComputeContext(mySparkCluster)

        # Run a logistic regression
        system.time(  
           modelSpark <- rxLogit(formula, data = airOnTimeData)
        )
        
        # Display a summary
        summary(modelSpark)


   > [!NOTE]
   > È anche possibile utilizzare MapReduce toodistribute calcolo tra nodi del cluster. Per altre informazioni sul contesto di calcolo, vedere [Opzioni del contesto di calcolo per R Server su HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).


## <a name="distribute-r-code-toomultiple-nodes"></a>Distribuire i nodi toomultiple codice R

Con R Server, è possibile eseguire codice R esistente facilmente ed eseguito in più nodi nel cluster hello utilizzando `rxExec`. Questa funzione è utile in caso di sweep di parametri o simulazioni. il codice seguente Hello è riportato un esempio di come toouse `rxExec`:

    rxExec( function() {Sys.info()["nodename"]}, timesToRun = 4 )

Se si utilizza ancora hello Spark o contesto MapReduce, questo comando restituisce il valore di nodename hello per nodi di lavoro hello tale codice hello `(Sys.info()["nodename"])` viene eseguito in. Ad esempio, in un cluster a quattro nodi, si prevede di tooreceive output simili toohello seguenti:

    $rxElem1
        nodename
    "wn3-myrser"

    $rxElem2
        nodename
    "wn0-myrser"

    $rxElem3
        nodename
    "wn3-myrser"

    $rxElem4
        nodename
    "wn3-myrser"


## <a name="accessing-data-in-hive-and-parquet"></a>Accesso ai dati in Hive e Parquet

Una funzionalità disponibile in R Server 9.1 consente l'accesso diretto toodata Hive e Parquet per l'utilizzo per le funzioni ScaleR nel contesto di calcolo di hello Spark. Queste funzionalità sono disponibili tramite i nuovi dati origine le funzioni ScaleR chiamate RxHiveData e RxParquetData che funzionano tramite l'utilizzo di dati di Spark SQL tooload direttamente in un frame di dati di Spark per l'analisi da ScaleR.  

Hello di codice seguente fornisce un codice di esempio sull'utilizzo di nuove funzioni hello:

    #Create a Spark compute context:
    myHadoopCluster <- rxSparkConnect(reset = TRUE)

    #Retrieve some sample data from Hive and run a model:
    hiveData <- RxHiveData("select * from hivesampletable",
                     colInfo = list(devicemake = list(type = "factor")))
    rxGetInfo(hiveData, getVarInfo = TRUE)

    rxLinMod(querydwelltime ~ devicemake, data=hiveData)

    #Retrieve some sample data from Parquet and run a model:
    rxHadoopMakeDir('/share')
    rxHadoopCopyFromLocal(file.path(rxGetOption('sampleDataDir'), 'claimsParquet/'), '/share/')
    pqData <- RxParquetData('/share/claimsParquet',
                     colInfo = list(
                age    = list(type = "factor"),
               car.age = list(type = "factor"),
                  type = list(type = "factor")
             ) )
    rxGetInfo(pqData, getVarInfo = TRUE)

    rxNaiveBayes(type ~ age + cost, data = pqData)

    #Check on Spark data objects, cleanup, and close hello Spark session:
    lsObj <- rxSparkListData() # two data objs are cached
    lsObj
    rxSparkRemoveData(lsObj)
    rxSparkListData() # it should show empty list
    rxSparkDisconnect(myHadoopCluster)


Per altre informazioni sull'utilizzo di queste nuove funzioni, vedere la Guida online hello in R Server tramite l'utilizzo di hello `?RxHivedata` e `?RxParquetData` comandi.  


## <a name="install-additional-r-packages-on-hello-edge-node"></a>Installare pacchetti R aggiuntivi nel nodo del bordo hello

Se si desidera tooinstall pacchetti R aggiuntivi nel nodo di hello edge, è possibile utilizzare `install.packages()` direttamente dall'interno hello console R quando connesso toohello bordo nodo tramite SSH. Tuttavia, se è necessario pacchetti R tooinstall in nodi di lavoro di hello di hello cluster, è necessario utilizzare un'azione di Script.

Le azioni script sono gli script Bash toomake utilizzato configurazione modifiche toohello HDInsight cluster o tooinstall software aggiuntivo, ad esempio pacchetti R aggiuntivi. tooinstall pacchetti aggiuntivi con un'azione di Script, utilizzare hello alla procedura seguente:

> [!IMPORTANT]
> Utilizzo di pacchetti R aggiuntivi di azioni Script tooinstall sono utilizzabili solo dopo aver creato il cluster hello. Non utilizzare questa procedura durante la creazione del cluster come script hello si basa su R Server viene completamente installato e configurato.
>
>

1. Da hello [portale di Azure](https://portal.azure.com), selezionare il Server di R nel cluster HDInsight.

2. Da hello **impostazioni** pannello seleziona **azioni Script** e quindi **inviare nuovi** toosubmit una nuova azione di Script.

   ![Immagine del pannello Azioni script](./media/hdinsight-hadoop-r-server-get-started/scriptaction.png)

3. Da hello **inviare l'azione script** pannello fornire hello le seguenti informazioni:

   * **Nome**: un semplice nome tooidentify questo script

   * **URI script Bash**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`

   * **Head**: questa voce deve essere **deselezionata**

   * **Lavoro**: questa voce deve essere **selezionata**

   * **Nodi perimetrali**: questa voce deve essere **deselezionata**

   * **Zookeeper**: questa voce deve essere **deselezionata**

   * **I parametri**: hello R pacchetti toobe installato. Ad esempio, `bitops stringr arules`

   * **Salvare questa azione script in modo permanente...**: questa voce deve essere **selezionata**  

   > [!NOTE]
   > 1. Per impostazione predefinita, tutti i pacchetti R installati da uno snapshot del repository MRAN Microsoft hello coerente con la versione di hello del Server di R che è stato installato. Se si desidera tooinstall le versioni più recenti dei pacchetti, vi è rischio di incompatibilità. Tuttavia questo tipo di installazione è possibile specificando `useCRAN` come hello elencare primo elemento del pacchetto di hello, ad esempio `useCRAN bitops, stringr, arules`.  
   > 2. Alcuni pacchetti R richiedono librerie di sistema di Linux aggiuntive. Per praticità, è stato preinstallato dipendenze hello necessarie hello primi 100 pacchetti R più diffusi. Tuttavia, se si installa i pacchetti R di hello richiedono librerie oltre a questi quindi è necessario scaricare script di base hello utilizzato in questo argomento e aggiungere passaggi tooinstall hello sistema librerie. È necessario quindi pubblica tooa script hello modificato di caricamento blob contenitore nell'archiviazione di Azure e utilizzare i pacchetti hello modificato script tooinstall hello.
   >    Per altre informazioni sullo sviluppo di azioni script, vedere l'articolo [Sviluppo di azioni script con HDInsight](hdinsight-hadoop-script-actions-linux.md).  
   >
   >

   ![Aggiunta di un'azione script](./media/hdinsight-getting-started-with-r/submitscriptaction.png)

4. Selezionare **crea** script hello toorun. Al termine dell'esecuzione dello script hello, i pacchetti hello R sono disponibili in tutti i nodi di lavoro.


## <a name="using-microsoft-r-server-operationalization"></a>Uso della messa in funzione di Microsoft R Server

Una volta completata la modellazione dei dati, è possibile rendere operative le stime di toomake modello hello. tooconfigure per rendere operativo Microsoft R Server, eseguire hello alla procedura seguente:

Prima di tutto, ssh nel nodo di hello del bordo. Ad esempio, 

    ssh -L USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

Dopo l'utilizzo di ssh, cambiare directory per la versione appropriata di hello e sudo hello dotnet dll: 

- Per Microsoft R Server 9.1:

    cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0 sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll

- Per Microsoft R Server 9.0:

    cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll

rendere operativo Microsoft R Server tooconfigure con una configurazione di una casella hello seguenti:

1. Selezionare "Configure R Server for Operationalization" (Configurare R Server per la messa in funzione)
2. Selezionare "A. One-box (web + compute nodes)” (Una casella (Web + nodi di calcolo)"
3. Immettere una password per hello **admin** utente

![Opzione per una casella](./media/hdinsight-hadoop-r-server-get-started/admin-util-one-box-.png)

Come passaggio facoltativo, è possibile eseguire controlli diagnostici eseguendo un test di diagnostica, come illustrato di seguito:

1. Selezionare "6. Run diagnostic tests" (Esegui test diagnostici)
2. Selezionare "A. Test configuration" (Configurazione test)
3. Immettere nome utente = "admin" e la password del passaggio di configurazione precedente
4. Conferma dell'integrità complessiva = pass
5. Utilità di amministrazione di hello uscita
6. Uscire da SSH

![Diagnostica per la messa in funzione](./media/hdinsight-hadoop-r-server-get-started/admin-util-diagnostics.png)


>[!NOTE]
>**Ritardi considerevoli quando si utilizza il servizio Web in Spark**
>
>Se si verificano ritardi quando si tenta di tooconsume un servizio web creato con mrsdeploy funzioni in un contesto di calcolo Spark, potrebbe essere necessario tooadd alcune cartelle mancanti. applicazione di Spark Hello appartiene tooa utente denominato '*rserve2*' ogni volta che viene chiamato da un servizio web utilizzando le funzioni mrsdeploy. toowork questo problema:

    # Create these required folders for user 'rserve2' in local and hdfs:

    hadoop fs -mkdir /user/RevoShare/rserve2
    hadoop fs -chmod 777 /user/RevoShare/rserve2

    mkdir /var/RevoShare/rserve2
    chmod 777 /var/RevoShare/rserve2


    # Next, create a new Spark compute context:
 
    rxSparkConnect(reset = TRUE)


In questa fase, configurazione hello per rendere operativo è stata completata. È ora possibile usare hello 'mrsdeploy' pacchetto sul toohello di tooconnect RClient rendere operativo il nel nodo del bordo e iniziare a usare le funzionalità come [esecuzione remota](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) e [servizi web](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette). A seconda se il cluster è installato in una rete virtuale o non, potrebbe essere necessario tooset backup Porta avanti tunneling tramite account di accesso SSH. Hello sezioni seguenti illustrano come tooset backup questo tunnel.

### <a name="rserver-cluster-on-virtual-network"></a>Cluster RServer su rete virtuale

Assicurarsi che consentire il traffico attraverso il nodo 12800 toohello bordo porta. In questo modo, è possibile utilizzare funzionalità di hello edge nodi tooconnect toohello rendere operativo.


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://[your-cluster-name]-ed-ssh.azurehdinsight.net:12800",
        username = "admin",
        password = "xxxxxxx"
    )


Se hello `remoteLogin()` non è possibile connettere toohello bordo nodo, ma è possibile nodo del bordo di toohello SSH, quindi è necessario tooverify se traffico sulla porta 12800 tooallow regole di hello è stato impostato correttamente o meno. Se si continua, il problema di hello tooface, è possibile aggirare il mediante l'impostazione di porta Avanti tunneling tramite SSH. Per istruzioni, vedere hello seguente sezione.

### <a name="rserver-cluster-not-set-up-on-virtual-network"></a>Cluster RServer non impostato su rete virtuale

Se il cluster non è configurato sulla rete virtuale o si riscontrano problemi relativi alla connettività tramite la rete virtuale, è possibile usare il tunneling di port forwarding SSH:

    ssh -L localhost:12800:localhost:12800 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

La configurazione è possibile anche in Putty.

![Connessione SSH con Putty](./media/hdinsight-hadoop-r-server-get-started/putty.png)

Una volta la sessione SSH è attiva, il traffico di hello dalla porta del computer 12800 verrà inoltrato porta del nodo perimetrale toohello 12800 tramite una sessione SSH. Assicurarsi di usare `127.0.0.1:12800` nel metodo `remoteLogin()`. Questo accesso rendere operativo il del nodo perimetrale toohello tramite inoltro alla porta.


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://127.0.0.1:12800",
        username = "admin",
        password = "xxxxxxx"
    )


## <a name="how-tooscale-microsoft-r-server-operationalization-compute-nodes-on-hdinsight-worker-nodes"></a>Come nodi in HDInsight i nodi di lavoro di calcolo tooscale rendere operativo il Microsoft R Server

### <a name="decommission-hello-worker-nodes"></a>Rimuovere le autorizzazioni ai nodi di lavoro hello

Attualmente Microsoft R Server non è gestito tramite Yarn. Se i nodi di lavoro hello non vengono rimossi, hello Gestione risorse di Yarn non funzionerà come previsto perché non sarà compatibile con risorse hello utilizzata dal server hello. In ordine tooavoid questa situazione, si consiglia di rimozione di nodi di lavoro hello prima la scalabilità orizzontale nodi di calcolo hello.

Nodi di lavoro toodecommissioning passaggi:

* Accedere alla console Ambari tooHDI del cluster e fare clic sulla scheda "host"
* Selezionare i nodi di lavoro (toobe messo fuori servizio), fare clic sul menu "azioni" > "Selezionato gli host" > "Hosts" > fare clic su "Attivare la modalità di manutenzione ON". Ad esempio, nella seguente immagine hello è stato selezionato toodecommission wn3 e wn4.  

   ![Rimozione delle autorizzazioni dei nodi del ruolo di lavoro](./media/hdinsight-hadoop-r-server-get-started/get-started-operationalization.png)  

* Selezionare **Actions** > **Selected Hosts** > **DataNodes** > fare clic su **Decommission** (Rimuovi autorizzazioni).
* Selezionare **Actions** > **Selected Hosts** > **NodeManagers** > fare clic su **Decommission** (Rimuovi autorizzazioni).
* Selezionare **Actions** > **Selected Hosts** > **DataNodes** > fare clic su **Stop** (Arresta).
* Selezionare **Actions** > **Selected Hosts** > **NodeManagers** > fare clic su **Stop** (Arresta).
* Selezionare **Actions** > **Selected Hosts** > **Hosts** > fare clic su **Stop All Components** (Arresta tutti i componenti).
* Deselezionare i nodi di lavoro hello e selezionare i nodi head hello
* Selezionare **Actions** > **Selected Hosts** > "**Hosts** > **Restart All Components** (Riavvia tutti i componenti).

### <a name="configure-compute-nodes-on-each-decommissioned-worker-nodes"></a>Configurare i nodi di calcolo su ogni nodo del ruolo di lavoro per il quale è stata rimossa l'autorizzazione

1. Accedere tramite SSH a ogni nodo del ruolo di lavoro per il quale è stata rimossa l'autorizzazione.
2. Eseguire l'utilità di amministrazione con `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.
3. Immettere "1" l'opzione tooselect "Configurare R Server per rendere operativo il".
4. Immettere l'opzione tooselect "c" "c. Compute node" (Nodo di calcolo). Consente di configurare il nodo di calcolo hello nel nodo lavoro hello.
5. Hello uscita utilità di amministrazione.

### <a name="add-compute-nodes-details-on-web-node"></a>Aggiungere i dettagli dei nodi di calcolo nel nodo Web

Dopo aver configurati tutti i nodi di lavoro rimossi toorun nodo di calcolo, tornare nel nodo edge hello e aggiungere gli indirizzi IP dei nodi di lavoro rimossi in configurazione del nodo di hello Microsoft R Server web:

* SSH nel nodo di hello del bordo.
* Eseguire `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.
* Cercare la sezione "URI" hello e aggiungere l'indirizzo IP del nodo di lavoro e dettagli della porta.

    ![Rimozione delle autorizzazioni dei nodi del ruolo di lavoro con la riga di comando](./media/hdinsight-hadoop-r-server-get-started/get-started-op-cmd.png)


## <a name="troubleshoot"></a>Risoluzione dei problemi

Se si verificano problemi di creazione dei cluster HDInsight, vedere i [requisiti dei controlli di accesso](hdinsight-administer-use-portal-linux.md#create-clusters).


## <a name="next-steps"></a>Passaggi successivi

A questo punto è necessario comprendere come un nuovo cluster HDInsight che include hello R Server hello concetti di base e dell'utilizzo toocreate hello console R da una sessione SSH. Hello seguenti argomenti vengono illustrati altri modi di gestione e utilizzo del Server di R in HDInsight:

* [Aggiungere RStudio Server tooHDInsight (se non è installato durante la creazione del cluster)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Opzioni del contesto di calcolo per R Server su HDInsight (anteprima)](hdinsight-hadoop-r-server-compute-contexts.md)
* [Opzioni di Archiviazione di Azure per R Server su HDInsight](hdinsight-hadoop-r-server-storage.md)
