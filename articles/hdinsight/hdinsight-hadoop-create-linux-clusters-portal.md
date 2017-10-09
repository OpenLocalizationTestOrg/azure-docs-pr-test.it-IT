---
title: i cluster Hadoop aaaCreate tramite un browser web - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come toocreate Hadoop, HBase, Storm o Spark cluster Linux per HDInsight mediante un web browser e hello portale di anteprima di Azure.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 697278cf-0032-4f7c-b9b2-a84c4347659e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 63027e35e2d66dd76218aff3e0c085fc811736ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-hello-azure-portal"></a>Creare i cluster basati su Linux in HDInsight mediante hello portale di Azure
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Hello portale di Azure è uno strumento di gestione basato su web per i servizi e le risorse ospitate nel cloud di Microsoft Azure hello. In questo articolo si apprenderà come toocreate HDInsight basati su Linux cluster tramite il portale di hello.

## <a name="prerequisites"></a>Prerequisiti
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Un Web browser moderno**. portale di Azure Hello utilizza HTML5 e Javascript e potrebbe non funzionare correttamente nei browser meno recenti.

## <a name="create-clusters"></a>Creare i cluster
Hello portale di Azure espone la maggior parte delle proprietà del cluster hello. Con il modello di Azure Resource Manager è possibile nascondere molti dettagli. Per altre informazioni, vedere [Creare cluster Hadoop basati su Linux in HDInsight tramite modelli di Azure Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md).

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Fare clic su **+**, **Intelligence e analisi** e quindi su **HDInsight**.
   
    ![Creare un nuovo cluster nel portale di Azure hello](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster.png "creazione di un nuovo cluster in hello portale di Azure")

3. In hello **HDInsight** pannello, fare clic su **personalizzato (dimensioni, le impostazioni, App)**, fare clic su **nozioni di base**, quindi immettere le seguenti informazioni hello.

    ![Creare un nuovo cluster nel portale di Azure hello](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-basics.png "creazione di un nuovo cluster in hello portale di Azure")

    * Inserire il **Nome cluster**: il nome deve essere univoco a livello globale.

    * Da hello **sottoscrizione** hello elenco a discesa, seleziona la sottoscrizione di Azure verrà utilizzata per il cluster hello.

    * Fare clic su **Tipo di cluster**, quindi scegliere:
   
        * **Tipo di cluster**: se non si conosce quali toochoose, selezionare **Hadoop**. È il tipo di cluster più diffuso hello.
     
            > [!IMPORTANT]
            > HDInsight cluster sono disponibili in un'ampia gamma di tipi che corrispondono a carico di lavoro toohello o tecnologia di hello cluster è ottimizzata per. Non è toocreate alcun metodo supportato per un cluster che combina più tipi, ad esempio Storm e HBase in un cluster. 
            > 
            > 
        
        * **Sistema operativo**: selezionare **Linux**.
        
        * **Versione**: utilizzare versione di hello predefinita se non si conosce quali toochoose. Per altre informazioni, vedere [Versioni del cluster HDInsight](hdinsight-component-versioning.md).
        * **Livello del cluster**: HDInsight di Azure fornisce offerte di cloud hello dati in due categorie: livello Standard e Premium. Per ulteriori informazioni, vedere [Livelli di cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-tiers).

    * Per **nome utente dell'account di accesso Cluster** e **password dell'account di accesso Cluster**, fornire nome utente hello e una password per l'utente amministratore hello.

    * Immettere un **nome utente SSH** e se si desidera password SSH di hello toohave identico hello password amministratore specificata in precedenza, selezionare hello **usare stessa password account di accesso cluster** casella di controllo. In caso contrario, specificare un **PASSWORD** o **chiave pubblica**, che sarà l'utente SSH hello tooauthenticate utilizzato. Utilizzo di una chiave pubblica è hello approccio consigliato. Fare clic su **selezionare** durante la configurazione di credenziali di hello inferiore toosave hello.
   
        Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

    * Per **gruppo di risorse**, specificare se si desidera toocreate un nuovo gruppo di risorse o utilizzarne uno esistente.

    * Specificare un data center **percorso** in cui verrà creato il cluster hello.

    * Fare clic su **Avanti**.

4. In hello **archiviazione** pannello, specificare se si desidera archiviazione di Azure (WASB) o archivio Data Lake come lo spazio di archiviazione predefinito. Esaminare la tabella hello riportata di seguito per ulteriori informazioni.

    ![Creare un nuovo cluster nel portale di Azure hello](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-storage.png "creazione di un nuovo cluster in hello portale di Azure")

    | Archiviazione                                      | Descrizione |
    |----------------------------------------------|-------------|
    | **BLOB del servizio di archiviazione di Azure come risorsa di archiviazione predefinita**   | <ul><li>Per **Tipo di archiviazione primario** selezionare **Archiviazione di Azure**. Successivamente, per **metodo di selezione**, è possibile scegliere **sottoscrizioni personali** se si desidera toospecify un account di archiviazione che fa parte di una sottoscrizione di Azure e account di archiviazione selezionate hello. In caso contrario, fare clic su **chiave di accesso** e fornire informazioni hello hello account di archiviazione che si desidera toochoose da esterni alla sottoscrizione di Azure.</li><li>Per **contenitore predefinito**, è possibile scegliere toogo con nome del contenitore predefinito hello suggerite dal portale hello o specificare i propri.</li><li>Se si utilizza WASB come spazio di archiviazione predefinito, è possibile (facoltativamente) fare clic su **altri account di archiviazione** tooassociate con cluster hello gli account di archiviazione aggiuntive di toospecify. In hello **chiavi di archiviazione di Azure** pannello, fare clic su **aggiungere una chiave di archiviazione**, e quindi è possibile fornire un account di archiviazione dalle sottoscrizioni di Azure o da altre sottoscrizioni (fornendo l'account di archiviazione hello chiave di accesso).</li><li>Se si utilizza WASB come spazio di archiviazione predefinito, è possibile (facoltativamente) fare clic su **accesso archivio Data Lake** toospecify archivio Azure Data Lake come ulteriore spazio di archiviazione. Per altre informazioni, vedere [Creare un cluster HDInsight con Data Lake Store tramite il Portale di Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</li></ul> |
    | **Azure Data Lake Store come risorsa di archiviazione predefinita** | Per **tipo di archiviazione primario**selezionare **archivio Data Lake** e quindi fare riferimento articolo toohello [creare un cluster HDInsight con archivio Data Lake tramite il portale di Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md) per istruzioni. |
    | **Metastore esterni**                      | Facoltativamente, è possibile specificare un SQL database toosave Hive e Oozie i metadati associati con cluster hello. Per **selezionare un database SQL per l'Hive** selezionare un database SQL e quindi fornire nome utente/password hello per database hello. Ripetere questi passaggi per i metadati Oozie.<br><br>Alcune considerazioni durante l'utilizzo del database SQL di Azure per metastore. <ul><li>database SQL di Azure Hello utilizzato per il metastore hello deve consentire la connettività tooother servizi di Azure, tra cui Azure HDInsight. Nel dashboard del database SQL di Azure hello, sul lato destro di hello, fare clic sul nome del server hello. Si tratta hello server sul quale hello SQL è in esecuzione l'istanza del database. Nella visualizzazione di hello del server, fare clic su **configura**e quindi per **servizi Azure**, fare clic su **Sì**, quindi fare clic su **salvare**.</li><li>Quando si crea un metastore, non utilizzare un nome di database che contiene i trattini o trattini, poiché ciò potrebbe causare hello cluster creazione processo toofail.</li></ul>                                                                                                                                                                       |

    Fare clic su **Avanti**. 

    > [!WARNING]
    > Utilizzo di un account di archiviazione aggiuntivo in un percorso diverso da quello del cluster HDInsight hello non è supportato.

5. Facoltativamente, fare clic su **applicazioni** tooinstall applicazioni che funzionano con i cluster HDInsight. Queste applicazioni possono essere sviluppate da Microsoft, da fornitori di software indipendenti (ISV) o dall'utente. Per altre informazioni, vedere [Installare applicazioni HDInsight](hdinsight-apps-install-applications.md#install-applications-during-cluster-creation).


6. Fare clic su **dimensioni del Cluster** toodisplay informazioni sui nodi hello che verranno creati per questo cluster. Impostare il numero di hello di nodi di lavoro che è necessario per il cluster hello. Hello stimato verrà visualizzato all'interno di blade hello costo del cluster di hello.
   
    ![Pannello Piani tariffari per il nodo](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-nodes.png "Specificare il numero di nodi del cluster")
   
   > [!IMPORTANT]
   > Se si prevede più di 32 nodi di lavoro, al momento della creazione del cluster o ridimensionando cluster hello dopo la creazione, è necessario selezionare una dimensione del nodo head con almeno 8 core e 14GB di ram.
   > 
   > Per altre informazioni sulle dimensioni di nodo e i costi associati, vedere [Prezzi di HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).
   > 
   > 
   
   Fare clic su **Avanti** nodo hello toosave dei prezzi di configurazione.

7. Fare clic su **impostazioni avanzate** tooconfigure altre impostazioni facoltative, ad esempio utilizzando **azioni Script** toocustomize tooinstall un cluster i componenti personalizzati o aggiungendo un **diretevirtuale**. Esaminare la tabella hello riportata di seguito per ulteriori informazioni.

    ![Pannello Piani tariffari per il nodo](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-advanced.png "Specificare il numero di nodi del cluster")

    | Opzione | Descrizione |
    |--------|-------------|
    | **Azioni Script** | Utilizzare questa opzione se si desidera toouse toocustomize un script personalizzato, un cluster come cluster hello viene creato. Per altre informazioni sulle azioni di script, vedere [Personalizzare i cluster HDInsight mediante le azioni script](hdinsight-hadoop-customize-cluster-linux.md). |
    | **Rete virtuale** | Se si desidera tooplace hello cluster in una rete virtuale, selezionare una subnet hello e di rete virtuale Azure. Per informazioni sull'uso di HDInsight con una rete virtuale, inclusi i requisiti di configurazione specifico per hello rete virtuale, vedere [funzionalità estendere HDInsight tramite una rete virtuale di Azure](hdinsight-extend-hadoop-virtual-network.md). |

    Fare clic su **Avanti**.

8. In hello **riepilogo** pannello, verificare le informazioni di hello immesso in precedenza e quindi fare clic su **crea**.

    ![Pannello Piani tariffari per il nodo](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-summary.png "Specificare il numero di nodi del cluster")
    
    > [!NOTE]
    > Richiederà del tempo hello cluster toobe creato, in genere circa 15 minuti. Utilizzare il riquadro hello su hello schermata iniziale oppure hello **notifiche** voce hello a sinistra della hello pagina toocheck nel processo di provisioning hello.
    > 
    > 
12. Al termine del processo di creazione di hello, fare clic su riquadro hello per cluster hello dal Pannello di hello schermata iniziale toolaunch hello cluster. Pannello cluster Hello fornisce hello le seguenti informazioni.
    
    ![Pannello Cluster](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-completed.png "Proprietà del cluster")
    
    Utilizzare hello seguendo le icone di hello toounderstand nella parte superiore di hello di questo pannello.
    
    * **Panoramica** scheda fornisce tutte le informazioni essenziali hello sul cluster hello, ad esempio nome hello, hello risorsa gruppo a cui appartiene, percorso hello, sistema operativo hello, URL per il dashboard di cluster hello e così via.
    * **Dashboard** rimanda toohello Ambari portale associato hello cluster.
    * **Secure Shell**: le informazioni necessarie cluster hello tooaccess tramite SSH.
    * **Cluster di scala** consente aumentare il numero di hello di nodi di lavoro associato hello cluster.
    * **Eliminare**: cluster HDInsight hello di eliminazione.
    

## <a name="customize-clusters"></a>Personalizzare i cluster
* Vedere [Personalizzare cluster HDInsight tramite Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md).
* Vedere [Personalizzare cluster HDInsight usando l'azione script](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="delete-hello-cluster"></a>Eliminare il cluster hello
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Risoluzione dei problemi

Se si verificano problemi di creazione dei cluster HDInsight, vedere i [requisiti dei controlli di accesso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Passaggi successivi
Ora che è stato creato correttamente un cluster HDInsight, utilizzare hello seguente come toolearn toowork con il cluster:

### <a name="hadoop-clusters"></a>Cluster Hadoop
* [Usare Hive con HDInsight](hdinsight-use-hive.md)
* [Usare Pig con HDInsight](hdinsight-use-pig.md)
* [Usare MapReduce con HDInsight](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a>Cluster HBase
* [Introduzione a HBase in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md)
* [Sviluppare applicazioni Java per HBase in HDInsight](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a>Cluster Storm
* [Sviluppare topologie Java per Storm in HDInsight](hdinsight-storm-develop-java-topology.md)
* [Usare i componenti di Python in Storm in HDInsight](hdinsight-storm-develop-python-topology.md)
* [Distribuire e monitorare le topologie con Storm in HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a>Cluster Spark
* [Creare un'applicazione autonoma con Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Eseguire i processi in modalità remota in un cluster Spark utilizzando Livy](hdinsight-apache-spark-livy-rest-interface.md)
* [Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight](hdinsight-apache-spark-use-bi-tools.md)
* [Spark con Machine Learning: usare Spark in HDInsight risultati dell'ispezione alimentare toopredict](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale](hdinsight-apache-spark-eventhub-streaming.md)

