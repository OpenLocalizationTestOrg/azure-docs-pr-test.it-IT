---
title: aaaUse interattivo Hive in HDInsight - Azure | Documenti Microsoft
description: Informazioni su come toouse interattivo (Hive nel LLAP) Hive in HDInsight.
keywords: 
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0957643c-4936-48a3-84a3-5dc83db4ab1a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 9e751a08091d18bc1b3d070468feef87f6828c61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a>Usare Interactive Hive in HDInsight (Anteprima)
Interactive Hive (o [Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) è un nuovo [tipo di cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) di HDInsight.  Interactive Hive consente il caching delle query Hive, rendendo le stesse molto più interattive e veloci. Questa nuova funzionalità rende HDInsight uno di hello la maggior parte delle ad alte prestazioni, flessibile e aperta Big Data le soluzioni del mondo nel cloud hello delle cache in memoria (tramite Hive e Spark) e la gestione avanzata analitica tramite una stretta integrazione con R Services. 

cluster Hive interattivo Hello è diverso da un cluster Hadoop hello. Contiene solo il servizio di Hive hello. 

> [!NOTE]
> MapReduce, Pig, Sqoop, Oozie e altri servizi saranno presto rimossi da questo cluster.
> servizio Hive nel cluster Hive interattivo hello Hello è accessibile solo tramite hello vista Ambari Hive, Beeline e Hive ODBC. Non è possibile accedervi tramite console Hive, Templeton, interfaccia della riga di comando di Azure e Azure PowerShell. 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a>Creare un cluster Interactive Hive
Il cluster Interactive Hive è supportato solo dai cluster basati su Linux. Per informazioni sulla creazione di cluster HDInsight, vedere [Creare cluster Hadoop basati su Linux in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="execute-hive-from-interactive-hive"></a>Eseguire Hive da Interactive Hive
Sono disponibili diverse opzioni per eseguire query Hive:

* Eseguire Hive utilizzando hello Ambari Hive visualizzazione
  
    Per informazioni di hello sull'utilizzo di hello Hive visualizzazione, vedere [hello utilizzare Vista Hive con Hadoop in HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).
* Eseguire Hive tramite Beeline
  
    Per informazioni di hello sull'utilizzo di Beeline in HDInsight, vedere [utilizzare Hive con Hadoop in HDInsight con Beeline](hdinsight-hadoop-use-hive-beeline.md).
  
    Utilizzare Beeline dal nodo head hello o un nodo del bordo vuoto.  È consigliabile usare Beeline da un nodo perimetrale vuoto.  Per informazioni sulla creazione di un cluster HDInsight con un nodo perimetrale vuoto, vedere [Usare nodi perimetrali vuoti in HDInsight](hdinsight-apps-use-edge-node.md).
* Eseguire Hive tramite Hive ODBC
  
    Per informazioni di hello sull'utilizzo di ODBC Hive, vedere [tooHadoop connessione Excel con il driver ODBC di Microsoft Hive hello](hdinsight-connect-excel-hive-odbc-driver.md).

**hello toofind stringa di connessione JDBC:**

1. Accedere utilizzando l'URL seguente hello tooAmbari: https://<ClusterName>. Cluster>.azurehdinsight.NET.
2. Fare clic su **Hive** dal menu a sinistra di hello.
3. Fare clic su hello evidenziato icona toocopy hello URL:
   
   ![JDBC di HDInsight Hadoop Interactive Hive LLAP](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a>Vedere anche
* [Creare i cluster basati su Linux, Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): informazioni su come i cluster toocreate interattivo Hive in HDInsight.
* [Usare l'Hive con Hadoop in HDInsight con Beeline](hdinsight-hadoop-use-hive-beeline.md): informazioni su come le query Hive di toouse Beeline toosubmit.
* [Connettere Excel tooHadoop con hello Hive di Microsoft ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md): informazioni su come tooconnect tooHive di Excel.

