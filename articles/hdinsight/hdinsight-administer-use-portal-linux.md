---
title: cluster aaaManage Hadoop in HDInsight mediante il portale di Azure | Documenti Microsoft
description: Informazioni su come toocreate e gestire cluster HDInsight tramite hello portale di Azure.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5a76f897-02e8-4437-8f2b-4fb12225854a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: c242d43d4ccea7cf1e7be19c3f3d7ed3c4f50918
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-hello-azure-portal"></a>Gestire i cluster Hadoop in HDInsight con hello portale di Azure
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Utilizzo di hello [portale di Azure][azure-portal], è possibile gestire i cluster Hadoop in HDInsight di Azure. Usare il selettore di scheda hello per informazioni sulla gestione di cluster Hadoop in HDInsight mediante altri strumenti.

**Prerequisiti**

Prima di iniziare questo articolo, è necessario disporre di hello seguenti elementi:

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di prova gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="open-hello-portal"></a>Portale hello aperto
1. Accedi troppo[https://portal.azure.com](https://portal.azure.com).
2. Dopo aver aperto il portale di hello, è possibile:

   * Fare clic su **New** dal menu a sinistra di hello toocreate un nuovo cluster:

       ![Pulsante Nuovo cluster HDInsight](./media/hdinsight-administer-use-portal-linux/azure-portal-new-button.png)
   * Fare clic su **cluster HDInsight** da hello toolist menu a sinistra hello cluster esistenti

       ![Pulsante Cluster HDInsight del portale di Azure](./media/hdinsight-administer-use-portal-linux/azure-portal-hdinsight-button.png)

       Se non viene visualizzato il cluster HDInsight, fare clic su **più servizi** hello alla fine dell'elenco di hello e quindi fare clic su **cluster HDInsight** in hello **Intelligence + Analitica** sezione.


## <a name="create-clusters"></a>Creare i cluster
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

HDInsight è compatibile con una vasta gamma di componenti Hadoop. Per hello l'elenco dei componenti di hello che sono stati verificati e supportati, vedere [è la versione di Hadoop in HDInsight di Azure](hdinsight-component-versioning.md). Per informazioni sulla creazione di cluster generale hello, vedere [cluster creare Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

### <a name="access-control-requirements"></a>Requisiti di controllo di accesso

Quando si crea un cluster HDInsight, è necessario specificare una sottoscrizione di Azure. È possibile creare il cluster in un nuovo gruppo di risorse di Azure o un gruppo di risorse esistente. È possibile utilizzare hello seguendo i passaggi tooverify le autorizzazioni per la creazione di cluster HDInsight:

- toouse un gruppo di risorse esistente.

    1. Accedi toohello [portale di Azure](https://portal.azure.com).
    2. Fare clic su **gruppi di risorse** da gruppi di risorse hello toolist hello menu a sinistra.
    3. Selezionare il gruppo di risorse hello desiderato toouse per la creazione del cluster HDInsight.
    4. Fare clic su **Access control (IAM)**e verificare che si (o un gruppo di cui si appartiene) hanno almeno hello accesso toohello risorse dei collaboratori.

- toocreate un nuovo gruppo di risorse

    1. Accedi toohello [portale di Azure](https://portal.azure.com).
    2. Fare clic su **sottoscrizione** dal menu a sinistra di hello. Viene visualizzata un'icona gialla a forma di chiave. Verrà visualizzato un elenco di sottoscrizioni.
    3. Fare clic sulla sottoscrizione hello utilizzare toocreate cluster. 
    4. Fare clic su **Autorizzazioni personali**.  Viene illustrato il [ruolo](../active-directory/role-based-access-control-what-is.md#built-in-roles) sottoscrizione hello. È necessario almeno cluster di HDInsight toocreate accesso collaboratore.

Se viene visualizzato l'errore di NoRegisteredProviderFound hello o MissingSubscriptionRegistration hello, vedere [risolvere i problemi relativi a errori comuni di distribuzione di Azure con Azure Resource Manager](../azure-resource-manager/resource-manager-common-deployment-errors.md).

## <a name="list-and-show-clusters"></a>Elencare e visualizzare i cluster
1. Accedi troppo[https://portal.azure.com](https://portal.azure.com).
2. Fare clic su **cluster HDInsight** da hello toolist menu a sinistra hello cluster esistenti.
3. Fare clic su nome cluster hello. Se l'elenco di cluster hello è lungo, è possibile utilizzare filtri nella parte superiore di hello della pagina hello.
4. Fare clic su un cluster dalla pagina di panoramica hello toosee elenco hello:

    ![Informazioni di base sul cluster HDInsight del Portale di Azure](./media/hdinsight-administer-use-portal-linux/hdinsight-essentials.png)

    * **Dashboard**: dashboard del cluster hello viene aperto, ovvero Ambari Web per i cluster basati su Linux.
    * **Secure Shell**: cluster Mostra hello istruzioni tooconnect toohello utilizzando una connessione Secure Shell (SSH).
    * **Applicare la scalabilità del Cluster**: consente di numero hello toochange di nodi di lavoro per questo cluster.
    * **Eliminare**: cluster hello di eliminazione.
    * **Log attività**: visualizza ed effettua una query dei log attività.
    * **Controllo di accesso (IAM)**: usa le assegnazioni di ruolo.  Vedere [utilizzare le risorse di sottoscrizione di Azure tooyour accesso toomanage assegnazioni ruolo](../active-directory/role-based-access-control-configure.md).
    * **Tag**: consente di tooset chiave/valore coppie toodefine una tassonomia personalizzata dei servizi cloud. Ad esempio, è possibile creare una chiave denominata **progetto**e usare un valore comune per tutti i servizi associati a un progetto specifico.
    * **Diagnostica e risoluzione dei problemi**: visualizza informazioni per la risoluzione dei problemi.
    * **Blocca**: aggiungere blocco tooprevent hello cluster viene modificata o eliminata.
    * **Script di automazione**: modello di gestione risorse di Azure hello visualizzazione ed esportazione per il cluster hello. Attualmente, è possibile esportare solo hello dipendenti account di archiviazione Azure. Vedere [Creare cluster Hadoop basati su Linux in HDInsight tramite modelli di Azure Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md).
    * **Avvio rapido**: visualizza informazioni utili per iniziare a usare HDInsight.
    * **Strumenti per HDInsight**: informazioni della Guida per gli strumenti correlati a HDInsight.
    * **Account di accesso del cluster**: visualizzare le informazioni di accesso cluster hello.
    * **Utilizzo di Core della sottoscrizione**: visualizzazione hello core usate e disponibili per la sottoscrizione.
    * **Applicare la scalabilità del Cluster**: aumento e riduzione hello numero di nodi di lavoro del cluster. Vedere [Ridimensionare i cluster](hdinsight-administer-use-management-portal.md#scale-clusters).
    * **Secure Shell**: cluster Mostra hello istruzioni tooconnect toohello utilizzando una connessione Secure Shell (SSH). Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).
    * **Il HDInsight Partner**: Aggiungi/Rimuovi hello HDInsight Partner corrente.
    * **I Metastore esterni**: visualizzare Metastore Hive e Oozie hello. i Metastore Hello possono essere configurati solo durante il processo di creazione di cluster hello. Vedere [Usare metastore Hive/Oozie](hdinsight-hadoop-provision-linux-clusters.md#use-hiveoozie-metastore).
    * **Script delle azioni**: Bash eseguire script in cluster hello. Vedere [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md).
    * **Applicazioni**: aggiungere/rimuovere applicazioni HDInsight.  Vedere [Installare applicazioni HDInsight personalizzate](hdinsight-apps-install-custom-applications.md).
    * **Proprietà**: consente di visualizzare le proprietà del cluster hello.
    * **Gli account di archiviazione**: visualizzare gli account di archiviazione hello e chiavi hello. gli account di archiviazione Hello vengono configurati durante il processo di creazione di cluster hello.
    * **Identità AAD cluster**:
    * **Nuova richiesta di supporto**: consente di toocreate un ticket di supporto con il supporto tecnico Microsoft.
    
6. Fare clic su **Proprietà**:

    proprietà Hello sono:

   * **Nome host**: nome del cluster.
   * **URL cluster**. Hello URL per l'interfaccia di hello Ambari web.
   * **Stato**: include Aborted, Accepted, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, Operational, Running, Error, Deleting, Deleted, Timedout, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization
   * **Area**: località di Azure. Per un elenco delle posizioni di Azure supportate, vedere hello **area** casella di riepilogo a discesa in [prezzi di HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).
   * **Dati creati**.
   * **Sistema operativo**: **Windows** o **Linux**.
   * **Tipo**: Hadoop, HBase, Storm, Spark.
   * **Versione**. Vedere [Versioni di HDInsight](hdinsight-component-versioning.md)
   * **Sottoscrizione**: nome della sottoscrizione.
   * **Origine dati predefinita**: hello file system cluster predefinito.
   * **Worker nodes size** (Dimensioni nodi di lavoro).
   * **Dimensioni nodo head**.

## <a name="delete-clusters"></a>Eliminare cluster
L'eliminazione di un cluster di non eliminare account di archiviazione predefinito hello o qualsiasi account di archiviazione collegati. È possibile ricreare il cluster hello utilizzando hello stessi account di archiviazione e hello Metastore stesso. È consigliabile toouse un nuovo contenitore Blob predefinito quando si ricrea il cluster hello.

1. Accedi toohello [portale][azure-portal].
2. Fare clic su **cluster HDInsight** dal menu a sinistra di hello. Se **Cluster HDInsight** non è visualizzato, prima fare clic su **Altri servizi**.
3. Fare clic su cluster hello che si desidera toodelete.
4. Fare clic su **eliminare** dal menu superiore hello e quindi seguire le istruzioni di hello.

Vedere anche [Sospendere/Arrestare i cluster](#pauseshut-down-clusters).

## <a name="add-additional-storage-accounts"></a>Aggiungere altri account di archiviazione

Dopo la creazione di un cluster, è possibile aggiungere altri account di archiviazione di Azure e account Azure Data Lake Store. Per ulteriori informazioni, vedere [aggiungere ulteriore spazio di archiviazione account tooHDInsight](./hdinsight-hadoop-add-storage.md).

## <a name="scale-clusters"></a>Ridimensionare i cluster
scalabilità funzionalità cluster di Hello consente numero hello toochange di nodi di lavoro utilizzato da un cluster che è in esecuzione in Azure HDInsight senza toore-creare cluster hello.

> [!NOTE]
> Sono supportati solo i cluster con HDInsight versione 3.1.3 o successive. Se si è certi della versione di hello del cluster, è possibile controllare una pagina delle proprietà hello.  Vedere [Elencare e visualizzare i cluster](#list-and-show-clusters).
>
>

impatto di Hello di modifica del numero di hello di nodi di dati per ogni tipo di cluster supportato da HDInsight:

* Hadoop

    È possibile aumentare facilmente numero hello di nodi di lavoro in un cluster Hadoop che è in esecuzione senza conseguenze per tutti i processi in sospeso o in esecuzione. È inoltre possibile avviare nuovi processi mentre è in corso hello operazione. Gli errori in un'operazione di ridimensionamento normalmente vengono gestiti in modo che hello cluster rimanga sempre in uno stato funzionale.

    Quando un cluster Hadoop è ridotta, riducendo il numero di hello di nodi di dati, alcuni dei servizi di hello cluster hello vengono riavviati. Questo comportamento causa tutti in esecuzione e in sospeso toofail processi al completamento di hello di hello l'operazione di ridimensionamento. È tuttavia possibile inviare di nuovo i processi di hello al termine dell'operazione di hello.
* HBase

    Senza problemi, è possibile aggiungere o rimuovere cluster HBase di nodi tooyour mentre è in esecuzione. Server locali sono bilanciati automaticamente entro pochi minuti di completare l'operazione di ridimensionamento hello. Tuttavia, è possibile bilanciare manualmente server regionali hello accedendo toohello nodo head del cluster e in esecuzione hello seguendo i comandi da una finestra del prompt dei comandi:

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer

    Per ulteriori informazioni sull'utilizzo della shell di HBase hello, vedere]
* Storm

    Senza problemi, è possibile aggiungere o rimuovere cluster Storm tooyour nodi di dati in fase di esecuzione. Tuttavia, dopo il completamento dell'operazione di ridimensionamento hello, sarà necessario topologia hello toorebalance.

    A tale scopo, è possibile scegliere tra due opzioni:

  * Interfaccia utente Web di Storm
  * Interfaccia della riga di comando (CLI)

    Fare riferimento toohello [documentazione di Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) per altri dettagli.

    interfaccia utente web di Storm Hello è disponibile nel cluster HDInsight hello:

    ![Ribilanciamento di HDInsight Storm](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster-storm-rebalance.png)

    Di seguito è riportato un esempio come toouse hello CLI comando topologia di Storm toorebalance hello:

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

**cluster tooscale**

1. Accedi toohello [portale][azure-portal].
2. Fare clic su **cluster HDInsight** dal menu a sinistra di hello.
3. Fare clic su cluster hello da tooscale.
3. Fare clic su **Ridimensiona cluster**.
4. Immettere il **numero di nodi del ruolo di lavoro**. limite Hello hello numero dei nodi del cluster varia tra le sottoscrizioni di Azure. È possibile contattare fatturazione limite hello tooincrease di supporto.  informazioni sui costi di Hello riflette hello apportate toohello numero di nodi.

    ![Scalabilità di HDInsight Hadoop, HBase, Storm, Spark](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster.png)

## <a name="pauseshut-down-clusters"></a>Sospendere/Arrestare i cluster

La maggior parte dei processi Hadoop sono processi batch che vengono eseguito solo occasionalmente. Per la maggior parte dei cluster Hadoop, esistono grandi periodi di tempo tale cluster hello non utilizzato per l'elaborazione. Con HDInsight, i dati vengono archiviati in Archiviazione di Azure ed è possibile eliminare tranquillamente un cluster quando non viene usato.
Vengono addebitati i costi anche per i cluster HDInsight che non sono in uso. Poiché gli addebiti di hello per cluster hello sono spesso più addebiti hello per l'archiviazione, è opportuno economica toodelete cluster quando non sono in uso.

Esistono molti modi, è possibile programmare processo hello:

* Usare Data factory di Azure. Per la creazione di servizi collegati di HDInsight, vedere [Creare cluster Hadoop on demand basati su Linux in HDInsight con Azure Data Factory](hdinsight-hadoop-create-linux-clusters-adf.md) .
* Usare Azure PowerShell.  Vedere [Analizzare i dati relativi ai ritardi dei voli](hdinsight-analyze-flight-delay-data.md).
* Usare l'interfaccia della riga di comando di Azure. Vedere [Gestire cluster Hadoop in HDInsight tramite l'interfaccia della riga di comando di Azure](hdinsight-administer-use-command-line.md).
* Usare HDInsight .NET SDK. Vedere [Inviare processi di Hadoop](hdinsight-submit-hadoop-jobs-programmatically.md).

Per informazioni sui prezzi di hello, vedere [prezzi di HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/). toodelete un cluster da hello portale, vedere [eliminare cluster](#delete-clusters)


## <a name="upgrade-clusters"></a>Aggiornare i cluster

Vedere [versione più recente di HDInsight aggiornamento cluster tooa](./hdinsight-upgrade-cluster.md).

## <a name="change-passwords"></a>Modificare le password
Per un cluster HDInsight possono esistere due account utente. Hello (anche noto come account utente del cluster HDInsight Account utente per HTTP) e account utente SSH hello vengono creati durante il processo di creazione di hello. È possibile utilizzare hello Ambari web UI toochange hello cluster account utente e la password e script azioni toochange hello account utente SSH

### <a name="change-hello-cluster-user-password"></a>Modifica password utente di cluster hello
È possibile utilizzare password dell'utente di hello dell'interfaccia utente Web Ambari toochange hello Cluster. toolog in tooAmbari, è necessario utilizzare nome utente del cluster esistenti hello e password.

> [!NOTE]
> La modifica della password utente (amministrazione) cluster hello potrebbe causare script azioni è state eseguite su toofail questo cluster. Se si dispone di tutte le azioni script persistenti i nodi di lavoro di destinazione, questi script potrebbero non riuscire quando si aggiunge i nodi cluster toohello tramite operazioni di ridimensionamento. Per altre informazioni sulle azioni script, vedere [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md).
>
>

1. Accesso tramite interfaccia utente Web Ambari toohello hello le credenziali utente del cluster HDInsight. nome utente predefinito Hello **admin**. hello URL **https://&lt;nome del Cluster HDInsight > cluster>.azurehdinsight.NET**.
2. Fare clic su **Admin** dal menu in alto hello e quindi fare clic su "Gestisci Ambari".
3. Scegliere dal menu a sinistra hello **utenti**.
4. Fare clic su **Admin**.
5. Fare clic su **Change Password**(Modifica password).

Ambari quindi modifica la password di hello in tutti i nodi del cluster di hello.

### <a name="change-hello-ssh-user-password"></a>Modificare la password utente SSH hello
1. Utilizzando un editor di testo, salvare hello segue testo come un file denominato **changepassword.sh**.

   > [!IMPORTANT]
   > È necessario utilizzare un editor che utilizza LF come terminazione di riga hello. Se l'editor di hello utilizza CR/LF, quindi hello script non funziona.
   >
   >

        #! /bin/bash
        USER=$1
        PASS=$2

        usermod --password $(echo $PASS | openssl passwd -1 -stdin) $USER
2. Caricare hello tooa percorso di archiviazione che è possibile accedere da HDInsight utilizzando un indirizzo HTTP o HTTPS. ad esempio in un archivio di file pubblico come OneDrive o l'archiviazione BLOB di Azure. Salvare i file di toohello di hello URI (indirizzo HTTP o HTTPS), come nel passaggio successivo hello è necessario questo URI.
3. Dal portale di Azure hello, fare clic su **cluster HDInsight**.
4. Fare clic sul cluster HDInsight.
4. Fare clic su **Azioni script**.
4. Da hello **azioni Script** pannello seleziona **inviare nuove**. Quando hello **inviare l'azione script** pannello viene visualizzato, immettere hello le seguenti informazioni:

   | Campo | Valore |
   | --- | --- |
   | Nome |Modifica password SSH |
   | URI script Bash |file di Hello URI toohello changepassword.sh |
   | Nodi (head, lavoro, Nimbus, Supervisor, Zookeeper, e così via) |✓ per tutti i tipi di nodo elencati |
   | parameters |Immettere nome utente di hello SSH e quindi hello nuova password. Deve esserci uno spazio tra il nome di utente hello e una password hello. |
   | Salvare questa azione script... |Lasciare questo campo vuoto. |
5. Selezionare **crea** script hello tooapply. Al termine dell'esecuzione dello script hello, si è in grado di tooconnect toohello cluster tramite SSH con nuova password hello.

## <a name="grantrevoke-access"></a>Concedere/Revocare l'accesso
Cluster HDInsight sono hello (tutti questi servizi hanno endpoint REST) i servizi HTTP web seguente:

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

Per impostazione predefinita, a questi servizi è concesso l'accesso. È possibile revoke o concedere l'accesso hello utilizzando [CLI di Azure](hdinsight-administer-use-command-line.md#enabledisable-http-access-for-a-cluster) e [Azure PowerShell](hdinsight-administer-use-powershell.md#grantrevoke-access).

## <a name="find-hello-subscription-id"></a>Trovare l'ID sottoscrizione hello

**toofind ID sottoscrizione di Azure**

1. Accedi toohello [portale][azure-portal].
2. Fare clic su **Sottoscrizioni**. Ogni sottoscrizione ha un nome e un ID.

Ogni cluster è abbinato tooan sottoscrizione di Azure. Hello sottoscrizione ID è mostrato sul cluster hello **essenziali** riquadro. Vedere [Elencare e visualizzare i cluster](#list-and-show-clusters).

## <a name="find-hello-resource-group"></a>Trovare il gruppo di risorse hello
In modalità Azure Resource Manager hello, ogni cluster HDInsight viene creato con un gruppo di gestione risorse di Azure. gruppo di gestione risorse di Hello che un cluster appartiene tooappears in:

* elenco di cluster Hello dispone di un **gruppo di risorse** colonna.
* Riquadro **Informazioni di base** del cluster.  

Vedere [Elencare e visualizzare i cluster](#list-and-show-clusters).

## <a name="find-hello-default-storage-account"></a>Trovare l'account di archiviazione predefinito hello
Ogni cluster HDInsight ha un account di archiviazione predefinito. Hello account di archiviazione predefinito e le relative chiavi per un cluster viene visualizzato in **gli account di archiviazione**. Vedere [Elencare e visualizzare i cluster](#list-and-show-clusters).

## <a name="run-hive-queries"></a>Eseguire query Hive
Non è possibile eseguire un processo Hive direttamente dal portale di Azure hello, ma è possibile utilizzare hello Hive visualizzazione nell'interfaccia utente Web Ambari.

**query Hive toorun Ambari Hive visualizzazione**

1. Accesso tramite interfaccia utente Web Ambari toohello hello le credenziali utente del cluster HDInsight. nome utente predefinito Hello **admin**. hello URL **https://&lt;nome del Cluster HDInsight > cluster>.azurehdinsight.NET**.
2. Aprire l'Hive vista come mostrato nella seguente schermata hello:  

    ![Vista Hive di HDInsight](./media/hdinsight-administer-use-portal-linux/hdinsight-hive-view.png)
3. Fare clic su **Query** menu principale di hello.
4. Immettere una query Hive in **Editor query** e quindi fare clic su **Esegui**.

## <a name="monitor-jobs"></a>Monitorare i processi
Vedere [HDInsight gestire cluster utilizzando l'interfaccia utente Web Ambari hello](hdinsight-hadoop-manage-ambari.md#monitoring).

## <a name="browse-files"></a>Ricerca dei file
Utilizza hello portale di Azure, è possibile esplorare il contenuto di hello del contenitore predefinito hello.

1. Accedi troppo[https://portal.azure.com](https://portal.azure.com).
2. Fare clic su **cluster HDInsight** da hello toolist menu a sinistra hello cluster esistenti.
3. Fare clic su nome cluster hello. Se l'elenco di cluster hello è lungo, è possibile utilizzare filtri nella parte superiore di hello della pagina hello.
4. Fare clic su **gli account di archiviazione** dal menu a sinistra di hello del cluster.
5. Fare clic su un account di archiviazione.
7. Fare clic su hello **BLOB** riquadro.
8. Fare clic su nome del contenitore predefinito hello.

## <a name="monitor-cluster-usage"></a>Monitorare l'utilizzo del cluster
Hello **utilizzo** nella sezione del Pannello di cluster HDInsight hello vengono visualizzate informazioni hello numero di core disponibili tooyour sottoscrizione per l'utilizzo con HDInsight, nonché il numero di hello di core allocati toothis cluster e il modo in cui allocato per i nodi di hello all'interno di questo cluster. Vedere [Elencare e visualizzare i cluster](#list-and-show-clusters).

> [!IMPORTANT]
> servizi di hello toomonitor fornito da hello cluster HDInsight, è necessario utilizzare Ambari Web o hello Ambari REST API. Per altre informazioni sull'uso di Ambari, vedere [Gestire i cluster HDInsight tramite Ambari](hdinsight-hadoop-manage-ambari.md)
>
>

## <a name="connect-tooa-cluster"></a>Connettere il cluster tooa

* [Usare Hive con HDInsight](hdinsight-hadoop-use-hive-ambari-view.md)
* [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)

## <a name="next-steps"></a>Passaggi successivi
In questo articolo si sono apprese alcune funzioni amministrative di base. toolearn informazioni, vedere hello seguenti articoli:

* [Amministrare HDInsight tramite Azure PowerShell](hdinsight-administer-use-powershell.md)
* [Amministrare HDInsight tramite l'interfaccia della riga di comando di Azure](hdinsight-administer-use-command-line.md)
* [Creare cluster HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [Usare Hive in HDInsight](hdinsight-use-hive.md)
* [Usare Pig in HDInsight](hdinsight-use-pig.md)
* [Usare Sqoop in HDInsight](hdinsight-use-sqoop.md)
* [Introduzione ad Azure HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Versione di Hadoop inclusa in Azure HDInsight](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-portal-linux/hdinsight-hadoop-command-line.png "Riga di comando di Hadoop"
