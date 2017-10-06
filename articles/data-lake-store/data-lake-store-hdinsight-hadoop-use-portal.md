---
title: cluster di hello aaaUse toocreate portale Azure HDInsight di Azure con archivio Data Lake | Documenti Microsoft
description: Utilizzare hello toocreate portale Azure e i cluster di HDInsight con archivio Azure Data Lake
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: a8c45a83-a8e3-4227-8b02-1bc1e1de6767
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: nitinme
ms.openlocfilehash: f23113d444a3c5a01894dba29f75f3621b2d16bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-by-using-hello-azure-portal"></a>Creare cluster HDInsight con archivio Data Lake tramite hello portale di Azure
> [!div class="op_single_selector"]
> * [Utilizzare hello portale di Azure](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Usare PowerShell (per l'archiviazione predefinita)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Usare PowerShell (per l'archiviazione aggiuntiva)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Usare Resource Manager](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

Informazioni su come toouse hello toocreate portale Azure un cluster di HDInsight con un account archivio Azure Data Lake come spazio di archiviazione predefinito hello o un ulteriore spazio di archiviazione. Anche se ulteriore spazio di archiviazione è facoltativa per un cluster HDInsight, è consigliabile toostore i dati di business in account di archiviazione aggiuntivi hello.

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questa esercitazione, verificare che siano soddisfatti hello seguenti requisiti:

* **Una sottoscrizione di Azure**. Andare troppo[versione di valutazione gratuita di Azure ottenere](https://azure.microsoft.com/pricing/free-trial/).
* **Un account Azure Data Lake Store**. Seguire le istruzioni di hello da [introduzione archivio Azure Data Lake tramite il portale di Azure hello](data-lake-store-get-started-portal.md). È inoltre necessario creare una cartella radice account hello.  In questa esercitazione viene usata una cartella radice denominata __/clusters__.
* **Un'entità servizio di Azure Active Directory**. In questa esercitazione vengono fornite istruzioni su come toocreate un'entità servizio in Azure Active Directory (Azure AD). Tuttavia, toocreate un'entità servizio, è necessario essere un amministratore di Azure AD. Se si è un amministratore, è possibile ignorare questo prerequisito e continuare l'esercitazione hello.

    >[!NOTE]
    >È possibile creare un'entità servizio solo se si è un amministratore di Azure AD. Prima di poter creare un cluster HDInsight con Data Lake Store, un amministratore di Azure AD deve creare un'entità servizio. Entità servizio hello deve essere creato anche con un certificato, come descritto in [creare un'entità servizio con certificato](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).
    >

## <a name="create-an-hdinsight-cluster"></a>Creazione di un cluster HDInsight

In questa sezione creare un cluster di HDInsight con account archivio Data Lake come valore predefinito di hello o spazio di archiviazione aggiuntivo hello. Questo articolo è incentrato solo parte di hello della configurazione di account archivio Data Lake.  Per informazioni sulla creazione di hello cluster generali e procedure, vedere [cluster creare Hadoop in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).

### <a name="create-a-cluster-with-data-lake-store-as-default-storage"></a>Creare un cluster con Data Lake Store come risorsa di archiviazione predefinita

**toocreate un HDInsight cluster con un archivio Data Lake come account di archiviazione predefinito hello**

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Seguire [creare cluster](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) per le informazioni generali sulla creazione di cluster HDInsight hello.
3. In hello **archiviazione** pannello, in **tipo di archiviazione primario**selezionare **archivio Data Lake**e quindi immettere hello le seguenti informazioni:

    ![Aggiungi il principale tooHDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.adls.storage.png "cluster tooHDInsight principale del componente servizio")

    - **Seleziona account Data Lake Store**: selezionare un account Data Lake Store esistente. È necessario un account Data Lake Store esistente.  Vedere [Prerequisiti](#prereuisites).
    - **Percorso radice**: immettere un percorso in cui i file specifici per i cluster hello sono toobe archiviati. Nella schermata di hello è __/cluster myhdiadlcluster/__, in cui hello __/cluster__ cartella deve essere presente e hello portale crea *myhdicluster* cartella.  Hello *myhdicluster* è il nome del cluster hello.
    - **Accesso archivio Data Lake**: configurare l'accesso tra account archivio Data Lake hello e il cluster HDInsight. Per istruzioni, vedere [Configurare l'accesso a Data Lake Store](#configure-data-lake-store-access).
    - **Account di archiviazione aggiuntivi**: aggiungere gli account di archiviazione di Azure come ulteriore spazio di archiviazione degli account per il cluster hello. tooadd aggiuntive Data Lake archivi viene eseguito, assegnando autorizzazioni cluster hello sui dati in più account archivio Data Lake durante la configurazione di un account archivio Data Lake come tipo di archiviazione primaria hello. Vedere [Configurare l'accesso a Data Lake Store](#configure-data-lake-store-access).

4. In hello **accesso archivio Data Lake**, fare clic su **selezionare**, quindi continuare con la creazione del cluster, come descritto in [cluster creare Hadoop in HDInsight](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md).


### <a name="create-a-cluster-with-data-lake-store-as-additional-storage"></a>Creare un cluster con Data Lake Store come risorsa di archiviazione aggiuntiva

Hello istruzioni riportate di seguito creare un cluster di HDInsight con un account di archiviazione di Azure come spazio di archiviazione predefinito hello e un account archivio Data Lake come un'ulteriore spazio di archiviazione.
**toocreate un HDInsight cluster con un archivio Data Lake come account di archiviazione predefinito hello**

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Seguire [creare cluster](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) per le informazioni generali sulla creazione di cluster HDInsight hello.
3. In hello **archiviazione** pannello, in **tipo di archiviazione primario**, selezionare **di archiviazione di Azure**e quindi immettere hello le seguenti informazioni:

    ![Aggiungi il principale tooHDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.png "cluster tooHDInsight principale del componente servizio")

    - **Metodo di selezione**: utilizzare una delle seguenti opzioni hello:

        * Selezionare un account di archiviazione che fa parte della sottoscrizione di Azure, toospecify **sottoscrizioni personali**, quindi selezionare l'account di archiviazione hello.
        * un account di archiviazione che non rientra nella sottoscrizione di Azure, seleziona toospecify **chiave di accesso**, quindi fornire le informazioni di hello per hello all'esterno di account di archiviazione.

    - **Contenitore predefinito**: utilizzare il valore predefinito di hello o specificare il proprio nome.

    - Altri account di archiviazione: aggiungere altri account di archiviazione di Azure come spazio di archiviazione aggiuntivo hello.
    - Accesso archivio Data Lake: configurare l'accesso tra account archivio Data Lake hello e il cluster HDInsight. Per istruzioni, vedere [Configurare l'accesso a Data Lake Store](#configure-data-lake-store-access).

## <a name="configure-data-lake-store-access"></a>Configurare l'accesso a Data Lake Store 

In questa sezione è possibile configurare l'accesso a Data Lake Store dai cluster HDInsight usando un'entità servizio di Azure Active Directory. 

### <a name="specify-a-service-principal"></a>Specificare un'entità servizio

Dal portale di Azure hello, è possibile utilizzare un'entità servizio esistente o crearne uno nuovo.

**toocreate un'entità servizio da hello portale di Azure**

1. Fare clic su **accesso archivio Data Lake** dal pannello archivio hello.
2. In hello **accesso archivio Data Lake** pannello, fare clic su **Crea nuovo**.
3. Fare clic su **dell'entità servizio**, quindi seguire le istruzioni di hello toocreate un'entità servizio.
4. Scaricare il certificato di hello se si decide di toouse nuovamente in futuro hello. Download certificato hello è utile che se si desidera toouse hello stesso servizio principale quando si crea i cluster HDInsight aggiuntivi.

    ![Aggiungi il principale tooHDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.2.png "cluster tooHDInsight principale del componente servizio")

4. Fare clic su **accesso** tooconfigure accesso alle cartelle di hello.  Vedere [Configurare le autorizzazioni file](#configure-file-permissions).


**toouse un'entità dal portale di Azure hello servizio esistente**

1. Fare clic su **Accesso a Data Lake Store**.
1. In hello **accesso archivio Data Lake** pannello, fare clic su **utilizzare esistente**.
2. Fare clic su **Entità servizio** e quindi selezionare un'entità servizio. 
3. Caricare il certificato di hello (file con estensione pfx) che ha associato l'entità servizio selezionata e quindi immettere la password del certificato hello.

    ![Aggiungi il principale tooHDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.5.png "cluster tooHDInsight principale del componente servizio")

4. Fare clic su **accesso** tooconfigure accesso alle cartelle di hello.  Vedere [Configurare le autorizzazioni file](#configure-file-permissions).


### <a name="configure-file-permissions"></a>Configurare le autorizzazioni file

Configura Hello sono diverse a seconda se account hello viene utilizzato come spazio di archiviazione predefinito hello o un account di archiviazione aggiuntive:

- Uso come risorsa di archiviazione predefinita

    - autorizzazione a livello di radice hello di hello account archivio Data Lake
    - autorizzazione a livello di radice hello di hello archiviazione cluster HDInsight. Ad esempio, hello __/cluster__ cartella utilizzata in precedenza nell'esercitazione hello.
- Uso come risorsa di archiviazione aggiuntiva

    - Autorizzazione in cartelle hello in cui è necessario accesso al file.

**autorizzazione tooassign hello a livello di radice account archivio Data Lake**

1. In hello **accesso archivio Data Lake** pannello, fare clic su **accesso**. Hello **selezionare le autorizzazioni del file** pannello viene aperto. Elenca tutti gli account archivio Data Lake hello nella sottoscrizione.
2. Passare il mouse (non selezionare) passaggio del mouse hello Nome hello di hello account archivio Data Lake toomake hello casella di controllo è visibile, quindi selezionare hello casella di controllo.

    ![Aggiungi il principale tooHDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3.png "cluster tooHDInsight principale del componente servizio")

  Per impostazione predefinita, __LETTURA__, __SCRITTURA__ ed __ESECUZIONE__ sono selezionati.

3. Fare clic su **selezionare** nella parte inferiore di hello della pagina hello.
4. Fare clic su **eseguire** tooassign autorizzazione.
5. Fare clic su **Done**.

**autorizzazione tooassign al livello radice del cluster HDInsight hello**

1. In hello **accesso archivio Data Lake** pannello, fare clic su **accesso**. Hello **selezionare le autorizzazioni del file** pannello viene aperto. Elenca tutti gli account archivio Data Lake hello nella sottoscrizione.
1. Da hello **selezionare le autorizzazioni del file** pannello, fare clic su tooshow nome di archivio Data Lake hello il relativo contenuto.
2. Selezionare una radice di archiviazione del cluster HDInsight hello selezionando la casella di controllo di hello a sinistra di hello della cartella hello. Secondo toohello schermata precedente, è radice di archiviazione cluster hello __/cluster__ cartella specificata durante la selezione di archivio Data Lake di hello come spazio di archiviazione predefinito.
3. Impostare le autorizzazioni di hello nella cartella hello.  Per impostazione predefinita, sono selezionate lettura, scrittura ed esecuzione.
4. Fare clic su **selezionare** nella parte inferiore di hello della pagina hello.
5. Fare clic su **Run**.
6. Fare clic su **Done**.

Se si utilizza l'archivio Data Lake come ulteriore spazio di archiviazione, è necessario assegnare autorizzazioni solo per le cartelle di hello che si desidera tooaccess dal cluster HDInsight hello. Ad esempio, nella schermata hello seguente permette di accedere solo troppo**hdiaddonstorage** cartella in un account archivio Data Lake.

![Assegnare i cluster di HDInsight toohello autorizzazioni dell'entità servizio](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3-1.png "cluster di HDInsight toohello autorizzazioni dell'entità servizio Assign")


## <a name="verify-cluster-set-up"></a>Verificare la configurazione del cluster

Al termine dell'installazione del cluster di hello, nel Pannello di hello cluster, verificare i risultati effettuando uno o entrambi hello alla procedura seguente:

* tooverify hello spazi di archiviazione associati per il cluster hello è account archivio Data Lake hello specificato, fare clic su **gli account di archiviazione** nel riquadro di sinistra hello.

    ![Aggiungi il principale tooHDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6-1.png "cluster tooHDInsight principale del componente servizio")

* tooverify che hello dell'entità servizio è associato correttamente al cluster HDInsight hello, fare clic su **accesso archivio Data Lake** nel riquadro di sinistra hello.

    ![Aggiungi il principale tooHDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6.png "cluster tooHDInsight principale del componente servizio")


## <a name="examples"></a>esempi

Dopo aver impostato i cluster hello con archivio Data Lake come lo spazio di archiviazione, vedere esempi toothese come toouse HDInsight cluster tooanalyze hello i dati archiviati nell'archivio Data Lake.

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-primary-storage"></a>Eseguire una query Hive sui dati archiviati in Data Lake Store (come risorsa di archiviazione primaria)

toorun una query Hive, usare l'interfaccia di viste di Hive di hello nel portale Ambari hello. Per istruzioni su come toouse Ambari Hive viste, vedere [hello utilizzare Vista Hive con Hadoop in HDInsight](../hdinsight/hdinsight-hadoop-use-hive-ambari-view.md).

Quando si lavora con i dati in un archivio Data Lake, esistono alcune stringhe toochange.

Se si utilizza, ad esempio, hello cluster che è stato creato con l'archivio Data Lake come archiviazione primaria, dati di toohello hello del percorso sono: *adl: / / < data_lake_store_account_name > /azuredatalakestore.net/path/to/file*. Un toocreate query Hive di una tabella dai dati di esempio che viene archiviati in hello account archivio Data Lake aspetto hello istruzione:

    CREATE EXTERNAL TABLE websitelog (str string) LOCATION 'adl://hdiadlsstorage.azuredatalakestore.net/clusters/myhdiadlcluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/'

Descrizioni:
* `adl://hdiadlstorage.azuredatalakestore.net/`è la radice hello di hello account archivio Data Lake.
* `/clusters/myhdiadlcluster`è hello radice dei dati di cluster hello specificato durante la creazione di cluster hello.
* `/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/`è il percorso di hello del file di esempio hello che è stato utilizzato nella query hello.

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-additional-storage"></a>Eseguire una query Hive sui dati archiviati in Data Lake Store (come risorsa di archiviazione aggiuntiva)

Se il cluster hello creato utilizza l'archiviazione Blob come spazio di archiviazione predefinito, i dati di esempio hello non sono contenuti in hello account archivio Azure Data Lake utilizzato come spazio di archiviazione aggiuntivo. In tal caso, innanzitutto trasferire dati hello da archiviazione di Blob toohello archivio Data Lake e quindi si eseguono query hello come illustrato nell'esempio sopra riportato hello.

Per informazioni sulla modalità di memorizzazione tooa Data Lake di toocopy dati dall'archiviazione Blob, vedere hello seguenti articoli:

* [Utilizzare i dati di toocopy Distcp tra BLOB di archiviazione di Azure e archivio Data Lake](data-lake-store-copy-data-wasb-distcp.md)
* [Usa AdlCopy toocopy dati da archiviazione di Azure BLOB tooData Lake archivio](data-lake-store-copy-data-azure-storage-blob.md)

### <a name="use-data-lake-store-with-a-spark-cluster"></a>Usare Data Lake Store con un cluster Spark
È possibile utilizzare un processi di Spark toorun cluster Spark sui dati archiviati in un archivio Data Lake. Per ulteriori informazioni, vedere [usare HDInsight Spark cluster tooanalyze dati archivio Data Lake](../hdinsight/hdinsight-apache-spark-use-with-data-lake-store.md).


### <a name="use-data-lake-store-in-a-storm-topology"></a>Usare Data Lake Store in una topologia Storm
È possibile utilizzare dati di hello archivio Data Lake toowrite da una topologia di Storm. Per istruzioni su come tooachieve questo scenario, vedere [archivio utilizzare Azure Data Lake con Apache Storm con HDInsight](../hdinsight/hdinsight-storm-write-data-lake-store.md).

## <a name="see-also"></a>Vedere anche
* [PowerShell: Creazione di un toouse cluster HDInsight archivio Data Lake](data-lake-store-hdinsight-hadoop-use-powershell.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
