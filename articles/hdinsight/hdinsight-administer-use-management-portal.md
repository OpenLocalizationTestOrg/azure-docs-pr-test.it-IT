---
title: i cluster Hadoop basato su Windows aaaManage HDInsight con hello portale di Azure | Documenti Microsoft
description: Informazioni su come tooadminister HDInsight Service. Creare un cluster HDInsight, console JavaScript interattiva aprire hello e console dei comandi aprire hello Hadoop.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 9295a988-bd88-453a-8c8b-55fa103bf39c
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: a237726b0e37a08005ce22e96581739e93edb050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-windows-based-hadoop-clusters-in-hdinsight-by-using-hello-azure-portal"></a>Gestire i cluster basati su Windows Hadoop in HDInsight mediante hello portale di Azure

Utilizzo di hello [portale di Azure][azure-portal], è possibile creare cluster basati su Windows Hadoop in HDInsight di Azure, cambiare la password utente di Hadoop e abilitare Remote Desktop Protocol (RDP), pertanto è possibile accedere hello Hadoop console dei comandi nel cluster hello.

informazioni di Hello in questo articolo si applicano solo i cluster HDInsight basati su tooWindow. Per informazioni sulla gestione dei cluster basati su Linux, vedere [hello di cluster di gestire Hadoop in HDInsight mediante il portale di Azure](hdinsight-administer-use-portal-linux.md).

> [!IMPORTANT]
> Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).


## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare questo articolo, è necessario disporre delle seguenti hello:

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di prova gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Account di archiviazione Azure** -HDInsight un cluster utilizza un contenitore di archiviazione Blob di Azure come file system predefinito hello. Per altre informazioni sull'esperienza lineare offerta dall'archivio BLOB con cluster HDInsight, vedere [Usare l'archivio BLOB di Azure con HDInsight](hdinsight-hadoop-use-blob-storage.md). Per informazioni dettagliate sulla creazione di un account di archiviazione di Azure, vedere [come un Account di archiviazione tooCreate](../storage/common/storage-create-storage-account.md).

## <a name="open-hello-portal"></a>Aprire hello portale
1. Accedi troppo[https://portal.azure.com](https://portal.azure.com).
2. Dopo aver aperto il portale di hello, è possibile:

   * Fare clic su **New** dal menu a sinistra di hello toocreate un nuovo cluster:

       ![Pulsante Nuovo cluster HDInsight](./media/hdinsight-administer-use-management-portal/azure-portal-new-button.png)
   * Fare clic su **cluster HDInsight** dal menu a sinistra di hello.

       ![Pulsante Cluster HDInsight del portale di Azure](./media/hdinsight-administer-use-management-portal/azure-portal-hdinsight-button.png)

     Se **HDInsight** non vengono visualizzati nel menu a sinistra di hello, fare clic su **Sfoglia**.

     ![Pulsante Sfoglia del portale di Azure](./media/hdinsight-administer-use-management-portal/azure-portal-browse-button.png)

## <a name="create-clusters"></a>Creare i cluster
Per istruzioni di creazione hello utilizzando hello portale, vedere [cluster HDInsight creare](hdinsight-hadoop-provision-linux-clusters.md).

HDInsight è compatibile con una vasta gamma di componenti Hadoop. Per hello l'elenco dei componenti di hello che sono stati verificati e supportati, vedere [è la versione di Hadoop in HDInsight di Azure](hdinsight-component-versioning.md). È possibile personalizzare HDInsight tramite una delle seguenti opzioni hello:

* Utilizzare genera Script azione toorun gli script personalizzati che è possono personalizzare un cluster di tooeither modificare la configurazione del cluster o installare i componenti personalizzati, ad esempio Giraph o Solr. Per altre informazioni, vedere [Personalizzare cluster HDInsight mediante le azioni script](hdinsight-hadoop-customize-cluster.md).
* Utilizzare parametri di personalizzazione hello cluster HDInsight .NET SDK hello o Azure PowerShell durante la creazione del cluster. Queste modifiche alla configurazione, quindi vengono mantenute per tutta la durata hello del cluster hello e non sono interessati da reimages nodo cluster che esegue periodicamente il piattaforma Azure per la manutenzione. Per ulteriori informazioni sull'utilizzo dei parametri di personalizzazione di hello cluster, vedere [cluster HDInsight creare](hdinsight-hadoop-provision-linux-clusters.md).
* Alcuni componenti di Java native, ad esempio Mahout e a catena, possono essere eseguiti nel cluster hello come file JAR. I file JAR possono essere distribuita tooAzure nell'archiviazione Blob e inviate tooHDInsight cluster tramite meccanismi di invio processi Hadoop. Per altre informazioni, vedere [Inviare processi Hadoop a livello di codice](hdinsight-submit-hadoop-jobs-programmatically.md).

  > [!NOTE]
  > Se si presentano problemi di distribuzione di cluster di tooHDInsight file JAR o chiamata file JAR nel cluster HDInsight, contattare [supporto Microsoft](https://azure.microsoft.com/support/options/).
  >
  > Cascading non è supportato da HDInsight, pertanto in caso di problemi non è possibile rivolgersi al Supporto Microsoft. Per gli elenchi di componenti supportati, vedere [novità introdotta nelle versioni di cluster hello fornite da HDInsight](hdinsight-component-versioning.md).
  >
  >

Installazione di software personalizzati nel cluster hello mediante connessione Desktop remoto non è supportata. È consigliabile evitare l'archiviazione di file nelle unità di hello del nodo head hello, come verranno perse se è necessario toore-creare cluster hello. È consigliabile archiviare i file nell'archivio BLOB di Azure. L'archivio BLOB è persistente.

## <a name="list-and-show-clusters"></a>Elencare e visualizzare i cluster
1. Accedi troppo[https://portal.azure.com](https://portal.azure.com).
2. Fare clic su **cluster HDInsight** dal menu a sinistra di hello.
3. Fare clic su nome cluster hello. Se l'elenco di cluster hello è lungo, è possibile utilizzare filtri nella parte superiore di hello della pagina hello.
4. Fare doppio clic su un cluster da hello elencare tooshow hello i dettagli.

    **Menu e informazioni di base**:

    ![Informazioni di base sul cluster HDInsight del Portale di Azure](./media/hdinsight-administer-use-management-portal/hdinsight-essentials.png)

   * menu di hello toocustomize, fare clic sul menu hello e quindi fare clic su **Personalizza**.
   * **Impostazioni** e **tutte le impostazioni**: hello Visualizza **impostazioni** pannello per cluster hello, che consente di tooaccess dettagliate informazioni di configurazione per il cluster hello.
   * **Dashboard**, **Dashboard Cluster** e **URL: si tratta di tutti i metodi tooaccess hello dashboard del cluster, ovvero Ambari Web per i cluster basati su Linux. -**Sicuro Shell * *: Mostra i cluster di hello istruzioni tooconnect toohello utilizzando una connessione Secure Shell (SSH).
   * **Applicare la scalabilità del Cluster**: consente di numero hello toochange di nodi di lavoro per questo cluster.
   * **Eliminare**: cluster hello di eliminazione.
   * **Avvio rapido**: visualizza le informazioni che consentiranno di iniziare a usare HDInsight.
   * * * Utenti: Consente le autorizzazioni tooset per *Gestione portale* del cluster per altri utenti nella sottoscrizione di Azure.

     > [!IMPORTANT]
     > Questo *solo* influisce sull'accesso e autorizzazioni cluster toothis nel portale di Azure hello e non ha alcun effetto su quali utenti possono connettersi il cluster HDInsight toohello di tooor invia i processi.
     >
     >
   * **Tag**: tag consentono di tooset chiave/valore coppie toodefine una tassonomia personalizzata dei servizi cloud. Ad esempio, è possibile creare una chiave denominata **progetto**e usare un valore comune per tutti i servizi associati a un progetto specifico.
   * **Viste Ambari**: collegamenti tooAmbari Web.

     > [!IMPORTANT]
     > servizi di hello toomanage fornito da hello cluster HDInsight, è necessario utilizzare Ambari Web o hello Ambari REST API. Per altre informazioni sull'uso di Ambari, vedere [Gestire i cluster HDInsight tramite Ambari](hdinsight-hadoop-manage-ambari.md).
     >
     >

     **Utilizzo**:

     ![Utilizzo dei cluster HDInsight del portale di Azure](./media/hdinsight-administer-use-management-portal/hdinsight-portal-cluster-usage.png)
5. Fare clic su **Impostazioni**.

    ![Utilizzo dei cluster HDInsight del portale di Azure](./media/hdinsight-administer-use-management-portal/hdinsight.portal.cluster.settings.png)

   * **Proprietà**: consente di visualizzare le proprietà del cluster hello.
   * **Identità AAD cluster**:
   * **Le chiavi di archiviazione Azure**: visualizzare l'account di archiviazione predefinito hello e la relativa chiave. account di archiviazione Hello è configurazione durante il processo di creazione di cluster hello.
   * **Account di accesso del cluster**: modificare nome utente di hello cluster HTTP e la password.
   * **I Metastore esterni**: visualizzare Metastore Hive e Oozie hello. i Metastore Hello possono essere configurati solo durante il processo di creazione di cluster hello.
   * **Applicare la scalabilità del Cluster**: aumento e riduzione hello numero di nodi di lavoro del cluster.
   * **Desktop remoto**: abilitare e disabilitare l'accesso desktop remoto (RDP) e configurare il nome utente RDP hello.  il nome utente RDP Hello deve essere diverso dal nome utente di hello HTTP.
   * **Partner of Record**:

     > [!NOTE]
     > Si tratta di un elenco generico di impostazioni disponibili, non tutte saranno presenti per tutti i tipi di cluster.
     >
     >
6. Fare clic su **Proprietà**:

    sezione relativa alle proprietà Hello Elenca seguente hello:

   * **Nome host**: nome del cluster.
   * **URL cluster**.
   * **Stato**: include Aborted, Accepted, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, Operational, Running, Error, Deleting, Deleted, Timedout, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization
   * **Area**: località di Azure. Per un elenco delle posizioni di Azure supportate, vedere hello **area** casella di riepilogo a discesa in [prezzi di HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).
   * **Data di creazione**.
   * **Sistema operativo**: **Windows** o **Linux**.
   * **Tipo**: Hadoop, HBase, Storm, Spark.
   * **Versione**. Vedere [Versioni di HDInsight](hdinsight-component-versioning.md)
   * **Sottoscrizione**: nome della sottoscrizione.
   * **ID sottoscrizione**.
   * **Origine dati primaria**. account di archiviazione Blob di Azure Hello usato come file system Hadoop di hello predefinito.
   * **Piano tariffario nodi del ruolo di lavoro**.
   * **Piano tariffario per il nodo head**.

## <a name="delete-clusters"></a>Eliminare cluster
Un cluster non eliminerà gli account di archiviazione collegato o di account di archiviazione predefinito hello. È possibile ricreare il cluster hello utilizzando hello stessi account di archiviazione e hello Metastore stesso.

1. Accedi toohello [portale][azure-portal].
2. Fare clic su **Esplora tutto** hello a sinistra fare clic su **cluster HDInsight**, fare clic sul nome del cluster.
3. Fare clic su **eliminare** dal menu superiore hello e quindi seguire le istruzioni di hello.

Vedere anche [Sospendere/Arrestare i cluster](#pauseshut-down-clusters).

## <a name="scale-clusters"></a>Ridimensionare i cluster
scalabilità funzionalità cluster di Hello consente numero hello toochange di nodi di lavoro utilizzato da un cluster che è in esecuzione in Azure HDInsight senza toore-creare cluster hello.

> [!NOTE]
> Sono supportati solo i cluster con HDInsight versione 3.1.3 o successive. Se si è certi della versione di hello del cluster, è possibile controllare una pagina delle proprietà hello.  Vedere [Elencare e visualizzare i cluster](#list-and-show-clusters).
>
>

impatto di Hello di modifica del numero di hello di nodi di dati per ogni tipo di cluster supportato da HDInsight:

* Hadoop

    È possibile aumentare facilmente numero hello di nodi di lavoro in un cluster Hadoop che è in esecuzione senza conseguenze per tutti i processi in sospeso o in esecuzione. È inoltre possibile avviare nuovi processi mentre è in corso hello operazione. Gli errori in un'operazione di ridimensionamento normalmente vengono gestiti in modo che hello cluster rimanga sempre in uno stato funzionale.

    Quando un cluster Hadoop è ridotta, riducendo il numero di hello di nodi di dati, alcuni dei servizi di hello cluster hello vengono riavviati. In questo modo tutti in esecuzione e in sospeso toofail processi al completamento di hello di hello l'operazione di ridimensionamento. È tuttavia possibile inviare di nuovo i processi di hello al termine dell'operazione di hello.
* HBase

    Senza problemi, è possibile aggiungere o rimuovere cluster HBase di nodi tooyour mentre è in esecuzione. Server locali sono bilanciati automaticamente entro pochi minuti di completare l'operazione di ridimensionamento hello. Tuttavia, è possibile bilanciare manualmente server regionali hello accedendo al nodo head hello del cluster e in esecuzione hello seguendo i comandi da una finestra del prompt dei comandi:

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer

    Per ulteriori informazioni sull'utilizzo della shell di HBase hello, vedere]
* Storm

    Senza problemi, è possibile aggiungere o rimuovere cluster Storm tooyour nodi di dati in fase di esecuzione. Tuttavia, dopo il completamento dell'operazione di ridimensionamento hello, sarà necessario topologia hello toorebalance.

    A tale scopo, è possibile scegliere tra due opzioni:

  * Interfaccia utente Web di Storm
  * Interfaccia della riga di comando (CLI)

    Consultare toohello [documentazione di Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) per altri dettagli.

    interfaccia utente web di Storm Hello è disponibile nel cluster HDInsight hello:

    ![Ribilanciamento scala di HDInsight Storm](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)

    Di seguito è riportato un esempio come toouse hello CLI comando topologia di Storm toorebalance hello:

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

**cluster tooscale**

1. Accedi toohello [portale][azure-portal].
2. Fare clic su **Esplora tutto** hello a sinistra fare clic su **cluster HDInsight**, fare clic sul nome del cluster.
3. Fare clic su **impostazioni** dal menu superiore hello e quindi fare clic su **Cluster scala**.
4. Immettere il **numero di nodi del ruolo di lavoro**. limite Hello hello numero del nodo del cluster varia tra le sottoscrizioni di Azure. È possibile contattare fatturazione limite hello tooincrease di supporto.  informazioni sui costi di Hello rifletterà hello apportate toohello numero di nodi.

    ![Ridimensionamento HDInsight Hadoop HBase Storm Spark](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

## <a name="pauseshut-down-clusters"></a>Sospendere/Arrestare i cluster
La maggior parte dei processi Hadoop sono processi batch che vengono eseguito solo occasionalmente. Per la maggior parte dei cluster Hadoop, esistono grandi periodi di tempo tale cluster hello non utilizzato per l'elaborazione. Con HDInsight, i dati vengono archiviati in Archiviazione di Azure ed è possibile eliminare tranquillamente un cluster quando non viene usato.
Vengono addebitati i costi anche per i cluster HDInsight che non sono in uso. Poiché gli addebiti di hello per cluster hello sono spesso più addebiti hello per l'archiviazione, è opportuno economica toodelete cluster quando non sono in uso.

Esistono molti modi, è possibile programmare processo hello:

* Usare Data factory di Azure. Per i servizi collegati di HDInsight su richiesta e autodefiniti, vedere [Servizio collegato Azure HDInsight](../data-factory/data-factory-compute-linked-services.md) e [Trasformare e analizzare tramite Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).
* Usare Azure PowerShell.  Vedere [Analizzare i dati relativi ai ritardi dei voli](hdinsight-analyze-flight-delay-data.md).
* Usare l'interfaccia della riga di comando di Azure. Vedere [Gestire cluster Hadoop in HDInsight tramite l'interfaccia della riga di comando di Azure](hdinsight-administer-use-command-line.md).
* Usare HDInsight .NET SDK. Vedere [Inviare processi di Hadoop](hdinsight-submit-hadoop-jobs-programmatically.md).

Per informazioni sui prezzi di hello, vedere [prezzi di HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/). toodelete un cluster da hello portale, vedere [eliminare cluster](#delete-clusters)

## <a name="change-cluster-username"></a>Modificare il nome utente del cluster
Per un cluster HDInsight possono esistere due account utente. account utente del cluster HDInsight Hello viene creato durante il processo di creazione di hello. È anche possibile creare un account utente RDP per l'accesso a cluster hello tramite RDP. Vedere la sezione relativa all' [abilitazione di Desktop remoto](#connect-to-hdinsight-clusters-by-using-rdp).

**la password e nome utente del cluster HDInsight hello toochange**

1. Accedi toohello [portale][azure-portal].
2. Fare clic su **Esplora tutto** hello a sinistra fare clic su **cluster HDInsight**, fare clic sul nome del cluster.
3. Fare clic su **impostazioni** dal menu superiore hello e quindi fare clic su **accesso Cluster**.
4. Se **accesso Cluster** è stato abilitato, è necessario fare clic su **disabilitare**, quindi fare clic su **abilitare** prima di poter impostare hello username e password...
5. Hello modifica **nome account di accesso Cluster** e/o hello **password dell'account di accesso Cluster**e quindi fare clic su **salvare**.

    ![Modifica di nome utente cluster, password e utente http in HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="grantrevoke-access"></a>Concedere/Revocare l'accesso
Cluster HDInsight sono hello (tutti questi servizi hanno endpoint REST) i servizi HTTP web seguente:

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

Per impostazione predefinita, a questi servizi è concesso l'accesso. È possibile revocare o concedere l'accesso hello dal portale di Azure hello.

> [!NOTE]
> Per concedere o revocare l'accesso hello, sarà necessario reimpostare la password e nome utente di hello del cluster.
>
>

**accesso ai servizi web di toogrant/revoke HTTP**

1. Accedi toohello [portale][azure-portal].
2. Fare clic su **Esplora tutto** hello a sinistra fare clic su **cluster HDInsight**, fare clic sul nome del cluster.
3. Fare clic su **impostazioni** dal menu superiore hello e quindi fare clic su **accesso Cluster**.
4. Se **accesso Cluster** è stato abilitato, è necessario fare clic su **disabilitare**, quindi fare clic su **abilitare** prima di poter impostare hello username e password...
5. Per **nome utente dell'account di accesso Cluster** e **password dell'account di accesso Cluster**, immettere hello nuovo nome utente e password, rispettivamente, per il cluster hello.
6. Fare clic su **SAVE**.

    ![Rimozione complessiva dell'accesso al servizio web http in HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="find-hello-default-storage-account"></a>Trovare l'account di archiviazione predefinito hello
Ogni cluster HDInsight ha un account di archiviazione predefinito. Hello account di archiviazione predefinito e le relative chiavi per un cluster viene visualizzato in **impostazioni**/**proprietà**/**chiavi di archiviazione di Azure**. Vedere [Elencare e visualizzare i cluster](#list-and-show-clusters).

## <a name="find-hello-resource-group"></a>Trovare il gruppo di risorse hello
In modalità Azure Resource Manager hello, ogni cluster HDInsight viene creato con un gruppo di risorse di Azure. gruppo di risorse di Azure Hello che un cluster appartiene tooappears in:

* elenco di cluster Hello dispone di un **gruppo di risorse** colonna.
* Riquadro **Informazioni di base** del cluster.  

Vedere [Elencare e visualizzare i cluster](#list-and-show-clusters).

## <a name="open-hdinsight-query-console"></a>Aprire la console query HDInsight
Hello console HDInsight Query include hello seguenti caratteristiche:

* **Editor Hive**: interfaccia Web GUI per l'invio di processi Hive.  Vedere [Hive eseguire query utilizzando hello Console Query](hdinsight-hadoop-use-hive-query-console.md).

    ![Portale editor hive in HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-hive-editor.png)
* **Cronologia processo**: monitora i processi Hadoop.  

    ![Portale cronologia processi in HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-job-history.png)

    Fare clic su **nome Query** dettagli hello tooshow comprese le proprietà di processo, **processo Query**, e * * Output del processo. È anche possibile scaricare query hello e hello output tooyour workstation.
* **File Browser**: esplorare l'account di archiviazione predefinito hello e hello gli account di archiviazione collegato.

    ![Esplorazione del browser file portale in HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-file-browser.png)

    Nella schermata di hello hello  **<Account>**  indica di tipo elemento hello è un account di archiviazione di Azure.  Selezionare i file hello hello account nome toobrowse.
* **Interfaccia utente Hadoop**.

    ![Interfaccia utente Hadoop portale in HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-ui.png)

    Dall'*interfaccia utente di Hadoop*è possibile cercare i file e controllare i log.
* **Interfaccia utente Yarn**.

    ![Interfaccia utente YARN portale in HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-yarn-ui.png)

## <a name="run-hive-queries"></a>Eseguire query Hive
Fare clic su processi Hive tooran dal portale, hello **Editor Hive** nella Query di HDInsight hello console. Vedere [Aprire la console query HDInsight](#open-hdinsight-query-console).

## <a name="monitor-jobs"></a>Monitorare i processi
Fare clic su processi toomonitor dal portale, hello **Cronologia processo** nella Query di HDInsight hello console. Vedere [Aprire la console query HDInsight](#open-hdinsight-query-console).

## <a name="browse-files"></a>Ricerca dei file
file toobrowse archiviati nell'account di archiviazione predefinito hello e hello gli account di archiviazione collegato, fare clic su **File Browser** nella Query di HDInsight hello console. Vedere [Aprire la console query HDInsight](#open-hdinsight-query-console).

È inoltre possibile utilizzare hello **sfogliare hello file system** utilità da hello **Hadoop UI** nella console di HDInsight hello.  Vedere [Aprire la console query HDInsight](#open-hdinsight-query-console).

## <a name="monitor-cluster-usage"></a>Monitorare l'utilizzo del cluster
Hello **utilizzo** nella sezione del Pannello di cluster HDInsight hello vengono visualizzate informazioni hello numero di core disponibili tooyour sottoscrizione per l'utilizzo con HDInsight, nonché il numero di hello di core allocati toothis cluster e il modo in cui allocato per i nodi di hello all'interno di questo cluster. Vedere [Elencare e visualizzare i cluster](#list-and-show-clusters).

> [!IMPORTANT]
> servizi di hello toomonitor fornito da hello cluster HDInsight, è necessario utilizzare Ambari Web o hello Ambari REST API. Per altre informazioni sull'uso di Ambari, vedere [Gestire i cluster HDInsight tramite Ambari](hdinsight-hadoop-manage-ambari.md)
>
>

## <a name="open-hadoop-ui"></a>Aprire l'interfaccia utente di Hadoop
cluster hello toomonitor Sfoglia hello file system e i log di controllo, fare clic su **Hadoop UI** nella Query di HDInsight hello console. Vedere [Aprire la console query HDInsight](#open-hdinsight-query-console).

## <a name="open-yarn-ui"></a>Aprire l'interfaccia utente di Yarn
toouse interfaccia utente di Yarn, fare clic su **dell'interfaccia utente Yarn** nella Query di HDInsight hello console. Vedere [Aprire la console query HDInsight](#open-hdinsight-query-console).

## <a name="connect-tooclusters-using-rdp"></a>Connettersi tooclusters tramite RDP
le credenziali di Hello per cluster hello fornito al momento della relativa creazione concede l'accesso toohello servizi in cluster hello, ma non toohello cluster tramite Desktop remoto. È possibile attivare l'accesso Desktop remoto durante o dopo il provisioning di un cluster. Per istruzioni hello sull'abilitazione di Desktop remoto al momento della creazione, vedere [cluster HDInsight creare](hdinsight-hadoop-provision-linux-clusters.md).

**tooenable Desktop remoto**

1. Accedi toohello [portale][azure-portal].
2. Fare clic su **Esplora tutto** hello a sinistra fare clic su **cluster HDInsight**, fare clic sul nome del cluster.
3. Fare clic su **impostazioni** dal menu superiore hello e quindi fare clic su **Desktop remoto**.
4. Immettere **Expires On** (Scadenza), **Nome utente Desktop remoto** e **Password Desktop remoto**, quindi fare clic su **Abilita**.

    ![HDInsight - abilitazione/disabilitazione/configurazione di Desktop remoto](./media/hdinsight-administer-use-management-portal/hdinsight.portal.remote.desktop.png)

    i valori predefiniti di Hello per scadenza è una settimana.

   > [!NOTE]
   > È anche possibile utilizzare hello HDInsight .NET SDK tooenable Desktop remoto in un cluster. Hello utilizzare **EnableRdp** metodo sull'oggetto client di HDInsight hello nel seguente modo hello: **client. EnableRdp (NomeCluster, percorso, "rdpuser", "rdppassword" DateTime.Now.AddDays(6))**. Analogamente, toodisable Desktop remoto in cluster hello, è possibile utilizzare **client. DisableRdp (clustername, percorso)**. Per altre informazioni su questi metodi, vedere [Documentazione di riferimento relativa a HDInsight .NET SDK](http://go.microsoft.com/fwlink/?LinkId=529017). È applicabile solo per i cluster HDInsight in esecuzione in Windows.
   >
   >

**tooconnect tooa cluster tramite RDP**

1. Accedi toohello [portale][azure-portal].
2. Fare clic su **Esplora tutto** hello a sinistra fare clic su **cluster HDInsight**, fare clic sul nome del cluster.
3. Fare clic su **impostazioni** dal menu superiore hello e quindi fare clic su **Desktop remoto**.
4. Fare clic su **Connetti** e seguire le istruzioni di hello. Se Connetti è disabilitato, è necessario prima abilitarlo. Assicurarsi che utilizzano Desktop remoto hello nome utente e password.  Non è possibile utilizzare le credenziali utente del Cluster hello.

## <a name="open-hadoop-command-line"></a>Aprire la riga di comando di Hadoop.
tooconnect toohello cluster tramite Desktop remoto e della riga di comando utilizzare hello Hadoop, è necessario innanzitutto aver attivato cluster toohello di accesso Desktop remoto come descritto nella sezione precedente hello.

**tooopen una riga di comando di Hadoop**

1. Connettere il cluster toohello tramite Desktop remoto.
2. Dal desktop hello, fare doppio clic su **della riga di comando Hadoop**.

    ![HDI.HadoopCommandLine][image-hadoopcommandline]

    Per altre informazioni sui comandi Hadoop, vedere la [documentazione di riferimento sui comandi Hadoop](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/CommandsManual.html).

Nella schermata precedente hello, nome della cartella hello ha numero di versione di Hadoop hello incorporato. il numero di versione di Hello possibile creare versioni modificate hello in base dei componenti di Hadoop hello installato nel cluster hello. È possibile utilizzare le cartelle toothose toorefer di Hadoop ambiente variabili. ad esempio:

    cd %hadoop_home%
    cd %hive_home%
    cd %hbase_home%
    cd %pig_home%
    cd %sqoop_home%
    cd %hcatalog_home%

## <a name="next-steps"></a>Passaggi successivi
In questo articolo, si è appreso come un cluster HDInsight tramite toocreate hello portale e modalità tooopen hello strumento da riga di comando di Hadoop. toolearn informazioni, vedere hello seguenti articoli:

* [Amministrare HDInsight tramite Azure PowerShell](hdinsight-administer-use-powershell.md)
* [Amministrare HDInsight tramite l'interfaccia della riga di comando di Azure](hdinsight-administer-use-command-line.md)
* [Creare cluster HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [Inviare processi Hadoop a livello di codice](hdinsight-submit-hadoop-jobs-programmatically.md)
* [Introduzione ad Azure HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Versione di Hadoop inclusa in Azure HDInsight](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-command-line.png "Riga di comando di Hadoop"
