---
title: "versione più recente tooa cluster HDInsight aaaUpgrade-Azure | Documenti Microsoft"
description: "Informazioni su come tooUpgrade HDInsight cluster tooa di versione più recente."
services: hdinsight
documentationcenter: 
author: bhanupr
manager: asadk
editor: bhanupr
ms.assetid: 60eb573c-e639-4815-9fc6-ea8b106d8dbc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/04/2017
ms.author: bhanupr
ms.openlocfilehash: 5fff3c9bc88dfbcbc1ccb0188accdfbbec3a62f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-hdinsight-cluster-tooa-newer-version"></a>L'aggiornamento di versione più recente tooa del cluster HDInsight
sfruttare tootake hello funzionalità più recenti di HDInsight, è consigliabile che il cluster HDInsight versione toolatest aggiornato. Seguire hello sotto tooupgrade linee guida per le versioni cluster HDInsight.

> [!NOTE]
> Le versioni 3.2 e 3.3 dei cluster HDInsight sono prossime alla data di ritiro. Per altre informazioni sulle versioni di HDInsight vedere [Versioni del componente HDInsight](hdinsight-component-versioning.md#supported-hdinsight-versions).
>
>

## <a name="upgrade-tasks"></a>Procedure di aggiornamento
Hello del flusso di lavoro tooupgrade HDInsight Cluster è come indicato di seguito.

![Diagramma del flusso di lavoro di aggiornamento](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. Leggere ogni sezione di questo documento toounderstand modifiche che possono essere necessari durante l'aggiornamento del cluster HDInsight.
2. Creare un cluster come ambiente di test/controllo qualità. Per ulteriori informazioni sulla creazione di un cluster, vedere [informazioni su come i cluster HDInsight basati su Linux di toocreate](hdinsight-hadoop-provision-linux-clusters.md)
3. Copia esistente processi, origini dati e sink toohello nuovo ambiente. Vedere [tooTest copia dati ambiente](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) per altri dettagli.
4. Eseguire test toomake assicurarsi che i processi di funzionano come previsto nel nuovo cluster hello di convalida.


Dopo avere verificato che tutto funzioni come previsto, pianificare i tempi di inattività per la migrazione di hello. Durante questo periodo di inattività, hello le seguenti operazioni:

1.  Eseguire il backup dei dati temporanei archiviati in locale sui nodi del cluster hello. ad esempio se i dati sono archiviati direttamente in un nodo head.
2.  Eliminare il cluster esistente hello.
3.  Creare un cluster in hello stessa rete virtuale subnet con più recente (o supportate) HDI versione utilizzando hello allo stesso archivio dati predefinito che hello precedente cluster utilizzato. In questo modo hello nuovo cluster toocontinue utilizzano i dati di produzione esistente.
4.  Importare i dati temporanei di cui è stata eseguita una copia di backup.
5.  Avvia processi/continua l'elaborazione tramite il nuovo cluster di hello.

## <a name="next-steps"></a>Passaggi successivi
* [Informazioni su come i cluster HDInsight basati su Linux di toocreate](hdinsight-hadoop-provision-linux-clusters.md)
* [Connettersi tramite SSH tooHDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)
* [Gestire un cluster basato su Linux tramite Ambari](hdinsight-hadoop-manage-ambari.md)

