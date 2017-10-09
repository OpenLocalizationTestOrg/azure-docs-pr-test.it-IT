---
title: "aaaGet familiarità e Hadoop Hive in HDInsight di Azure | Documenti Microsoft"
description: Informazioni su come cluster di HDInsight toocreate e dati di query con Hive.
keywords: introduzione a Hadoop, Hadoop basato su Linux, guida introduttiva a Hadoop, introduzione a Hive, guida introduttiva a Hive
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6a12ed4c-9d49-4990-abf5-0a79fdfca459
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: jgao
ms.openlocfilehash: 3d96d78121200ebda3626dd2c3885e3ddacd546d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="hadoop-tutorial-get-started-using-hadoop-in-hdinsight"></a>Esercitazione su Hadoop: Introduzione all'uso di Hadoop in HDInsight

Informazioni su come toocreate [Hadoop](http://hadoop.apache.org/) cluster HDInsight e come processi di toorun Hive in HDInsight. [Apache Hive](https://hive.apache.org/) hello componente più diffusi nell'ecosistema Hadoop hello. HDInsight attualmente viene fornito con [sette diversi tipi di cluster](hdinsight-hadoop-introduction.md#overview). Ogni tipo di cluster supporta un set diverso di componenti. Tutti i tipi di cluster supportano Hive. Per un elenco dei componenti supportati in HDInsight, vedere [novità introdotta nelle versioni di cluster Hadoop hello fornite da HDInsight?](hdinsight-component-versioning.md)  

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questa esercitazione, è necessario avere:

* **Sottoscrizione di Azure**: toocreate un mese di un account di prova, è esplorare troppo[azure.microsoft.com/free](https://azure.microsoft.com/free).

## <a name="create-cluster"></a>Creare cluster

La maggior parte dei processi Hadoop è costituita da processi batch. Creare un cluster, eseguire alcuni processi e quindi eliminare il cluster hello. In questa sezione viene creato un cluster Hadoop in HDInsight usando un [modello di Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). Per questa esercitazione non è necessario conoscere il modello di Resource Manager. Per altri metodi di creazione del cluster e informazioni sulle proprietà hello utilizzate in questa esercitazione, vedere [cluster HDInsight creare](hdinsight-hadoop-provision-linux-clusters.md). Usare il selettore di hello in primo piano hello di hello pagina toochoose le opzioni di creazione del cluster.

modello di gestione risorse di Hello utilizzato in questa esercitazione si trova in [GitHub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/). 

1. Fare clic su hello seguente immagine toosign in tooAzure e il modello di gestione risorse hello Apri nel portale di Azure hello. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-ssh-password%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Immettere o selezionare hello seguenti valori:
   
    ![HDInsight Linux get avviato il modello di gestione delle risorse nel portale](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-arm-template-on-portal.png "cluster Hadoop distribuire usando HDInsigut hello portale di Azure e un modello di gestione di gruppo di risorse").
   
    * **Sottoscrizione**: selezionare una sottoscrizione di Azure.
    * **Gruppo di risorse**: creare un gruppo di risorse o selezionarne uno esistente.  Un gruppo di risorse è un contenitore di componenti di Azure.  In questo caso, il gruppo di risorse di hello contiene cluster HDInsight hello e account di archiviazione Azure hello dipendenti. 
    * **Percorso**: selezionare una località di Azure in cui si desidera toocreate del cluster.  Scegliere un percorso di più vicino tooyou per ottenere prestazioni migliori. 
    * **Tipo di cluster**: selezionare **hadoop** per questa esercitazione.
    * **Nome del cluster**: immettere un nome per un cluster Hadoop hello.
    * **Nome account di accesso e la password del cluster**: nome di account di accesso predefinito hello **admin**.
    * **Nome utente SSH e password**: nome utente predefinito hello **sshuser**.  È possibile rinominarlo. 
     
    Alcune proprietà sono stati impostati come hardcoded nel modello di hello.  È possibile configurare questi valori dal modello hello.

    * **Percorso**: hello posizione del cluster hello e condivisione di account di archiviazione dipendenti hello hello stesso percorso del gruppo di risorse hello.
    * **Versione del cluster**: 3.5
    * **Tipo di sistema operativo**: Linux
    * **Numero di nodi del ruolo di lavoro**: 2

     Ogni cluster ha una dipendenza da un [account di archiviazione di Azure](hdinsight-hadoop-use-blob-storage.md) o da un [account Azure Data Lake](hdinsight-hadoop-use-data-lake-store.md). Viene definito come account di archiviazione predefinito hello. Cluster HDInsight e il relativo account di archiviazione predefinito devono essere posizionati in hello stessa area di Azure. L'eliminazione di cluster non comporta l'eliminazione di account di archiviazione hello. 
     
     Per una spiegazione più approfondita di queste proprietà, vedere l'articolo su come [create cluster Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

3. Selezionare **accetto le condizioni indicate in precedenza toohello** e **Pin toodashboard**, quindi fare clic su **acquisto**. Verrà visualizzato un nuovo riquadro denominato **distribuzione del modello di distribuzione** nel dashboard del portale hello. Dovrà trascorrere circa toocreate circa 20 minuti di un cluster. Una volta creato il cluster hello, didascalia hello del riquadro hello è modificato toohello nome gruppo di risorse specificato. E portale hello apre automaticamente il gruppo di risorse hello in un nuovo pannello. È possibile visualizzare sia i cluster di hello e spazio di archiviazione predefinito hello elencati.
   
    ![Gruppo di risorse iniziale in HDInsight basato su Linux](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-resource-group.png "Gruppo di risorse cluster in Azure HDInsight").

4. Fare clic su cluster hello cluster nome tooopen hello in un nuovo pannello.

   ![Impostazioni iniziali del cluster HDInsight basato su Linux](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-cluster-settings.png "Proprietà del cluster HDInsight")


## <a name="run-hive-queries"></a>Eseguire query Hive
[Apache Hive](hdinsight-use-hive.md) è componente più diffusi di hello utilizzato in HDInsight. Esistono diversi modi i processi Hive toorun in HDInsight. In questa esercitazione è utilizzare hello vista Ambari Hive dal portale hello. Per altri metodi di esecuzione di processi Hive, vedere [Usare Hive in HDInsight](hdinsight-use-hive.md).

1. Dalla schermata precedente hello, fare clic su **Dashboard Cluster**, quindi fare clic su **Dashboard del Cluster HDInsight**.  È inoltre possibile esplorare troppo **https://&lt;ClusterName >. cluster>.azurehdinsight.NET**, dove &lt;ClusterName > hello cluster creato nella precedente sezione tooopen di hello Ambari.
2. Immettere nome utente di Hadoop hello e la password specificati nella sezione precedente hello. nome utente predefinito Hello **admin**.
3. Aprire **visualizzazione Hive** come illustrato nella seguente schermata hello:
   
    ![Selezione delle visualizzazioni di Ambari](./media/hdinsight-hadoop-linux-tutorial-get-started/selecthiveview.png "Menu di visualizzazione di Hive di HDInsight").
4. In hello **Editor di Query** sezione della pagina di hello, hello Incolla seguendo le istruzioni HiveQL nel foglio di lavoro hello:
   
        SHOW TABLES;
   
   > [!NOTE]
   > Il punto e virgola è obbligatorio per Hive.       
   > 
   > 
5. Fare clic su **Execute**. Oggetto **risultati della Query processo** sezione dovrà essere visualizzato di sotto di hello Editor di Query e visualizzare informazioni sul processo hello. 
   
    Al termine di query hello, hello **risultati della Query processo** sezione Visualizza risultati di hello dell'operazione di hello. Verrà visualizzata una tabella denominata **hivesampletable**. Questa tabella Hive di esempio viene fornito con tutti i cluster HDInsight hello.
   
    ![Visualizzazioni Hive di HDInsight](./media/hdinsight-hadoop-linux-tutorial-get-started/hiveview.png "Editor di query della visualizzazione Hive di HDInsight").
6. Ripetere i passaggi 4 e hello toorun passaggio 5 seguente query:
   
        SELECT * FROM hivesampletable;
   
   > [!TIP]
   > Hello nota **salvare risultati** elenco a discesa nella hello superiore sinistra del hello **risultati della Query processo** sezione; è possibile utilizzare i risultati hello download tooeither o salvarli tooHDInsight archiviazione come un file CSV.
   > 
   > 
7. Fare clic su **cronologia** tooget un elenco di processi di hello.

Dopo aver completato un processo Hive, è possibile [esportare hello risultati tooAzure SQL database o database di SQL Server](hdinsight-use-sqoop-mac-linux.md), è anche possibile [visualizzare i risultati di hello utilizzando Excel](hdinsight-connect-excel-power-query.md). Per ulteriori informazioni sull'utilizzo di Hive in HDInsight, vedere [utilizzare Hive e HiveQL con Hadoop in HDInsight tooanalyze un file di esempio Apache log4j](hdinsight-use-hive.md).

## <a name="clean-up-hello-tutorial"></a>Pulire esercitazione hello
Dopo aver completato l'esercitazione hello, si consiglia di cluster hello toodelete. Con HDInsight, i dati vengono archiviati in Archiviazione di Azure ed è possibile eliminare tranquillamente un cluster quando non viene usato. Vengono addebitati i costi anche per i cluster HDInsight che non sono in uso. Poiché gli addebiti di hello per cluster hello sono spesso più addebiti hello per l'archiviazione, è opportuno economica toodelete cluster quando non sono in uso. 

> [!NOTE]
> Utilizzando [Data Factory di Azure](hdinsight-hadoop-create-linux-clusters-adf.md), è possibile creare cluster HDInsight su richiesta e configurare una TimeToLive impostazione troppo eliminare cluster hello automaticamente. 
> 
> 

**toodelete hello cluster e/o hello account di archiviazione predefinito**

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Dal dashboard del portale di hello, fare clic sul riquadro hello con nome gruppo di risorse hello che è utilizzato per creare cluster hello.
3. Fare clic su **eliminare** in hello pannello toodelete hello risorsa gruppo di risorse, che contiene il cluster hello e account di archiviazione predefinito hello; o fare clic sul nome del cluster hello in hello **risorse** riquadro e quindi fare clic su **Eliminare** nel Pannello di cluster hello. Si noti che il gruppo di risorse hello di eliminazione Elimina account di archiviazione hello. Se si desidera l'account di archiviazione tookeep hello, è possibile scegliere solo i cluster di hello toodelete.

## <a name="troubleshoot"></a>Risoluzione dei problemi

Se si verificano problemi di creazione dei cluster HDInsight, vedere i [requisiti dei controlli di accesso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione, si è appreso come toocreate un HDInsight basati su Linux utilizzando un modello di gestione risorse del cluster e come query Hive base tooperform.

toolearn più sull'analisi dei dati con HDInsight, vedere hello seguenti articoli:

* toolearn ulteriori informazioni sull'utilizzo di Hive con HDInsight, incluso come una query Hive tooperform da Visual Studio, vedere [utilizzare Hive con HDInsight][hdinsight-use-hive].
* toolearn su Pig, un linguaggio tootransform dati, vedere [usare Pig con HDInsight][hdinsight-use-pig].
* toolearn su MapReduce, un toowrite programmi che elaborano i dati in Hadoop, vedere [utilizzare MapReduce con HDInsight][hdinsight-use-mapreduce].
* toolearn sull'uso di strumenti di HDInsight hello per i dati di Visual Studio tooanalyze in HDInsight, vedere [iniziare a usare gli strumenti di Visual Studio Hadoop per HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).

Se si sta toostart pronto funziona con i propri dati ed è necessario tooknow ulteriori informazioni sugli come HDInsight archivia i dati o come dati tooget in HDInsight, vedere l'esempio hello:

* Per informazioni sul modo in cui HDInsight usa Archiviazione di Azure, vedere [Usare Archiviazione di Azure con HDInsight](hdinsight-hadoop-use-blob-storage.md).
* Per informazioni su come tooupload tooHDInsight di dati, vedere [caricare dati tooHDInsight][hdinsight-upload-data].

Se si desidera toolearn ulteriori informazioni sulla creazione o la gestione di un cluster HDInsight, vedere l'esempio hello:

* toolearn sulla gestione dei cluster HDInsight basati su Linux, vedere [cluster di gestire HDInsight con Ambari](hdinsight-hadoop-manage-ambari.md).
* toolearn più sulle opzioni di hello è possibile selezionare durante la creazione di un cluster HDInsight, vedere [la creazione di HDInsight su Linux usando le opzioni personalizzate](hdinsight-hadoop-provision-linux-clusters.md).
* Se si ha familiarità con Linux e Hadoop, ma si desidera specifiche tooknow sul Hadoop in HDInsight hello, vedere [utilizzo di HDInsight su Linux](hdinsight-hadoop-linux-information.md). In questo articolo sono disponibili informazioni quali:
  
  * URL per i servizi ospitati nel cluster di hello, ad esempio Ambari e WebHCat
  * percorso di Hello del file Hadoop ed esempi sulla hello file system locale
  * utilizzo di Hello di Azure Storage (WASB) anziché HDFS come archivio dati predefinito di hello

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


