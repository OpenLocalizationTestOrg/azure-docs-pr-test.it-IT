---
title: i cluster Hadoop aaaCreate con PowerShell - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come toocreate Hadoop, HBase, Storm o Spark cluster Linux per HDInsight tramite Azure PowerShell.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4208deca-d64a-45e1-8948-2673d5d7678c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 53afe4702f6b61a0720ceda48a4a34d7fa8797d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a>Creare cluster basati su Linux in HDInsight tramite Azure PowerShell

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Azure PowerShell è un ambiente di scripting potente che è possibile utilizzare toocontrol e automatizzare la distribuzione di hello e la gestione dei carichi di lavoro in Microsoft Azure. Questo documento fornisce informazioni su come toocreate un HDInsight basati su Linux cluster tramite Azure PowerShell. Include anche uno script di esempio.

> [!NOTE]
> Azure PowerShell è disponibile solo su client Windows. Se si utilizza un client Mac OS X, Linux o Unix, vedere [creare un cluster HDInsight basati su Linux mediante Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) per informazioni sull'utilizzo di hello Azure CLI toocreate un cluster.

## <a name="prerequisites"></a>Prerequisiti
È necessario disporre delle seguenti hello prima di iniziare questa procedura:

* Una sottoscrizione di Azure. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* [Azure PowerShell](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > Il supporto di Azure PowerShell per la gestione delle risorse HDInsight tramite Azure Service Manager è **deprecato** ed è stato rimosso dal 1° gennaio 2017. Hello passaggi in questo documento usa hello nuovi cmdlet di HDInsight che funzionano con Gestione risorse di Azure.
    >
    > Eseguire le operazioni di hello in [installare Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooinstall hello più recente di Azure PowerShell. Se si dispone di script che toobe necessità modificato toouse hello nuovi cmdlet che funzionano con Gestione risorse di Azure, vedere [di strumenti di migrazione tooAzure sviluppo basato su Gestione risorse per i cluster HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) per ulteriori informazioni.

## <a name="create-cluster"></a>Creare cluster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

toocreate un cluster HDInsight tramite Azure PowerShell, è necessario completare hello seguire le procedure seguenti:

* Creare un gruppo di risorse di Azure
* Creare un account di Archiviazione di Azure
* Creazione di un contenitore BLOB di Azure
* Creazione di un cluster HDInsight

Hello script riportato di seguito viene illustrato come toocreate un nuovo cluster:

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]

i valori di Hello specificati per l'account di accesso cluster hello sono utilizzati toocreate hello account utente Hadoop per il cluster hello. Utilizzare questo tooservices tooconnect account ospitate nel cluster di hello, ad esempio web le interfacce utente o le API REST.

valori Hello specificati per l'utente SSH hello sono utilizzati toocreate hello SSH utente cluster hello. Utilizzare questo account toostart una sessione SSH remota in cluster hello ed eseguire i processi. Per ulteriori informazioni, vedere hello [utilizzo di SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.

> [!IMPORTANT]
> Se si prevede di toouse più di 32 nodi di lavoro (al momento della creazione del cluster o hello scalabilità del cluster dopo la creazione), è necessario specificare anche una dimensione del nodo head con almeno 8 core e 14 GB di RAM.
>
> Per altre informazioni sulle dimensioni di nodo e i costi associati, vedere [Prezzi di HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

Potrebbe essere necessaria fino too20 minuti toocreate un cluster.

## <a name="create-cluster-configuration-object"></a>Creare il cluster: oggetto di configurazione

È anche possibile creare un oggetto di configurazione di HDInsight tramite il cmdlet `New-AzureRmHDInsightClusterConfig`. È quindi possibile modificare questa configurazione oggetto tooenable ulteriori opzioni di configurazione per il cluster. Infine, utilizzare hello `-Config` parametro di hello `New-AzureRmHDInsightCluster` configurazione hello toouse di cmdlet.

Hello script seguente crea un tooconfigure oggetto di configurazione Server R sul tipo di cluster HDInsight. configurazione di Hello consente un nodo del bordo, RStudio e un account di archiviazione aggiuntivi.

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]

> [!WARNING]
> Non è supportato l'utilizzo di un account di archiviazione in un percorso diverso da quello del cluster HDInsight hello. Quando si utilizza questo esempio, creare account di archiviazione aggiuntivo hello in hello stesso percorso server hello.

## <a name="customize-clusters"></a>Personalizzare i cluster

* Vedere [Personalizzare cluster HDInsight tramite Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).
* Vedere [Personalizzare cluster HDInsight usando l'azione script](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="delete-hello-cluster"></a>Eliminare il cluster hello

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Risoluzione dei problemi

Se si verificano problemi di creazione dei cluster HDInsight, vedere i [requisiti dei controlli di accesso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Passaggi successivi

Ora che è stato creato correttamente un cluster HDInsight, utilizzare hello seguenti come risorse toolearn toowork con il cluster.

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

