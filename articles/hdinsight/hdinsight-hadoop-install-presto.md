---
title: cluster di accedere in Linux di Azure HDInsight aaaInstall | Documenti Microsoft
description: Informazioni su come accedere tooinstall Airpal in basati su Linux HDInsight Hadoop cluster e tramite le azioni Script.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: nitinme
ms.openlocfilehash: 5d54d0efc3e5fdc6f5a8d3a94ad2f61d16df24c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-presto-on-hdinsight-hadoop-clusters"></a>Installare e usare Presto nei cluster HDInsight Hadoop

In questo argomento, viene illustrato come accedere in HDInsight Hadoop tooinstall cluster utilizzando l'azione di Script. Verrà inoltre descritto come tooinstall Airpal su un cluster HDInsight Presto esistente.

> [!IMPORTANT]
> Hello passaggi in questo documento richiedono un **cluster HDInsight Hadoop 3.5** che utilizza Linux. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere [Versioni di HDInsight](hdinsight-component-versioning.md).

## <a name="what-is-presto"></a>Che cos'è Presto?
[Presto](https://prestodb.io/overview.html) è un motore di query SQL distribuito veloce per Big Data. Presto è adatto per l'esecuzione di query interattive di petabyte di dati. Per ulteriori informazioni sui componenti hello di accedere e come interagiscono tra loro, vedere [concetti Presto](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).

> [!WARNING]
> I componenti forniti con i cluster di HDInsight hello sono completamente supportati e il supporto Microsoft verrà Guida tooisolate e risolvere i problemi correlati toothese componenti.
> 
> I componenti personalizzati, ad esempio Presto, ricevano supporto commercialmente ragionevole toohelp toofurther per risolvere il problema di hello. Ciò potrebbe comportare la risoluzione problema hello o chiedere che tooengage i canali disponibili per hello apertura di tecnologie di origine in cui si trova esperienza completa per tale tecnologia. È ad esempio possibile ricorrere a molti siti di community, come il [forum MSDN per HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight) o [http://stackoverflow.com](http://stackoverflow.com). Anche per i progetti Apache sono disponibili siti specifici in [http://apache.org](http://apache.org), ad esempio [Hadoop](http://hadoop.apache.org/).
> 
> 


## <a name="install-presto-using-script-action"></a>Installare Presto mediante l'azione di script

In questa sezione vengono fornite istruzioni su come script di esempio hello toouse quando si crea un nuovo cluster mediante hello portale di Azure. 

1. Avviare il provisioning di un cluster attenendosi alla procedura hello in [cluster HDInsight basati su Linux provisioning](hdinsight-hadoop-create-linux-clusters-portal.md). Assicurarsi di creare cluster di hello utilizzando hello **personalizzato** flusso di creazione del cluster. È necessario assicurarsi di tale cluster hello che crei soddisfi hello seguenti requisiti.

    a. Deve essere un cluster Hadoop con HDInsight versione 3.5.

    b. È necessario usare l'archiviazione di Azure come archivio dati hello. Utilizzo Presto in un cluster che utilizza l'archivio Azure Data Lake come opzione di archiviazione hello non è ancora supportato. 

    ![Creazione del cluster HDInsight con opzioni personalizzate](./media/hdinsight-hadoop-install-presto/hdinsight-install-custom.png)

2. In hello **impostazioni avanzate** pannello seleziona **azioni Script**e fornire informazioni hello riportate di seguito:
   
   * **NOME**: immettere un nome descrittivo per l'azione script hello.
   * **URI script Bash**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`
   * **HEAD**: selezionare questa opzione
   * **RUOLO DI LAVORO**: selezionare questa opzione
   * **ZOOKEEPER**: deselezionare questa casella di controllo
   * **PARAMETRI**: lasciare questo campo vuoto


3. Nella parte inferiore di hello di hello **azioni Script** pannello, fare clic su hello **selezionare** configurazione hello toosave dei pulsanti. Infine, fare clic su hello **selezionare** pulsante nella parte inferiore di hello di hello **impostazioni avanzate** informazioni di configurazione di blade toosave hello.

4. Continuano il provisioning del cluster di hello, come descritto in [cluster HDInsight basati su Linux provisioning](hdinsight-hadoop-create-linux-clusters-portal.md).

    > [!NOTE]
    > Azure PowerShell, hello CLI di Azure, HDInsight .NET SDK hello o modelli di gestione risorse di Azure possono anche essere azioni script tooapply utilizzato. È inoltre possibile applicare tooalready azioni script i cluster in esecuzione. Per altre informazioni, vedere [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md).
    > 
    > 

## <a name="use-presto-with-hdinsight"></a>Usare Presto con HDInsight

Eseguire hello seguendo i passaggi toouse accedere in un cluster di HDInsight dopo l'installazione utilizzando i passaggi di hello descritti in precedenza.

1. Connettere il cluster di HDInsight toohello tramite SSH:
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).
     

2. Avviare shell di hello Presto utilizzando hello comando seguente.
   
        presto --schema default

3. Eseguire una query sulla tabella di esempio, **hivesampletable**, che è disponibile in tutti i cluster HDInsight per impostazione predefinita.
   
        select count (*) from hivesampletable;
   
    Per impostazione predefinita sono già configurati i connettori [Hive](https://prestodb.io/docs/current/connector/hive.html) e [TPCH](https://prestodb.io/docs/current/connector/tpch.html) per Presto. Hive connettore è configurato toouse hello predefinito installato Hive installazione, pertanto tutte le tabelle di hello dall'Hive saranno automaticamente visibili nell'accedere.

    Per informazioni dettagliate su come è possibile usate Presto, vedere la [documentazione su Presto](https://prestodb.io/docs/current/index.html).

## <a name="use-airpal-with-presto"></a>Usare Airpal con Presto

[Airpal](https://github.com/airbnb/airpal#airpal) è un'interfaccia per query basate su Web open source per Presto. Per altre informazioni su Airpal, vedere la [documentazione su Airpal](https://github.com/airbnb/airpal#airpal).

In questa sezione viene analizzato in passaggi hello troppo**installarvi Airpal hello edgenode** di un cluster HDInsight Hadoop, che sono già disponibili accedere installato. In questo modo il che interfaccia di query che hello Airpal web è disponibile sulla hello Internet.

1. Tramite SSH, connettersi toohello nodo head del cluster HDInsight hello Presto installato:
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Una volta connessi, eseguire hello comando seguente.

        sudo slider registry  --name presto1 --getexp presto 
   
    Verrà visualizzato un output simile hello seguente:

        {
            "coordinator_address" : [ {
                "value" : "10.0.0.12:9090",
                "level" : "application",
                "updatedTime" : "Mon Apr 03 20:13:41 UTC 2017"
        } ]

3. Dall'output di hello, si noti il valore di hello per hello **valore** proprietà. È necessario durante l'installazione di Airpal nel edgenode cluster hello. Output di hello precedente valore hello che occorre è **10.0.0.12:9090**.

4. Usa modello hello  **[qui](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)**  toocreate un HDInsight edgenode del cluster e fornire valori hello, come illustrato nella seguente schermata hello.

    ![Installazione di HDInsight Airpal nel cluster Presto](./media/hdinsight-hadoop-install-presto/hdinsight-install-airpal.png)

5. Fare clic su **Acquista**.

6. Una volta apportate modifiche hello toohello applicato configurazione del cluster, è possibile accedere interfaccia web di hello Airpal utilizzando hello alla procedura seguente.

    a. Dal Pannello di hello cluster, fare clic su **applicazioni**.

    ![Avvio di HDInsight Airpal nel cluster Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal.png)

    b. Da hello **App installate** pannello, fare clic su **portale** contro airpal.

    ![Avvio di HDInsight Airpal nel cluster Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal-1.png)

    c. Quando richiesto, immettere le credenziali di amministratore hello specificato durante la creazione di hello cluster HDInsight Hadoop.

## <a name="customize-a-presto-installation-on-hdinsight-cluster"></a>Personalizzare un'installazione Presto nel cluster HDInsight

Dopo aver installato in un cluster HDInsight Hadoop accedere, è possibile personalizzare hello installazione toomake modifiche, ad esempio le impostazioni di aggiornamento della memoria, modificare i connettori e così via. Eseguire hello seguendo i passaggi toodo così.

1. Tramite SSH, connettersi toohello nodo head del cluster HDInsight hello Presto installato:
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Apportare le modifiche di configurazione nel file hello `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`. Per altre informazioni sulla configurazione di Presto, vedere [Configurazione di Presto per i cluster basati su YARN](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).

3. Interrompere e terminare hello istanza attualmente in esecuzione di accedere.

        sudo slider stop presto1 --force
        sudo slider destroy presto1 --force

4. Avviare una nuova istanza di accedere a personalizzazione hello.

       sudo slider create presto1 --template /var/lib/presto/presto-hdinsight-master/appConfig-default.json --resources /var/lib/presto/presto-hdinsight-master/resources-default.json

5. Attendere hello nuova istanza toobe pronto e prendere nota indirizzo coordinator presto.


       sudo slider registry --name presto1 --getexp presto

## <a name="generate-benchmark-data-for-hdinsight-clusters-that-run-presto"></a>Generare dati di benchmark per i cluster HDInsight in cui è in esecuzione Presto

TPC-DS è hello standard per la misurazione delle prestazioni di hello di molti sistemi di supporto decisionale, inclusi i sistemi di dati. È possibile utilizzare Presto sui dati di toogenerate cluster HDInsight e valutare mette a confronto con i propri dati di riferimento di HDInsight. Per altre informazioni, vedere [qui](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).



## <a name="see-also"></a>Vedere anche
* [Installare e usare Hue nei cluster HDInsight](hdinsight-hadoop-hue-linux.md). La tonalità corrisponde a un sito web dell'interfaccia utente che rende facile toocreate, eseguire e salvare i processi Pig e Hive, nonché come Sfoglia risorsa di archiviazione di hello predefinito per il cluster HDInsight.

* [Installare Giraph in cluster HDInsight](hdinsight-hadoop-giraph-install-linux.md). Utilizzare cluster personalizzazione tooinstall che cluster Giraph in HDInsight Hadoop. Giraph consente grafico tooperform elaborazione tramite Hadoop e può essere utilizzato con Azure HDInsight.

* [Installare Solr in cluster HDInsight](hdinsight-hadoop-solr-install-linux.md). Utilizzare cluster personalizzazione tooinstall che cluster Solr in HDInsight Hadoop. Solr consente operazioni di ricerca avanzate tooperform sui dati archiviati.

[hdinsight-install-r]: hdinsight-hadoop-r-scripts-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
