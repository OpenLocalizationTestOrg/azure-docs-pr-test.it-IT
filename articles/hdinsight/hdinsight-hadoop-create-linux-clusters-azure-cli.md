---
title: i cluster Hadoop aaaCreate tramite riga di comando - hello Azure HDInsight | Documenti Microsoft
description: Informazioni su come i cluster HDInsight toocreate usando hello multipiattaforma Azure CLI 1.0.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 50b01483-455c-4d87-b754-2229005a8ab9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 5295b01054b8c23df0e3b75a3e0e8c933ac48b3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-using-hello-azure-cli"></a>Creare il cluster HDInsight tramite hello CLI di Azure

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Hello passaggi in questa procedura dettagliata documento creazione di un cluster HDInsight 3.5 utilizzando hello Azure CLI 1.0.

> [!IMPORTANT]
> Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).


## <a name="prerequisites"></a>Prerequisiti

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* **Interfaccia della riga di comando di Azure**. passaggi di Hello in questo documento sono stati testati ultima con versione 0.10.14 CLI di Azure.

    > [!IMPORTANT]
    > passaggi di Hello in questo documento non funzionano con l'interfaccia CLI di Azure 2.0. L'interfaccia della riga di comando di Azure 2.0 non supporta la creazione di un cluster HDInsight.

## <a name="log-in-tooyour-azure-subscription"></a>Accedi tooyour sottoscrizione di Azure

Seguire i passaggi di hello documentati in [connettersi tooan sottoscrizione di Azure da hello interfaccia della riga di comando di Azure (Azure CLI)](../xplat-cli-connect.md) e connettersi tooyour sottoscrizione utilizzando hello **accesso** (metodo).

## <a name="create-a-cluster"></a>Creare un cluster

Hello alla procedura seguente deve essere eseguita dalla riga di comando, ad esempio PowerShell o Bash.

1. Utilizzare hello successivo comando tooauthenticate tooyour sottoscrizione di Azure:

        azure login

    Si è tooprovide richiesto il nome e la password. Se si dispone di più sottoscrizioni di Azure, utilizzare `azure account set <subscriptionname>` sottoscrizione hello tooset hello CLI di Azure, i comandi usano.

2. Passare in modalità di gestione risorse tooAzure utilizzando hello comando seguente:

        azure config mode arm

3. Creare un gruppo di risorse. Il gruppo di risorse cluster HDInsight hello e account di archiviazione associato.

        azure group create groupname location

    * Sostituire `groupname` con un nome univoco per il gruppo di hello.

    * Sostituire `location` con area geografica hello che si desidera che il gruppo di hello toocreate in.

       Per un elenco di percorsi validi, utilizzare hello `azure location list` comandi e quindi utilizzare uno dei percorsi di hello da hello `Name` colonna.

4. Creare un account di archiviazione. Questo account di archiviazione viene utilizzato come spazio di archiviazione di hello predefinito per il cluster HDInsight hello.

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * Sostituire `groupname` con nome hello del gruppo di hello creato nel passaggio precedente hello.

    * Sostituire `location` con hello nello stesso percorso utilizzato nel passaggio precedente hello.

    * Sostituire `storagename` con un nome univoco per l'account di archiviazione hello.

        > [!NOTE]
        > Per ulteriori informazioni sui parametri hello utilizzati in questo comando, utilizzare `azure storage account create -h` tooview della Guida in linea per questo comando.

5. Recuperare l'account di archiviazione hello hello chiave tooaccess utilizzato.

        azure storage account keys list -g groupname storagename

    * Sostituire `groupname` con nome gruppo di risorse hello.
    * Sostituire `storagename` con nome hello hello dell'account di archiviazione.

     Nei dati hello che viene restituiti, salvare hello `key` valore per `key1`.

6. Creare un cluster HDInsight

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 3 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * Sostituire `groupname` con nome gruppo di risorse hello.

    * Sostituire `Hadoop` con tipo di cluster hello che si desidera toocreate. ad esempio, `Hadoop`, `HBase`, `Kafka`, `Spark` o `Storm`.

     > [!IMPORTANT]
     > HDInsight cluster possono essere di vario tipo, che corrispondono a carico di lavoro toohello o tecnologia di hello cluster è ottimizzata per. Non è toocreate alcun metodo supportato per un cluster che combina più tipi, ad esempio Storm e HBase in un cluster.

    * Sostituire `location` con hello nello stesso percorso utilizzato nei passaggi precedenti.

    * Sostituire `storagename` con nome di account di archiviazione hello.

    * Sostituire `storagekey` con chiave hello ottenuta nel passaggio precedente hello.

    * Per hello `--defaultStorageContainer` parametro, utilizzare hello stesso nome che si utilizzi per i cluster di hello.

    * Sostituire `admin` e `httppassword` con nome hello e una password desiderato toouse quando si accede a cluster hello tramite HTTPS.

    * Sostituire `sshuser` e `sshuserpassword` con hello username e password desiderato toouse quando si accede a cluster hello tramite SSH

    > [!IMPORTANT]
    > L'esempio precedente crea un cluster con 2 nodi di ruolo di lavoro. È inoltre possibile modificare il numero di hello di nodi di lavoro dopo la creazione del cluster eseguendo le operazioni di ridimensionamento. Se si prevede di usare più di 32 nodi del ruolo di lavoro, è necessario selezionare una dimensione del nodo head con almeno 8 core e 14 GB di RAM. È possibile impostare le dimensioni di un nodo head hello utilizzando hello `--headNodeSize` parametro durante la creazione del cluster.
    >
    > Per altre informazioni sulle dimensioni di nodo e i costi associati, vedere [Prezzi di HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

    Potrebbe richiedere alcuni minuti per hello cluster creazione processo toofinish. in genere circa 15.

## <a name="troubleshoot"></a>Risoluzione dei problemi

Se si verificano problemi di creazione dei cluster HDInsight, vedere i [requisiti dei controlli di accesso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Passaggi successivi

Ora che la creazione di un cluster HDInsight tramite hello CLI di Azure è stata completata, utilizzare hello seguente come toolearn toowork con il cluster:

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
