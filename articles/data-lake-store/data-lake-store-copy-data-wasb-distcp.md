---
title: aaaCopy dati tooand da WASB in archivio Data Lake tramite Distcp | Documenti Microsoft
description: Utilizzare Distcp strumento toocopy dati tooand dall'archivio di Azure archiviazione BLOB tooData Lake
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ae2e9506-69dd-4b95-8759-4dadca37ea70
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: ec23410bbab0f82449a475412bc3b097c4a8fccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-distcp-toocopy-data-between-azure-storage-blobs-and-data-lake-store"></a>Utilizzare i dati di toocopy Distcp tra il BLOB di archiviazione di Azure e archivio Data Lake
> [!div class="op_single_selector"]
> * [Con DistCp](data-lake-store-copy-data-wasb-distcp.md)
> * [Con AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)
>
>

Dopo aver creato un cluster HDInsight che dispone di un account di accesso tooa archivio Data Lake, è possibile usare strumenti di ecosistema Hadoop come dati toocopy Distcp **tooand da** un'archiviazione del cluster HDInsight (WASB) in un account archivio Data Lake. In questo articolo vengono fornite istruzioni su come tooachieve questo.

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questo articolo, è necessario disporre delle seguenti hello:

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Un account Azure Data Lake Store**. Per istruzioni su come toocreate uno, vedere [introduzione archivio Azure Data Lake](data-lake-store-get-started-portal.md)
* **Cluster di Azure HDInsight** con accesso tooa account archivio Data Lake. Vedere [Creare un cluster HDInsight con Data Lake Store tramite il portale di Azure](data-lake-store-hdinsight-hadoop-use-portal.md). Assicurarsi di abilitare Desktop remoto per il cluster hello.

## <a name="do-you-learn-fast-with-videos"></a>Apprendimento rapido con i video
[Guardare questo video](https://mix.office.com/watch/1liuojvdx6sie) sulla toocopy dati tra il BLOB di archiviazione di Azure e archivio Data Lake tramite DistCp.

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a>Usare Distcp da un cluster HDInsight Linux

Un cluster HDInsight viene fornito con l'utilità Distcp hello, che può essere utilizzato toocopy dati provenienti da origini diverse in un cluster HDInsight. Se è stata configurata l'archivio Data Lake toouse cluster HDInsight hello come un'ulteriore spazio di archiviazione, hello Distcp utilità può essere utilizzato di casella toocopy tooand di dati da un account archivio Data Lake anche. In questa sezione verranno esaminate come toouse hello Distcp utilità.

1. Dal desktop, usare SSH tooconnect toohello cluster. Vedere [cluster HDInsight basati su Linux di Connect tooa](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md). Eseguire i comandi di hello dal prompt dei comandi di hello SSH.

2. Verificare se sia possibile accedere hello BLOB di archiviazione di Azure (WASB). Eseguire hello comando seguente:

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    Ciò dovrebbe fornire un elenco del contenuto nel blob di archiviazione hello.
3. Analogamente, verificare se è possibile accedere hello account archivio Data Lake dal cluster hello. Eseguire hello comando seguente:

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    Ciò dovrebbe fornire un elenco di file e cartelle in hello account archivio Data Lake.
4. Utilizzare dati toocopy Distcp WASB tooa account archivio Data Lake.

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    Verranno copiati contenuto hello di hello **esempio/data/gutenberg/** cartella WASB troppo**/myfolder** in hello account archivio Data Lake.
5. Analogamente, utilizzare dati toocopy Distcp tooWASB account archivio Data Lake.

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    Verranno copiati contenuto hello di **/myfolder** in archivio Data Lake hello account troppo**esempio/data/gutenberg/** cartella WASB.

## <a name="performance-considerations-while-using-distcp"></a>Considerazioni sulle prestazioni per l'uso di DistCp

Poiché DistCp's più basso granularità è un singolo file, impostazione hello massimo del numero di copie simultanee è hello più importante parametro toooptimize è in archivio Data Lake. Questa funzionalità è controllata impostando il numero di hello di BizTalk Mapper (sto ') del parametro nella riga di comando hello. Questo parametro specifica numero massimo di hello di BizTalk Mapper che verrà utilizzato toocopy dati. Il valore predefinito è 20.

**Esempio**

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-hello-number-of-mappers-toouse"></a>Come è possibile determinare il numero di hello di BizTalk Mapper toouse?

Ecco alcune linee guida che è possibile usare.

* **Passaggio 1: Determinare il totale memoria YARN** -hello primo passaggio consiste cluster disponibili toohello toodetermine hello YARN memoria in cui viene eseguito il processo di DistCp hello. Queste informazioni sono disponibili nel portale di Ambari hello associato hello cluster. Passare tooYARN e visualizzare hello configurazioni scheda toosee hello YARN memoria. tooget hello YARN memoria totale, moltiplicare hello memoria YARN per ogni nodo con il numero di hello di nodi nel cluster di cui si dispone.

* **Passaggio 2: Calcolare il numero di hello di BizTalk Mapper** -hello valore **m** è il quoziente toohello uguale totale di memoria YARN diviso hello dimensione del contenitore YARN. informazioni sulle dimensioni YARN contenitore Hello è disponibile nel portale nonché di hello Ambari. Passare tooYARN e hello di scheda configurazioni di visualizzazione hello dimensione del contenitore YARN viene visualizzato in questa finestra. Hello tooarrive equazione numero hello di BizTalk Mapper (**m**) è

        m = (number of nodes * YARN memory for each node) / YARN container size

**Esempio**

Si supponga di avere un 4 nodi D14v2s cluster hello e che si sta tentando di tootransfer 10TB di dati da 10 cartelle diverse. Ciascuna delle cartelle hello contenere quantità variabili di dati e delle dimensioni del file hello all'interno di ogni cartella sono diverse.

* Memoria totale di YARN - dal portale Ambari si determina che la memoria YARN hello hello è 96GB per un nodo D14. Pertanto, la memoria totale di YARN per un cluster a 4 nodi è: 

        YARN memory = 4 * 96GB = 384GB

* Numero di BizTalk Mapper - dal portale Ambari è determinare la dimensione del contenitore YARN hello 3072 per un nodo del cluster D14 hello. Il numero di mapper è quindi:

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

Se altre applicazioni utilizzano memoria, quindi è possibile utilizzare tooonly una parte della memoria YARN del cluster per DistCp.

### <a name="copying-large-datasets"></a>Copia di set di dati di grandi dimensioni

Le dimensioni hello di hello dataset toobe spostate è molto grande (ad esempio > 1TB) o se si dispone di molte cartelle diverse, è consigliabile utilizzare più processi DistCp. Non è probabile alcun miglioramento delle prestazioni, ma verrà distribuito processi hello in modo che se un processo non riesce, sarà sufficiente toorestart tale processo specifico anziché l'intero processo di hello.

### <a name="limitations"></a>Limitazioni

* DistCp tenta toocreate Mapper delle prestazioni toooptimize dimensioni simili. Aumentare il numero di hello BizTalk Mapper non può sempre aumentare le prestazioni.

* DistCp è limitato tooonly uno mapper per ogni file. quindi non è possibile avere più mapper che file. Poiché DistCp possibile assegnare solo un mapping tooa file, ciò limita quantità hello di concorrenza che può essere utilizzati toocopy file di grandi dimensioni.

* Se si dispone di un numero ridotto di file di grandi dimensioni, quindi è consigliabile dividerli in toogive blocchi di file da 256MB è maggiore concorrenza potenziale. 
 
* Se si copia da un account di archiviazione Blob di Azure, il processo di copia può essere limitato sul lato di archiviazione blob di hello. Si riducono le prestazioni di hello del processo di copia. toolearn ulteriori informazioni sui limiti di hello dell'archiviazione Blob di Azure, vedere i limiti di archiviazione di Azure in [sottoscrizione di Azure e limiti dei servizi](../azure-subscription-service-limits.md).

## <a name="see-also"></a>Vedere anche
* [Copiare i dati da un archivio Azure archiviazione BLOB tooData Lake](data-lake-store-copy-data-azure-storage-blob.md)
* [Proteggere i dati in Data Lake Store](data-lake-store-secure-data.md)
* [Usare Azure Data Lake Analytics con Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Usare Azure HDInsight con Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
