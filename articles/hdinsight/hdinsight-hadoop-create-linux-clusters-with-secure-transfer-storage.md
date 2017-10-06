---
title: aaaCreate Hadoop cluster con gli account di archiviazione di protezione del trasferimento in Azure HDInsight | Documenti Microsoft
description: Informazioni su come i cluster di HDInsight toocreate con protezione del trasferimento di abilitare gli account di archiviazione di Azure.
keywords: introduzione a Hadoop,Hadoop basato su Linux,guida introduttiva a Hadoop,trasferimento sicuro,account di archiviazione di Azure
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: jgao
ms.openlocfilehash: 0acb8814ad0d5d5b5652d930b2e3da90f9d7978d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-cluster-with-secure-transfer-storage-accounts-in-azure-hdinsight"></a>Creare un cluster Hadoop con account di archiviazione con trasferimento sicuro in Azure HDInsight

Hello [necessario trasferimento sicuro](../storage/common/storage-require-secure-transfer.md) funzionalità migliora la sicurezza hello dell'account di archiviazione di Azure tramite l'applicazione di tutti i conti tooyour richieste tramite una connessione protetta. Questo schema wasbs funzionalità e hello sono supportati solo dalla versione del cluster HDInsight 3.6 o versioni successive. 

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questa esercitazione, è necessario avere:

* **Sottoscrizione di Azure**: toocreate un mese di un account di prova, è esplorare troppo[azure.microsoft.com/free](https://azure.microsoft.com/free).
* **Account di archiviazione di Azure con trasferimento sicuro abilitato**. Per istruzioni hello, vedere [creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) e [richiedono il trasferimento protetto](../storage/common/storage-require-secure-transfer.md).
* **Un contenitore Blob nell'account di archiviazione hello**. 
## <a name="create-cluster"></a>Creare cluster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]


In questa sezione viene creato un cluster Hadoop in HDInsight usando un [modello di Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). modello Hello nella [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/). Per questa esercitazione non è necessario conoscere il modello di Resource Manager. Per altri metodi di creazione del cluster e informazioni sulle proprietà hello utilizzate in questa esercitazione, vedere [cluster HDInsight creare](hdinsight-hadoop-provision-linux-clusters.md).

1. Fare clic su hello seguente immagine toosign in tooAzure e il modello di gestione risorse hello Apri nel portale di Azure hello. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-existing-default-storage-account%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. Segue hello istruzioni toocreate hello cluster con hello seguenti specifiche: 

    - Specificare HDInsight versione 3.6.  versione predefinita di Hello è 3.5. È necessaria la versione 3.6 o successiva.
    - Specificare un account di archiviazione con trasferimento sicuro abilitato.
    - Utilizzare un nome breve per l'account di archiviazione hello.
    - Account di archiviazione hello sia il contenitore di blob hello deve essere create in precedenza. 

    Per istruzioni hello, vedere [Crea cluster](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster). 

Se si utilizzano script azione tooprovide dei file di configurazione, è necessario utilizzare wasbs in hello seguenti impostazioni:

- fs.defaultFS (core-site)
- spark.eventLog.dir 
- spark.history.fs.logDirectory

## <a name="add-additional-storage-accounts"></a>Aggiungere altri account di archiviazione

Sono disponibili diverse opzioni tooadd account di archiviazione aggiuntive trasferimento sicuro abilitato:

- Modificare il modello di Azure Resource Manager hello nell'ultima sezione hello.
- Creare un cluster utilizzando hello [portale di Azure](https://portal.azure.com) e specificare l'account di archiviazione collegato.
- Utilizzare script azione tooadd aggiuntive il trasferimento protetto è abilitato il cluster HDInsight esistente di storage account tooan.  Per ulteriori informazioni, vedere [aggiungere ulteriore spazio di archiviazione account tooHDInsight](hdinsight-hadoop-add-storage.md).

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione, si è appreso come toocreate un cluster HDInsight e abilitare protezione trasferire account di archiviazione toohello.

toolearn più sull'analisi dei dati con HDInsight, vedere hello seguenti articoli:

* toolearn ulteriori informazioni sull'utilizzo di Hive con HDInsight, incluso come una query Hive tooperform da Visual Studio, vedere [utilizzare Hive con HDInsight][hdinsight-use-hive].
* toolearn su Pig, un linguaggio tootransform dati, vedere [usare Pig con HDInsight][hdinsight-use-pig].
* toolearn su MapReduce, un toowrite programmi che elaborano i dati in Hadoop, vedere [utilizzare MapReduce con HDInsight][hdinsight-use-mapreduce].
* toolearn sull'uso di strumenti di HDInsight hello per i dati di Visual Studio tooanalyze in HDInsight, vedere [iniziare a usare gli strumenti di Visual Studio Hadoop per HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).

altre informazioni sulle modalità di archiviazione dati HDInsight toolearn o dati tooget in HDInsight, vedere hello seguenti articoli:

* Per informazioni sul modo in cui HDInsight usa Archiviazione di Azure, vedere [Usare Archiviazione di Azure con HDInsight](hdinsight-hadoop-use-blob-storage.md).
* Per informazioni su come tooupload tooHDInsight di dati, vedere [caricare dati tooHDInsight][hdinsight-upload-data].

toolearn più sulla creazione o la gestione di un cluster HDInsight, vedere hello seguenti articoli:

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


