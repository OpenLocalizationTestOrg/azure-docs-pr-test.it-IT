---
title: pianificazione di applicazione di patch aaaConfigure del sistema operativo per i cluster HDInsight basati su Linux - Azure | Documenti Microsoft
description: Informazioni su come cluster di pianificazione di applicazione di patch tooconfigure del sistema operativo per HDInsight basati su Linux.
services: hdinsight
documentationcenter: 
author: bprakash
manager: asadk
editor: bprakash
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: bhanupr
ms.openlocfilehash: 1598d64e594d7e8a68573fc63dd86051a5a9d025
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="os-patching-for-hdinsight"></a>Applicazione di patch del sistema operativo per HDInsight 
Come un servizio gestito di Hadoop, HDInsight si occupa del processo di hello del sistema operativo di hello macchine virtuali sottostanti usate dai cluster di HDInsight. A partire dal 1 agosto 2016, sono stati modificati criteri applicazione di patch del sistema operativo guest di hello per i cluster HDInsight basati su Linux (versione 3.4 o successiva). obiettivo di Hello del nuovo criterio di hello è toosignificantly ridurre il numero di riavvii di hello toopatching scadenza. il nuovo criterio di Hello continuerà toopatch virtuali (VM) in Linux cluster ogni lunedì o giovedì a partire da Mezzanotte ora UTC in un termineranno tra i nodi del cluster specificato. Tuttavia, tutte le VM determinata riavvierà solo al massimo una volta ogni 30 giorni a causa del sistema operativo tooguest l'applicazione di patch. Inoltre, il primo riavvio hello per un cluster appena creato non si verificherà prima di 30 giorni dalla data di creazione di cluster hello. Patch è efficace quando le macchine virtuali hello vengono riavviate.

## <a name="how-tooconfigure-hello-os-patching-schedule-for-linux-based-hdinsight-clusters"></a>Come tooconfigure hello pianificazione patch del sistema operativo per i cluster HDInsight basati su Linux
macchine virtuali Hello in un cluster HDInsight è necessario toobe riavviato in alcuni casi, in modo che sia possono installare le patch di sicurezza importante. A partire dal 1 agosto 2016, nuovi cluster HDInsight basati su Linux (versione 3.4 o versioni successive) vengono riavviati utilizzando hello seguente pianificazione:

1. Una macchina virtuale in cluster hello solo possibile riavviare le patch al massimo una volta all'interno di un periodo di 30 giorni.
2. il riavvio di Hello si verifica a partire da Mezzanotte UTC.
3. il processo di riavvio Hello avviene a fasi su macchine virtuali nel cluster hello, in modo cluster hello è ancora disponibile durante il processo di riavvio hello.
4. il primo riavvio Hello per un cluster appena creato non verrà eseguito prima di 30 giorni dopo la data di creazione cluster hello.

Utilizzando l'azione di script hello descritta in questo articolo, è possibile modificare pianificazione patch hello del sistema operativo come indicato di seguito:
1. Abilitare o disabilitare il riavvio automatico
2. Frequenza di hello set di riavvio (giorni tra i riavvii)
3. Impostare hello giorno della settimana hello quando si verifica un riavvio

> [!NOTE]
> Questa azione di script funziona solo con i cluster HDInsight basati su Linux creati dopo il 1° agosto 2016. I patch verranno applicati solo al riavvio delle macchine virtuali. 
>

## <a name="how-toouse-hello-script"></a>Come toouse hello script 

Quando questo script richiede hello le seguenti informazioni:
1. percorso dello script Hello: https://hdiconfigactions.blob.core.windows.net/linuxospatchingrebootconfigv01/os-patching-reboot-config.sh.  HDInsight utilizza toofind questo URI ed eseguire script hello in tutte le macchine virtuali hello cluster hello.
  
2. tipi di nodo del cluster è applicare lo script hello Hello: nodo head, workernode, zookeeper. Questo script deve essere applicato tooall i tipi di nodo nel cluster hello. Se non è il tipo di nodo tooa applicati, quindi hello virtuale macchine per quel tipo di nodo continueranno pianificazione delle patch di toouse hello precedente.


3.  Parametro: Questo script accetta tre parametri numerici:

    | Parametro | Definizione |
    | --- | --- |
    | Abilitare/disabilitare il riavvio automatico |0 o 1. Il valore 0 disabilita il riavvio automatico, mentre 1 consente il riavvio automatico. |
    | Frequenza |too90 7 (inclusivo). numero di Hello di toowait giorni prima di riavviare le macchine virtuali di hello per le patch che richiedono un riavvio. |
    | Giorno della settimana |1 too7 (inclusivo). Il valore 1 indica il riavvio di hello deve essere eseguiti su un lunedì e 7 indica un esempio di Sunday.For, utilizzando i parametri di 1 60 2 risultati in automatico viene riavviato ogni 60 giorni (al massimo) martedì. |
    | Persistenza |Quando l'applicazione di un cluster di script azione tooan esistente, è possibile contrassegnare script hello come persistente. Script persistenti vengono applicate quando workernodes nuovo vengono aggiunti il cluster toohello tramite operazioni di ridimensionamento. |

> [!NOTE]
> È necessario contrassegnare questo script come persistente quando l'applicazione cluster esistente tooan. In caso contrario, eventuali nuovi nodi creati tramite operazioni di ridimensionamento utilizzerà l'applicazione di patch pianificazione predefinito di hello.
Se si applica script hello come parte del processo di creazione cluster di hello, viene mantenuta automaticamente.
>

## <a name="next-steps"></a>Passaggi successivi

Per passaggi specifici sull'utilizzo di azione script hello, vedere le sezioni in hello seguenti hello [HDInsight basati su personalizzare Linuz cluster utilizzando l'azione script](hdinsight-hadoop-customize-cluster-linux.md):

* [Usare un'azione script durante la creazione di un cluster](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation)
* [Applicare un tooa azione script in esecuzione del cluster](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster)
