---
title: aaaAccess applicazione YARN Hadoop a livello di codice - log di Azure | Documenti Microsoft
description: Accedere ai log applicazioni a livello di codice su un cluster Hadoop in HDInsight.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0198d6c9-7767-4682-bd34-42838cf48fc5
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 064efee1ea6a864c29ab897692ead0152c926c0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="access-yarn-application-logs-on-windows-based-hdinsight"></a>Accesso ai log applicazioni YARN in HDInsight basato su Windows
Questo argomento viene illustrato come tooaccess hello registri per le applicazioni di YARN (ancora un'altra risorsa negoziatore) che vengono completate in un cluster basato su Windows Hadoop in HDInsight di Azure

> [!IMPORTANT]
> informazioni di Hello in questo documento si applicano solo tooWindows basato su cluster di HDInsight. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). Per informazioni sull'accesso ai log YARN in cluster HDInsight basati su Linux, vedere [Accedere ai log delle applicazioni YARN su Hadoop basato su Linux in HDInsight](hdinsight-hadoop-access-yarn-app-logs-linux.md)
>


### <a name="prerequisites"></a>Prerequisiti
* Un cluster HDInsight basato su Windows.  Vedere [Creare cluster Hadoop basati su Windows in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="yarn-timeline-server"></a>Server di sequenza temporale YARN
Hello <a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">YARN sequenza temporale Server</a> fornisce informazioni generiche in applicazioni completate anche come informazioni specifiche del framework applicazione tramite due interfacce diverse. In particolare:

* L'archiviazione e il recupero di informazioni generiche sulle applicazioni nei cluster HDInsight sono stati abilitati a partire dalla versione 3.1.1.374.
* componente di informazioni specifiche del framework applicazione Hello di hello Server sequenza temporale non è attualmente disponibile nel cluster HDInsight.

Informazioni generiche sulle applicazioni includono hello molti tipi di dati seguenti:

* ID dell'applicazione Hello, un identificatore univoco di un'applicazione
* utente Hello che ha avviato l'applicazione hello
* Informazioni sui tentativi rese applicazione hello toocomplete
* contenitori di Hello utilizzati da qualsiasi tentativo di applicazione specifico

Nei cluster di HDInsight, queste informazioni verranno archiviate dall'archivio di cronologia tooa Gestione risorse di Azure nel contenitore predefinito hello di account di archiviazione di Azure predefinito. Questi dati generici sulle applicazioni completate possono essere recuperati tramite un'API REST:

    GET on https://<cluster-dns-name>.azurehdinsight.net/ws/v1/applicationhistory/apps


## <a name="yarn-applications-and-logs"></a>Log e applicazioni YARN
YARN supporta diversi modelli di programmazione, tra cui MapReduce, separando la gestione delle risorse dalla pianificazione e dal monitoraggio dell'applicazione. A tale scopo, vengono usati un oggetto *ResourceManager* (RM) globale, oggetti *NodeManagers* (NM) per ogni nodo di lavoro e oggetti *ApplicationMasters* (AM) per ogni applicazione. Hello AM per ogni applicazione viene negoziato da risorse (CPU, memoria, disco, rete) per eseguire l'applicazione con RM. hello Hello RM funziona con toogrant NMs queste risorse, che vengono concesse a *contenitori*. è responsabile per tenere traccia dello stato di hello di hello tooit di contenitori assegnati da RM. hello Hello AM Un'applicazione potrebbe richiedere molti contenitori, a seconda della natura hello di un'applicazione hello.

Inoltre, ogni applicazione può essere costituito più *tentativi di applicazione* in ordine toofinish in presenza di hello di arresti anomali del sistema o a causa di toohello perdita di comunicazione tra un AM e un RM. Di conseguenza, i contenitori vengono concesse tooa tentativo specifici di un'applicazione. In un certo senso, un contenitore fornisce il contesto di hello per le unità di base delle operazioni eseguite da un'applicazione di YARN e tutte le operazioni che viene eseguita nel contesto di hello di un contenitore viene eseguita nel nodo singolo lavoro hello in cui hello contenitore è stato allocato. Per altri riferimenti, vedere [Concetti YARN][YARN-concepts].

Registri (registri applicazioni e hello associata contenitore) sono fondamentali per il debug di applicazioni di Hadoop problematiche. YARN fornisce un framework utile per raccogliere, aggregare e l'archiviazione dei log applicazione con hello [Log aggregazione] [ log-aggregation] funzionalità. funzione di aggregazione Log Hello rende più deterministiche, l'accesso ai log di applicazioni come aggrega i log in tutti i contenitori in un nodo di lavoro e li archivia come un aggregato file di log per ogni nodo di lavoro nel file system predefinito hello dopo il completamento di un'applicazione. L'applicazione può utilizzare centinaia o migliaia di contenitori, ma i log per tutti i contenitori devono essere eseguiti in un nodo singolo lavoro sarà sempre tooa aggregato singolo file, risultante in un file di log per ogni nodo di lavoro utilizzata dall'applicazione. Aggregazione di log è abilitato per impostazione predefinita nei cluster HDInsight (versione 3.0 e versioni successive), e aggregati i log si trovano nel contenitore predefinito hello del cluster in hello seguente posizione:

    wasb:///app-logs/<user>/logs/<applicationId>

In questa posizione, *utente* hello nome dell'utente hello che ha avviato l'applicazione hello, e *applicationId* è l'identificatore univoco di hello di un'applicazione assegnato da RM. YARN hello

Hello aggregati i registri non sono direttamente leggibili, quando vengono scritti un [TFile][T-file], [formato binario] [ binary-format] indicizzato dal contenitore. YARN fornisce CLI strumenti toodump questi log come testo normale per applicazioni o i contenitori di interesse. È possibile visualizzare questi log come testo normale eseguendo uno dei seguenti comandi YARN direttamente nei nodi del cluster hello (dopo la connessione tooit tramite RDP) hello:

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>


## <a name="yarn-resourcemanager-ui"></a>Interfaccia utente di ResourceManager YARN
Ciao YARN ResourceManager UI viene eseguito sul nodo head cluster hello e sono accessibili tramite hello dashboard del portale di Azure:

1. Accedi troppo[portale di Azure](https://portal.azure.com/).
2. Scegliere dal menu a sinistra, hello **Sfoglia**, fare clic su **cluster HDInsight**, fare clic su un cluster basato su Windows che si desidera tooaccess hello YARN registri delle applicazioni.
3. Scegliere dal menu superiore hello **Dashboard**. Verrà aperta una pagina in una nuova scheda del browser denominata **Console query HDInsight**.
4. In **HDInsight Query Console** (Console query HDInsight) fare clic su **Yarn UI** (UI YARN).

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/
