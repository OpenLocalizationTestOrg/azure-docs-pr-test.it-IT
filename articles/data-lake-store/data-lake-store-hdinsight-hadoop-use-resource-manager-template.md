---
title: aaaUse toocreate di modelli di Azure HDInsight e archivio Data Lake | Documenti Microsoft
description: Utilizzare Gestione risorse di Azure modelli toocreate e cluster HDInsight con archivio Azure Data Lake
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8ef8152f-2121-461e-956c-51c55144919d
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: nitinme
ms.openlocfilehash: eb88a626f2837dcc29295f3f73a91757059c3bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-hdinsight-cluster-with-data-lake-store-using-azure-resource-manager-template"></a>Creare un cluster HDInsight con Data Lake Store usando un modello di Azure Resource Manager
> [!div class="op_single_selector"]
> * [Uso del portale](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Uso di PowerShell (per l'archiviazione predefinita)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Uso di PowerShell (per l'archiviazione aggiuntiva)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Utilizzo di Resource Manager](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

Informazioni su come toouse Azure PowerShell tooconfigure un HDInsight cluster con archivio Azure Data Lake **come spazio di archiviazione aggiuntivo**.

Per i tipi di cluster supportati, Data Lake Store deve essere usato come risorsa di archiviazione predefinita o come account di archiviazione aggiuntivo. Quando archivio Data Lake viene utilizzato come spazio di archiviazione aggiuntivo, account di archiviazione hello predefinito per i cluster hello saranno ancora BLOB di archiviazione di Azure (WASB) e i file correlati al cluster hello (ad esempio, i log e così via) vengono scritti ancora spazio di archiviazione predefinito di toohello, mentre quelli di hello che si desidera tooprocess possono essere archiviati in un account archivio Data Lake. Utilizzo archivio Data Lake come un account di archiviazione aggiuntive non influisce sulle prestazioni o hello possibilità tooread/scrittura toohello archiviazione dal hello cluster.

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a>Udo di Data Lake Store per l'archiviazione di cluster HDInsight

Di seguito sono riportate alcune considerazioni importanti per l'uso di HDInsight con Data Lake Store:

* Cluster di HDInsight toocreate opzione con accesso tooData Lake archivio come spazio di archiviazione predefinito è disponibile per HDInsight versione 3.5 e 3.6.

* Cluster di HDInsight toocreate opzione con accesso tooData Lake archivio come spazio di archiviazione aggiuntivo è disponibile per le versioni 3.2, 3.4, 3.5 e 3.6 di HDInsight.

In questo articolo si effettuerà il provisioning di un cluster Hadoop con Archivio Data Lake come risorsa di archiviazione aggiuntiva. Per istruzioni su come toocreate un Hadoop cluster con archivio Data Lake come spazio di archiviazione predefinito, vedere [creare un cluster HDInsight con archivio Data Lake tramite il portale di Azure](data-lake-store-hdinsight-hadoop-use-portal.md).

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questa esercitazione, è necessario disporre delle seguenti hello:

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Azure PowerShell 1.0 o versioni successive**. Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).
* **Entità servizio di Azure Active Directory**. Passaggi di questa esercitazione vengono fornite istruzioni su come toocreate un'entità servizio in Azure AD. Tuttavia, è necessario essere un toocreate di in grado di Azure AD amministratore toobe un'entità servizio. Se si è un amministratore di Azure AD, è possibile ignorare questo prerequisito e continuare l'esercitazione hello.

    **Se non si è un amministratore di Azure AD**, non sarà in grado di tooperform hello passaggi necessari toocreate un'entità servizio. In tal caso, l'amministratore di Azure AD deve creare un'entità servizio prima di creare un cluster HDInsight con l'archivio Data Lake Store. Inoltre, dell'entità servizio hello devono essere creati utilizzando un certificato, come descritto in [creare un'entità servizio con certificato](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).

## <a name="create-an-hdinsight-cluster-with-azure-data-lake-store"></a>Creare un cluster HDInsight con Azure Data Lake Store
il modello di gestione risorse di Hello e hello prerequisiti per l'utilizzo di modello hello, sono disponibili in GitHub all'indirizzo [distribuire un cluster HDInsight Linux con nuovo archivio Data Lake](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage). Istruzioni di hello fornito in questo collegamento di toocreate un cluster HDInsight con archivio Azure Data Lake come spazio di archiviazione aggiuntivo hello.

istruzioni di Hello hello collegamento indicato in precedenza richiedono PowerShell. Prima di iniziare a tali istruzioni, assicurarsi che si accede tooyour account Azure. Dal desktop, aprire una nuova finestra di PowerShell di Azure e immettere i seguenti frammenti di codice hello. Quando richiesto toolog, assicurarsi che si accede con uno dei hello admininistrators/proprietario della sottoscrizione:

```
# Log in tooyour Azure account
Login-AzureRmAccount

# List all hello subscriptions associated tooyour account
Get-AzureRmSubscription

# Select a subscription
Set-AzureRmContext -SubscriptionId <subscription ID>
```

## <a name="upload-sample-data-toohello-azure-data-lake-store"></a>Caricare l'archivio di esempio dati toohello Azure Data Lake
il modello di gestione risorse di Hello crea un nuovo account archivio Data Lake e lo associa al cluster HDInsight hello. È ora necessario caricare alcuni toohello di dati di esempio archivio Data Lake. È necessario che questi dati in un secondo momento nei processi di esercitazione toorun di hello da un cluster HDInsight che accedono ai dati in archivio Data Lake hello. Per istruzioni su come tooupload dati, vedere [caricare tooyour un file archivio Data Lake](data-lake-store-get-started-portal.md#uploaddata). Se si sta cercando alcuni tooupload di dati di esempio, è possibile ottenere hello **dati ambulanza** cartella hello [Git Repository di Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).

## <a name="set-relevant-acls-on-hello-sample-data"></a>Impostare gli ACL rilevanti nei dati di esempio hello
toomake che i dati di esempio hello caricati siano accessibili dal cluster HDInsight hello, è necessario assicurarsi che l'applicazione hello Azure AD identity tooestablish utilizzato tra cluster di HDInsight hello e archivio Data Lake ha accesso toohello file/cartella che si sta durante il tentativo tooaccess. toodo, eseguire hello alla procedura seguente.

1. Trovare il nome di hello dell'applicazione Azure AD associata al cluster HDInsight hello e hello archivio Data Lake. Un modo toolook per nome hello pannello cluster HDInsight hello di tooopen creata tramite il modello di gestione risorse di hello, fare clic su hello **identità AAD Cluster** scheda e cercare il valore di hello di **dell'entità servizio Nome visualizzato**.
2. A questo punto, fornire accesso toothis applicazione Azure AD sul hello file o sulla cartella che si desidera tooaccess dal cluster HDInsight hello. il diritto di hello tooset gli ACL sul hello file o sulla cartella in archivio Data Lake, vedere [la protezione dei dati in archivio Data Lake](data-lake-store-secure-data.md#filepermissions).

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a>Eseguire i processi di prova in hello toouse di cluster HDInsight hello archivio Data Lake
Dopo aver configurato un cluster HDInsight, è possibile eseguire i processi di prova in hello cluster tootest tale hello HDInsight cluster può accedere l'archivio Data Lake. toodo in tal caso, si verrà eseguito un processo Hive di esempio che crea una tabella utilizzando i dati di esempio hello caricato archivio precedente tooyour Data Lake.

In questa sezione sarà possibile SSH in un cluster HDInsight Linux e in esecuzione hello un esempio di query Hive. Se si usa un client Windows, è consigliabile usare **PuTTY**, disponibile per il download all'indirizzo [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

Per altre informazioni sull'uso di PuTTY, vedere [Uso di SSH con Hadoop basato su Linux in HDInsight da Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).

1. Una volta connessi, è possibile avviare hello Hive CLI utilizzando hello comando seguente:

   ```
   hive
   ```
2. Tramite hello CLI, immettere hello seguendo le istruzioni toocreate una nuova tabella denominata **veicoli** utilizzando dati di esempio hello in hello archivio Data Lake:

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   Verrà visualizzato un segue toohello simili di output:

   ```
   1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
   1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
   1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
   1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
   1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
   1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
   1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
   1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
   1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
   1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1
   ```


## <a name="access-data-lake-store-using-hdfs-commands"></a>Accedere ad Archivio Data Lake tramite comandi HDFS
Dopo aver configurato archivio Data Lake toouse cluster HDInsight hello, è possibile utilizzare hello HDFS shell comandi tooaccess hello archivio.

In questa sezione sarà possibile SSH in un cluster HDInsight Linux e in esecuzione hello comandi HDFS. Se si usa un client Windows, è consigliabile usare **PuTTY**, disponibile per il download all'indirizzo [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

Per altre informazioni sull'uso di PuTTY, vedere [Uso di SSH con Hadoop basato su Linux in HDInsight da Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).

Una volta connessi, utilizzare i seguenti file HDFS filesystem comando toolist hello in archivio Data Lake hello hello.

```
hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/
```

Vengono elencati i file hello caricato archivio precedente toohello Data Lake.

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder
```

È inoltre possibile utilizzare hello `hdfs dfs -put` comando tooupload alcuni toohello file archivio Data Lake e quindi utilizzare `hdfs dfs -ls` tooverify file hello se caricati correttamente.


## <a name="next-steps"></a>Passaggi successivi
* [Copiare i dati da un archivio Azure archiviazione BLOB tooData Lake](data-lake-store-copy-data-wasb-distcp.md)
