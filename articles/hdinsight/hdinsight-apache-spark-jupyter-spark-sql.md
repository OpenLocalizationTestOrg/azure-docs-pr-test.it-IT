---
title: cluster aaaCreate un Apache Spark in HDInsight di Azure | Documenti Microsoft
description: "Guida introduttiva di HDInsight Spark in modalità di cluster toocreate un Apache Spark in HDInsight."
keywords: guida introduttiva spark,spark interattivo,query interattiva,hdinsight spark,azure spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 91f41e6a-d463-4eb4-83ef-7bbb1f4556cc
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 002f71b3cd4fb315d4a556cebc9263026515ec4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-spark-cluster-in-azure-hdinsight"></a>Creare un cluster Apache Spark in Azure HDInsight

In questo articolo viene illustrato come cluster di toocreate un Apache Spark in HDInsight di Azure. Per informazioni su Spark in HDInsight, vedere [Panoramica: Apache Spark in Azure HDInsight](hdinsight-apache-spark-overview.md).

   ![Guida introduttiva diagramma che descrive i passaggi toocreate un cluster Apache Spark in Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "delle Guide rapide Spark usando Apache Spark in HDInsight. Passaggi illustrati: creare un cluster; eseguire una query interattiva Spark")

## <a name="prerequisites"></a>Prerequisiti

* **Una sottoscrizione di Azure**. Prima di iniziare questa esercitazione, è necessario disporre di un abbonamento ad Azure. Vedere [Crea subito il tuo account Azure gratuito](https://azure.microsoft.com/free).

## <a name="create-hdinsight-spark-cluster"></a>Creare un cluster HDInsight Spark

In questa sezione viene creato un cluster HDInsight Spark usando un [modello di Azure Resource Manager](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/). Per altri metodi di creazione dei cluster, vedere [Creare cluster HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

1. Fare clic su hello seguente immagine tooopen hello modello hello portale di Azure.         

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-spark-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apache-spark-jupyter-spark-sql/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. Immettere i seguenti valori hello:

    ![Creare un cluster HDInsight Spark usando un modello di Azure Resource Manager](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Creare un cluster Spark in HDInsight usando un modello di Azure Resource Manager")

    * **Sottoscrizione**: selezionare la sottoscrizione di Azure per questo cluster.
    * **Gruppo di risorse**: creare un gruppo di risorse o selezionarne uno esistente. Gruppo di risorse viene utilizzato toomanage risorse di Azure per i progetti.
    * **Percorso**: selezionare un percorso per il gruppo di risorse hello. modello Hello questo percorso viene utilizzato per la creazione di cluster hello anche come spazio di archiviazione cluster hello predefinito.
    * **ClusterName**: immettere un nome per il cluster HDInsight hello che si desidera toocreate.
    * **Versione di Spark**: selezionare **2.0** come versione di hello che si desidera tooinstall nel cluster hello.
    * **Nome account di accesso e la password del cluster**: nome di account di accesso predefinito di hello è amministratore.
    * **Nome utente e password SSH**.

   Annotare questi valori  È necessario più avanti nell'esercitazione di hello.

3. Selezionare **accetto le condizioni indicate in precedenza toohello**selezionare **Pin toodashboard**, quindi fare clic su **acquisto**. È possibile visualizzare un nuovo riquadro denominato Invio della distribuzione per Distribuzione modello. Accetta cluster hello toocreate di circa 20 minuti.

Se verifica un problema con la creazione di cluster HDInsight, è possibile che non si dispone hello delle corrette autorizzazioni toodo così. Per altre informazioni, vedere i [requisiti dei controlli di accesso](hdinsight-administer-use-portal-linux.md#create-clusters).

> [!NOTE]
> In questo articolo viene creato un cluster Spark che usa [archiviazione BLOB di archiviazione di Azure come hello del cluster](hdinsight-hadoop-use-blob-storage.md). È inoltre possibile creare un cluster Spark che usa [archivio Azure Data Lake](hdinsight-hadoop-use-data-lake-store.md) come spazio di archiviazione predefinito hello. Per istruzioni, vedere [Creare un cluster HDInsight con Archivio Data Lake](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).
>
>

## <a name="run-a-hive-query-using-spark-sql"></a>Eseguire una query Hive usando Spark SQL

Quando si utilizza un server Jupyter notebook configurato per il cluster HDInsight Spark, si ottiene un set di impostazioni `sqlContext` che è possibile utilizzare le query Hive toorun utilizzando Spark SQL. In questa sezione viene illustrato come un server Jupyter notebook toostart e quindi eseguire una query Hive base.

1. Aprire hello [portale di Azure](https://portal.azure.com/).

2. Se si è scelto di dashboard di toohello toopin hello del cluster, fare clic su riquadro cluster hello dal Pannello di hello dashboard toolaunch hello cluster.

    Se si non blocca hello cluster toohello dashboard nel riquadro di sinistra hello, fare clic su **cluster HDInsight**, quindi fare clic su cluster hello è stato creato.

3. In **Collegamenti rapidi** fare clic su **Dashboard cluster** e quindi su **Notebook di Jupyter**. Se richiesto, immettere le credenziali di amministratore hello cluster hello.

   ![Aprire Server Jupyter notebook toorun Spark SQL query interattivo](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "aprire Jupyter notebook toorun interattivo Spark nella query SQL")

   > [!NOTE]
   > È inoltre possibile accedere notebook Jupyter hello per il cluster usando hello apertura URL seguente nel browser. Sostituire **CLUSTERNAME** con nome hello del cluster:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. Creare un notebook. Fare clic su **Nuovo** e quindi su **PySpark**.

   ![Creare una query di Spark SQL interattiva Jupyter notebook toorun](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "creare una query di Spark SQL interattiva Jupyter notebook toorun")

   Un nuovo blocco appunti viene creato e aperto con il nome di hello Untitled(Untitled.pynb).

4. Fare clic sul nome di blocco per Appunti hello nella parte superiore di hello e immettere un nome descrittivo, se si desidera.

    ![Specificare un nome per hello Jupter notebook toorun Spark query interattivo da](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "specificare un nome per hello Jupter notebook toorun Spark query interattivo da")

5.  Esempio hello Incolla del codice in una cella vuota e quindi premere **MAIUSC + INVIO** codice hello toorun. Nel seguente codice hello `%%sql` (magic sql denominato hello) indica hello toouse di Jupyter notebook preimpostato `sqlContext` query Hive di hello toorun. query Hello recupera hello prime 10 righe da una tabella Hive (**hivesampletable**) che è disponibile per impostazione predefinita in tutti i cluster HDInsight.

        %%sql
        SELECT * FROM hivesampletable LIMIT 10

    ![Query Hive in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Query Hive in HDInsight Spark")

    Per ulteriori informazioni su hello `%%sql` magic e hello predefinito contesti, vedere [Jupyter kernel disponibile per un cluster HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).

    > [!NOTE]
    > Ogni volta che si esegue una query in Jupyter, il titolo della finestra del browser web viene illustrato un **(occupata)** stato insieme a titolo di hello notebook. Viene visualizzato anche un toohello Avanti cerchio pieno **PySpark** testo nell'angolo superiore destro di hello. Dopo aver completato il processo di hello, assume la forma cerchio tooa.
    >
    >
    
6. schermata Ciao necessario aggiornare l'output della query tooshow hello.

    ![Output della query Hive in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Output della query Hive in HDInsight Spark")

7. Arresto delle risorse cluster di hello notebook toorelease hello al termine dell'esecuzione di un'applicazione hello. toodo in questo caso, da hello **File** menu notebook hello, fare clic su **chiudere e interrompere**.

8. Se si prevede i passaggi successivi di toocomplete hello in un secondo momento, assicurarsi che eliminare il cluster di HDInsight hello che è stato creato in questo articolo. 

    [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-step"></a>Passaggio successivo 

In questo articolo si è appreso come cluster di toocreate un HDInsight Spark ed eseguire una base di Spark SQL eseguire una query. Spostare toohello Avanti articolo toolearn come toouse un HDInsight Spark cluster toorun interattivo query su dati di esempio.

> [!div class="nextstepaction"]
>[Eseguire query interattive in un cluster di Azure HDInsight Spark](hdinsight-apache-spark-load-data-run-query.md)



