---
title: aaaUse Apache Phoenix & esce con HBase - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come toouse Phoenix Apache in HDInsight e come tooinstall e configurare esce sul cluster workstation tooconnect tooan HBase in HDInsight.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: cda0f33b-a2e8-494c-972f-ae0bb482b818
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/26/2017
ms.author: jgao
ms.openlocfilehash: a63e8c8212b7a992453ec94fa638ec3863a0ede3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a>Usare Apache Phoenix con cluster HBase basati su Linux in HDinsight
Informazioni su come toouse [Phoenix Apache](http://phoenix.apache.org/) in HDInsight e come toouse SQLLine. Per altre informazioni su Phoenix, vedere la [breve panoramica su Phoenix](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html). Per hello grammatica Phoenix, vedere [grammatica Phoenix](http://phoenix.apache.org/language/index.html).

> [!NOTE]
> Per informazioni sulla versione Phoenix in HDInsight hello, vedere [novità introdotta nelle versioni di cluster Hadoop hello fornite da HDInsight?](hdinsight-component-versioning.md).
>
>

## <a name="use-sqlline"></a>Usare SQLLine
[SQLLine](http://sqlline.sourceforge.net/) è tooexecute un'utilità della riga di comando SQL.

### <a name="prerequisites"></a>Prerequisiti
Prima di poter utilizzare SQLLine, è necessario disporre delle seguenti hello:

* **Un cluster HBase in HDInsight**. Per informazioni sul provisioning di un cluster HBase, vedere l'[introduzione all'uso di Apache HBase in HDInsight][hdinsight-hbase-get-started].
* **Connettere il cluster HBase toohello tramite protocollo desktop remoto hello**. Per istruzioni, vedere [hello di cluster di gestire Hadoop in HDInsight mediante il portale di Azure][hdinsight-manage-portal].

Quando ci si connette cluster HBase tooan, è necessario tooone tooconnect di hello Zookeepers. Ogni cluster HDInsight ha tre Zookeeper.

**toofind il nome host di hello Zookeeper**

1. Aprire Ambari esplorando troppo**https://<ClusterName>. cluster>.azurehdinsight.NET**.
2. Immettere nome utente e password toologin HTTP (cluster) di hello.
3. Fare clic su **ZooKeeper** dal menu a sinistra di hello. Vengono elencate tre voci **ZooKeeper Server**.
4. Fare clic su uno di hello **ZooKeeper Server** elencati. Nel riquadro Riepilogo hello trovare hello **Hostname**. È simile troppo*zk1 jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.

**toouse SQLLine**

1. Connettere il cluster toohello tramite SSH. Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Da SSH, eseguire hello comandi toorun SQLLine seguenti:

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. Esecuzione di una tabella HBase hello toocreate i comandi seguenti e inserire alcuni dati:

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

Per altre informazioni, vedere il [manuale di SQLLine](http://sqlline.sourceforge.net/#manual) e la [grammatica Phoenix](http://phoenix.apache.org/language/index.html).

## <a name="next-steps"></a>Passaggi successivi
In questo articolo, si è appreso come toouse Phoenix Apache in HDInsight.  toolearn informazioni, vedere:

* [Panoramica di HDInsight HBase][hdinsight-hbase-overview]: HBase è un database NoSQL open source Apache basato su Hadoop che fornisce un accesso casuale e coerenza assoluta a grandi quantità di dati non strutturati e semistrutturati.
* [Eseguire il provisioning di cluster HBase in rete virtuale di Azure][hdinsight-hbase-provision-vnet]: con l'integrazione di rete virtuale cluster HBase può essere distribuito toohello stessa virtuale rete delle applicazioni in modo che le applicazioni possono comunicare con HBase direttamente.
* [Configurare la replica di HBase in HDInsight](hdinsight-hbase-replication.md): informazioni su come la replica di HBase tooconfigure tra due Data Center di Azure.
* [Analizzare Twitter sentiment con HBase in HDInsight][hbase-twitter-sentiment]: informazioni su come toodo in tempo reale [analisi del sentiment](http://en.wikipedia.org/wiki/Sentiment_analysis) dei big data dall'utilizzo di HBase in un cluster Hadoop in HDInsight.

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
