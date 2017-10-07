---
title: Registra aaaAccess applicazione YARN Hadoop in HDInsight basati su Linux - Azure | Documenti Microsoft
description: Informazioni su come applicazione YARN tooaccess registra in un cluster HDInsight basati su Linux (Hadoop) tramite un web browser e hello della riga di comando.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 3ec08d20-4f19-4a8e-ac86-639c04d2f12e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 0bab356e3b97114abbb05712c8e7b21a194f2508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="access-yarn-application-logs-on-linux-based-hdinsight"></a>Accedere ai log delle applicazioni YARN in HDInsight basato su Linux

Informazioni su come tooaccess hello registri per le applicazioni di YARN (ancora un'altra risorsa negoziatore) in un cluster Hadoop in HDInsight di Azure.

> [!IMPORTANT]
> passaggi di Hello in questo documento richiedono un cluster HDInsight che utilizza Linux. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere l'articolo sul [controllo delle versioni del componente di HDInsight](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="YARNTimelineServer"></a>Server di sequenza temporale YARN

Hello [YARN sequenza temporale Server](http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html) fornisce informazioni generiche su applicazioni completate e informazioni specifiche del framework applicazione tramite due interfacce diverse. In particolare:

* L'archiviazione e il recupero di informazioni generiche sulle applicazioni nei cluster HDInsight sono stati abilitati a partire dalla versione 3.1.1.374.
* componente di informazioni specifiche del framework applicazione Hello di hello Server sequenza temporale non è attualmente disponibile nel cluster HDInsight.

Informazioni generali sulla applicazioni includono hello dopo il tipo di dati:

* ID dell'applicazione Hello, un identificatore univoco di un'applicazione
* utente Hello che ha avviato l'applicazione hello
* Informazioni sui tentativi rese applicazione hello toocomplete
* contenitori di Hello utilizzati da qualsiasi tentativo di applicazione specifico

## <a name="YARNAppsAndLogs"></a>Log e applicazioni YARN

YARN supporta diversi modelli di programmazione, tra cui MapReduce, separando la gestione delle risorse dalla pianificazione e dal monitoraggio dell'applicazione. YARN usa un oggetto *ResourceManager* (RM) globale, oggetti *NodeManagers* (NM) per ogni nodo di lavoro e oggetti *ApplicationMasters* (AM) per ogni applicazione. Hello AM per ogni applicazione viene negoziato da risorse (CPU, memoria, disco, rete) per eseguire l'applicazione con RM. hello Hello RM funziona con toogrant NMs queste risorse, che vengono concesse a *contenitori*. è responsabile per tenere traccia dello stato di hello di hello tooit di contenitori assegnati da RM. hello Hello AM Un'applicazione potrebbe richiedere molti contenitori, a seconda della natura hello di un'applicazione hello.

Ogni applicazione può essere costituita da più *tentativi dell'applicazione*. Se si verifica un errore in un'applicazione, è possibile ripetere un nuovo tentativo. Ogni tentativo viene eseguito in un contenitore. In un certo senso, un contenitore fornisce il contesto di hello per le unità di base delle operazioni eseguite da un'applicazione di YARN. Tutte le operazioni che viene eseguita nel contesto di hello di un contenitore viene eseguita nel nodo singolo lavoro hello in cui hello contenitore è stato allocato. Per altri riferimenti, vedere [Concetti YARN][YARN-concepts].

Registri (registri applicazioni e hello associata contenitore) sono fondamentali per il debug di applicazioni di Hadoop problematiche. YARN fornisce un framework utile per raccogliere, aggregare e l'archiviazione dei log applicazione con hello [Log aggregazione] [ log-aggregation] funzionalità. funzione di aggregazione Log Hello rende l'accesso ai log di applicazioni più deterministiche. Aggrega i log di tutti i contenitori in un nodo di lavoro e li archivia come file di log aggregati per ogni nodo di lavoro. log di Hello viene archiviato nel file system predefinito hello dopo il completamento di un'applicazione. L'applicazione può utilizzare centinaia o migliaia di contenitori, ma i log per tutti i contenitori devono essere eseguiti in un nodo singolo lavoro sono sempre tooa aggregato file singolo. Pertanto, sarà sempre disponibile un unico log per ogni nodo di lavoro usato dall'applicazione. La funzione di aggregazione dei log è abilitata per impostazione predefinita nei cluster HDInsight versione 3.0 o successiva. Aggregati registri si trovano in archivio predefinito per il cluster hello. percorso seguito Hello è hello HDFS percorso toohello log:

    /app-logs/<user>/logs/<applicationId>

Nel percorso di hello, `user` hello nome dell'utente hello che ha avviato l'applicazione hello. Hello `applicationId` è un'applicazione tooan hello identificatore univoco assegnato da RM. YARN hello

Hello aggregati i registri non sono direttamente leggibili, quando vengono scritti un [TFile][T-file], [formato binario] [ binary-format] indicizzato dal contenitore. Utilizzare hello che ResourceManager YARN registra o CLI strumenti tooview questi log come testo normale per applicazioni o i contenitori di interesse.

## <a name="yarn-cli-tools"></a>Strumenti dell’interfaccia di riga di comando YARN

strumenti di YARN CLI hello toouse, è necessario innanzitutto connettersi cluster HDInsight toohello tramite SSH. Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

È possibile visualizzare questi log come testo normale eseguendo uno dei seguenti comandi hello:

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>

Specificare hello &lt;applicationId >, &lt;che-avvio-the-dell'applicazione utente >, &lt;ID contenitore >, e &lt;lavoratore-nodo-address > informazioni durante l'esecuzione di questi comandi.

## <a name="yarn-resourcemanager-ui"></a>Interfaccia utente di ResourceManager YARN

interfaccia utente di ResourceManager YARN Hello viene eseguito nel nodo head del cluster di hello. È possibile accedervi tramite hello Ambari web dell'interfaccia utente. Hello utilizzare seguendo i passaggi tooview hello YARN. log:

1. Nel web browser, passare toohttps://CLUSTERNAME.azurehdinsight.net. Sostituire CLUSTERNAME con nome hello del cluster HDInsight.
2. Selezionare nell'elenco dei servizi a sinistra di hello hello **YARN**.

    ![Servizio Yarn selezionato](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnservice.png)
3. Da hello **collegamenti rapidi** elenco a discesa selezionare uno dei nodi head del cluster hello e quindi **ResourceManager Log**.

    ![Collegamenti rapidi Yarn](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnquicklinks.png)

    Viene visualizzata con un elenco di collegamenti tooYARN log.

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/
