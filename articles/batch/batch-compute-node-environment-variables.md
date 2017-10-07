---
title: aaa "variabili di ambiente nodo di calcolo di Azure Batch | Documenti di Microsoft"
description: Riferimento variabile di ambiente del nodo di calcolo per le analisi di Azure Batch.
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/05/2017
ms.author: tamram
ms.openlocfilehash: 860f34b530579a81fbd5cf8ffa31df79d917c080
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-batch-compute-node-environment-variables"></a>Variabili di ambiente per i nodi di calcolo di Azure Batch
Hello [servizio Azure Batch](https://azure.microsoft.com/services/batch/) imposta hello seguenti variabili di ambiente nei nodi di calcolo. È possibile fare riferimento a queste variabili di ambiente nelle righe di comando di attività e nei programmi hello e gli script eseguiti per le righe di comando hello.

Per altre informazioni sull'uso delle variabili di ambiente con Batch, vedere [Impostazioni di ambiente per le attività](https://docs.microsoft.com/azure/batch/batch-api-basics#environment-settings-for-tasks).

## <a name="environment-variable-visibility"></a>Visibilità delle variabili di ambiente

Queste variabili di ambiente sono visibili solo nel contesto di hello di hello **utente dell'attività**, hello account utente nel nodo hello in cui viene eseguita un'attività. Sarà possibile *non* vedere questi se si [connettersi in remoto](https://azure.microsoft.com/documentation/articles/batch-api-basics/#connecting-to-compute-nodes) tooa nodo tramite Remote Desktop Protocol (RDP) o Secure Shell (SSH) e l'elenco di variabili di ambiente hello di calcolo. Infatti, account utente di hello che viene utilizzato per la connessione remota non è hello come account hello utilizzato dall'attività hello.

## <a name="command-line-expansion-of-environment-variables"></a>Espansione delle variabili di ambiente della riga di comando

righe di comando Hello eseguite dalle attività in calcolo nodi non vengono eseguiti in una shell. Pertanto, queste righe di comando non è possibile in modo nativo sfruttare funzionalità della shell, ad esempio l'espansione di variabili di ambiente (inclusi hello `PATH`). Il vantaggio di tootake di tali funzionalità, è necessario **richiamare shell hello** nella riga di comando hello. Avviare ad esempio `cmd.exe` su nodi di calcolo Windows o `/bin/sh` su nodi Linux:

`cmd /c MyTaskApplication.exe %MY_ENV_VAR%`

`/bin/sh -c MyTaskApplication $MY_ENV_VAR`

## <a name="environment-variables"></a>Variabili di ambiente

| Nome variabile                     | Descrizione                                                              | Disponibilità | Esempio |
|-----------------------------------|--------------------------------------------------------------------------|--------------|---------|
| AZ_BATCH_ACCOUNT_NAME           | Hello nome dell'account Batch hello hello attività a cui appartiene.                  | Tutte le attività.   | mybatchaccount |
| AZ_BATCH_CERTIFICATES_DIR       | Una directory all'interno di hello [directory di lavoro attività] [ files_dirs] nodi di calcolo in cui i certificati vengono archiviati per Linux. Si noti che questa variabile di ambiente non si applicano tooWindows nodi di calcolo.                                                  | Tutte le attività.   |  /mnt/batch/tasks/workitems/batchjob001/job-1/task001/certs |
| AZ_BATCH_JOB_ID                 | ID di Hello hello del processo di cui hello attività a cui appartiene. | Tutte le attività tranne l'attività di avvio. | batchjob001 |
| AZ_BATCH_JOB_PREP_DIR           | percorso completo di Hello di preparazione del processo hello [directory attività] [ files_dirs] nel nodo hello. | Tutte le attività ad eccezione dell'attività di preparazione del processo e dell'attività di avvio. È disponibile solo se il processo di hello è configurato con un'attività di preparazione del processo. | C:\user\tasks\workitems\jobprepreleasesamplejob\job-1\jobpreparation |
| AZ_BATCH_JOB_PREP_WORKING_DIR   | percorso completo di Hello di preparazione del processo hello [directory di lavoro attività] [ files_dirs] nel nodo hello. | Tutte le attività ad eccezione dell'attività di preparazione del processo e dell'attività di avvio. È disponibile solo se il processo di hello è configurato con un'attività di preparazione del processo. | C:\user\tasks\workitems\jobprepreleasesamplejob\job-1\jobpreparation\wd |
| AZ_BATCH_NODE_ID                | Hello ID di nodo hello hello attività viene assegnato a. | Tutte le attività. | tvm-1219235766_3-20160919t172711z |
| AZ_BATCH_NODE_ROOT_DIR          | percorso completo di Hello della radice hello tutti [Batch directory] [ files_dirs] nel nodo hello. | Tutte le attività. | C:\user\tasks |
| AZ_BATCH_NODE_SHARED_DIR        | percorso completo di Hello di hello [directory condivisa] [ files_dirs] nel nodo hello. Tutte le attività eseguite in un nodo dispone di accesso di lettura/scrittura toothis directory. Le attività eseguite in altri nodi non presentano directory toothis di accesso remoto (non è una directory di rete "condivise"). | Tutte le attività. | C:\user\tasks\shared |
| AZ_BATCH_NODE_STARTUP_DIR       | percorso completo di Hello di hello [avviare directory attività] [ files_dirs] nel nodo hello. | Tutte le attività. | C:\user\tasks\startup |
| AZ_BATCH_POOL_ID                | ID di Hello del pool di hello hello attività è in esecuzione. | Tutte le attività. | batchpool001 |
| AZ_BATCH_TASK_DIR               | percorso completo di Hello di hello [directory attività] [ files_dirs] nel nodo hello. Questa directory contiene hello `stdout.txt` e `stderr.txt` per attività hello e hello AZ_BATCH_TASK_WORKING_DIR. | Tutte le attività. | C:\user\tasks\workitems\batchjob001\job-1\task001 |
| AZ_BATCH_TASK_ID                | Hello l'ID dell'attività corrente di hello. | Tutte le attività tranne l'attività di avvio. | task001 |
| AZ_BATCH_TASK_WORKING_DIR       | percorso completo di Hello di hello [directory di lavoro attività] [ files_dirs] nel nodo hello. Hello attualmente in esecuzione attività dispone di accesso di lettura/scrittura toothis directory. | Tutte le attività. | C:\user\tasks\workitems\batchjob001\job-1\task001\wd |
| CCP_NODES                       | elenco di Hello di nodi e numero di core per nodo allocati tooa [attività multi-istanza][multi_instance]. I nodi e core sono elencati in formato hello`numNodes<space>node1IP<space>node1Cores<space>`<br/>`node2IP<space>node2Cores<space> ...`, dove il numero di hello di nodi è seguito da uno o più indirizzi IP e numero hello di core per ogni. |  Principale multi-istanza e sottoattività. |`2 10.0.0.4 1 10.0.0.5 1` |
| AZ_BATCH_NODE_LIST              | elenco di Hello dei nodi che vengono allocati tooa [attività multi-istanza] [ multi_instance] in formato hello `nodeIP;nodeIP`. | Principale multi-istanza e sottoattività. | `10.0.0.4;10.0.0.5` |
| AZ_BATCH_HOST_LIST              | elenco di Hello dei nodi che vengono allocati tooa [attività multi-istanza] [ multi_instance] in formato hello `nodeIP,nodeIP`. | Principale multi-istanza e sottoattività. | `10.0.0.4,10.0.0.5` |
| AZ_BATCH_MASTER_NODE            | Hello indirizzo IP e porta di hello nodo di calcolo in attività hello primario di un [attività multi-istanza] [ multi_instance] viene eseguito. | Principale multi-istanza e sottoattività. | `10.0.0.4:6000`|
| AZ_BATCH_TASK_SHARED_DIR | Un percorso di directory che è identico per l'attività principale hello e ogni sottoattività di un [attività multi-istanza][multi_instance]. Hello percorso esista in ogni nodo in cui si esegue attività di multi-istanza hello ed è di lettura/scrittura toohello accessibili i comandi di attività in esecuzione su quel nodo (entrambi hello [comando coordinamento] [ coord_cmd] e hello [comando applicazione][app_cmd]). Sottoattività o un'attività principale eseguite in altri nodi non dispone di una directory toothis di accesso remoto (non è una directory di rete "condivise"). | Principale multi-istanza e sottoattività. | C:\user\tasks\workitems\multiinstancesamplejob\job-1\multiinstancesampletask |
| AZ_BATCH_IS_CURRENT_NODE_MASTER | Specifica se hello nodo corrente non sia hello master per un [attività multi-istanza][multi_instance]. I valori possibili sono `true` e `false`.| Principale multi-istanza e sottoattività. | `true` |
| AZ_BATCH_NODE_IS_DEDICATED | Se `true`, hello di nodo corrente è di dedicato. Se `false`, è un [nodo con priorità bassa](batch-low-pri-vms.md). | Tutte le attività. | `true` |

[files_dirs]: https://azure.microsoft.com/documentation/articles/batch-api-basics/#files-and-directories
[multi_instance]: https://azure.microsoft.com/documentation/articles/batch-mpi/
[coord_cmd]: https://azure.microsoft.com/documentation/articles/batch-mpi/#coordination-command
[app_cmd]: https://azure.microsoft.com/documentation/articles/batch-mpi/#application-command
