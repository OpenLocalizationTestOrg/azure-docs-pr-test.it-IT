---
title: aaaUse R nel cluster di HDInsight toocustomize - Azure | Documenti Microsoft
description: Informazioni su come tooinstall R tramite Script azione e utilizzare R nei cluster HDInsight.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: be851270-afa5-4af0-a69e-2d343a4deeb7
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: bf5adf2e18dc43a743b29fd1567fad731b9c3ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-r-on-hdinsight-hadoop-clusters"></a>Installare e usare R nei cluster Hadoop HDInsight

Informazioni su come toocustomize Windows basato su cluster HDInsight con R mediante l'azione di Script e come cluster di toouse R in HDInsight. Hello [HDInsight offerta](https://azure.microsoft.com/pricing/details/hdinsight/) include R Server come parte del cluster HDInsight. In questo modo gli script R toouse MapReduce e Spark toorun distribuiti i calcoli. Per altre informazioni, vedere [Introduzione all'uso di R Server in HDInsight](hdinsight-hadoop-r-server-get-started.md). Per informazioni sull'uso di R con un cluster basato su Linux, vedere [Installare e usare R nei cluster Hadoop di HDInsight (Linux)](hdinsight-hadoop-r-scripts-linux.md).

È possibile installare R in qualsiasi tipo di cluster (Hadoop, Storm, HBase, Spark) su Azure HDInsight usando *Azione di script*. Un tooinstall di script R di esempio in un cluster HDInsight è disponibile da un blob di archiviazione di Azure di sola lettura in [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).

**Articoli correlati**

* [Installare e usare R nei cluster Hadoop di HDInsight (Linux)](hdinsight-hadoop-r-scripts-linux.md)
* [Creare cluster Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): informazioni generali sulla creazione di cluster HDInsight
* [Personalizzare cluster HDInsight mediante l'azione script][hdinsight-cluster-customize]: informazioni generali sulla personalizzazione di cluster HDInsight tramite Azione script.
* [Sviluppare script di Azione script per HDInsight](hdinsight-hadoop-script-actions.md)

## <a name="what-is-r"></a>Che cos'è R?
Hello <a href="http://www.r-project.org/" target="_blank">R progetto per l'elaborazione statistica</a> è un linguaggio open source e l'ambiente per l'elaborazione statistica. R fornisce centinaia di funzioni statistiche integrate e un proprio linguaggio che combina aspetti di programmazione funzionale con aspetti di programmazione orientata agli oggetti. Offre inoltre funzionalità complete di grafica. R è hello ambiente di programmazione preferito per più professionale statistici e gli esperti in un'ampia gamma di campi.

R è compatibile con WASB (Azure Blob Storage), consentendo di elaborare i dati archiviati usando R in HDInsight.  

## <a name="install-r"></a>Installare R
Oggetto [script di esempio](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) tooinstall R in un cluster HDInsight è disponibile da un blob di sola lettura in archiviazione di Azure. In questa sezione vengono fornite istruzioni su come toouse hello script di esempio durante la creazione di cluster di hello utilizzando hello portale di Azure.

> [!NOTE]
> script di esempio Hello è stata introdotta con versione 3.1 del cluster HDInsight. Per altre informazioni sulle versioni dei cluster HDInsight, vedere [Versioni cluster HDInsight](hdinsight-component-versioning.md).
>
>

1. Quando si crea un cluster HDInsight da hello portale, fare clic su **configurazione facoltativa**, quindi fare clic su **azioni Script**.
2. In hello **azioni Script** pagina, immettere hello seguenti valori:

    ![Utilizzare l'azione Script toocustomize un cluster](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "toocustomize azione Script Usa un cluster")

    <table border='1'>
        <tr><th>Proprietà</th><th>Valore</th></tr>
        <tr><td>Nome</td>
            <td>Specificare un nome per l'azione script hello, ad esempio, <b>installare R</b>.</td></tr>
        <tr><td>URI script</td>
            <td>Specificare uno script di toohello URI hello che è richiamato toocustomize hello cluster, ad esempio, <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></td></tr>
        <tr><td>Tipo di nodo</td>
            <td>Specificare i nodi di hello in cui viene eseguito uno script di personalizzazione di hello. È possibile scegliere <b>Tutti i nodi</b>, <b>Solo nodi head</b> o <b>Solo nodi di lavoro</b>.
        <tr><td>parameters</td>
            <td>Specificare i parametri di hello, se richiesti dallo script hello. Tuttavia, hello tooinstall di script R non richiede alcun parametro, pertanto è possibile lasciare vuoto questo.</td></tr>
    </table>

    È possibile aggiungere più di uno script azione tooinstall più componenti nel cluster hello. Dopo aver aggiunto gli script hello, fare clic su hello segno di spunta toostart creare cluster hello.

È anche possibile utilizzare hello tooinstall di script R in HDInsight tramite Azure PowerShell o hello HDInsight .NET SDK. Le istruzioni relative a queste procedure vengono fornite più avanti in questo articolo.

## <a name="run-r-scripts"></a>Eseguire gli script R
In questa sezione viene descritto come script toorun una R su hello Hadoop cluster con HDInsight.

1. **Creare un cluster di toohello connessione Desktop remoto**: da hello portale, abilitare Desktop remoto per il cluster hello è stato creato con R installato e quindi connettersi toohello cluster. Per istruzioni, vedere [connettersi tooHDInsight cluster tramite RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).
2. **Console di aprire hello R**: programma di installazione di R hello inserisce una console di R toohello collegamento sul desktop di hello del nodo head hello. Fare clic su di esso console hello R tooopen.
3. **Eseguire script R hello**: è possibile eseguire script R hello direttamente dalla console di R hello incollandoli, selezionandola e premendo INVIO. Di seguito è riportato uno script di esempio semplice che genera l'errore hello too100 di numeri da 1 e quindi vengono moltiplicati per 2.

        library(rmr2)
        library(rhdfs)
        ints = to.dfs(1:100)
        calc = mapreduce(input = ints, map = function(k, v) cbind(v, 2*v))
        from.dfs(calc)

Hello prime due righe chiamata hello RHadoop librerie che vengono installate con R. hello riga finale viene stampato hello risultati toohello console. output di Hello dovrebbe essere simile al seguente:

    [1,]  1 2
    [2,]  2 4
    .
    .
    .
    [98,]  98 196
    [99,]  99 198
    [100,] 100 200


## <a name="install-r-using-aure-powershell"></a>Installare R usando Azure PowerShell
Vedere [Personalizzare cluster HDInsight usando l'azione script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).  esempio Hello viene illustrato come tooinstall Spark con Azure PowerShell. È necessario toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).

## <a name="install-r-using-net-sdk"></a>Installare R usando .NET SDK
Vedere [Personalizzare cluster HDInsight usando l'azione script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell). esempio Hello viene illustrato come tooinstall Spark usando hello .NET SDK. È necessario toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).

## <a name="see-also"></a>Vedere anche
* [Installare e usare R nei cluster Hadoop di HDInsight (Linux)](hdinsight-hadoop-r-scripts-linux.md)
* [Creare cluster Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): informazioni generali sulla creazione di cluster HDInsight
* [Personalizzare cluster HDInsight mediante l'azione script][hdinsight-cluster-customize]: informazioni generali sulla personalizzazione di cluster HDInsight tramite Azione script.
* [Sviluppare script di Azione script per HDInsight](hdinsight-hadoop-script-actions.md)
* [Installare e usare Spark nei cluster HDInsight][hdinsight-install-spark]: esempio di Azione script sull'installazione di Spark
* [Installare e usare Spark nei cluster HDInsight](hdinsight-hadoop-giraph-install.md): esempio di Script azione sull'installazione di Giraph
* [Installare Solr nei cluster HDInsight](hdinsight-hadoop-solr-install-linux.md): esempio di Azione di script sull'installazione di Solr.

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: ../hdinsight-provision-clusters/
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
[hdinsight-install-spark]: hdinsight-apache-spark-jupyter-spark-sql.md
