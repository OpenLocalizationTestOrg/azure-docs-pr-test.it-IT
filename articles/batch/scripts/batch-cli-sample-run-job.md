---
title: Esempio di Script CLI - esecuzione di un processo batch aaaAzure | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Eseguire un processo con Batch
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: f73a7cb341e550fd1c92f92201e20b27fa20d238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a>Eseguire processi in Azure Batch con l'interfaccia della riga di comando di Azure

Questo script crea un processo Batch e aggiunge una serie di processi toohello di attività. Viene inoltre illustrato come toomonitor un processo e le relative attività. Infine, Mostra come tooquery hello servizio Batch in modo efficiente per informazioni sulle attività del processo di hello.

## <a name="prerequisites"></a>Prerequisiti

- Installazione hello CLI di Azure utilizzando istruzioni hello fornite nella hello [Guida all'installazione di Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), se non è già stato fatto.
- Creare un account Batch, se non è già disponibile. Vedere [creare un account Batch con hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) per uno script di esempio che crea un account.
- Se non è ancora fatto, configurare un'applicazione toorun da un'attività di avvio. Vedere [aggiunta applicazioni tooAzure Batch con Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) per uno script di esempio che crea un'applicazione e carica un tooAzure pacchetto di applicazione.
- Configurare un pool in cui hello processo verrà eseguito. Vedere [Gestione dei pool di Azure Batch con l'interfaccia della riga di comando di Azure](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) per uno script di esempio che crea un pool con una configurazione del servizio cloud o della macchina virtuale.

## <a name="sample-script"></a>Script di esempio

[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]

## <a name="clean-up-job"></a>Pulire un processo

Dopo aver eseguito hello di sopra di script di esempio, eseguire hello tooremove comando seguendo il processo e tutte le attività. Si noti che il pool di hello sarà necessario toobe eliminata separatamente. Vedere [Gestione dei pool di Azure Batch con l'interfaccia della riga di comando di Azure](./batch-cli-sample-manage-pool.md) per altre informazioni sulla creazione e l'eliminazione di pool.

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza hello toocreate i comandi seguenti, attività e un processo Batch. Ogni comando nella documentazione di hello tabella collegamenti toocommand specifica.

| Comando | Note |
|---|---|
| [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) | Eseguire l'autenticazione con un account Batch.  |
| [az batch job create](https://docs.microsoft.com/cli/azure/batch/job#create) | Crea un processo Batch.  |
| [az batch job set](https://docs.microsoft.com/cli/azure/batch/job#set) | Aggiorna le proprietà di un processo Batch.  |
| [az batch job show](https://docs.microsoft.com/cli/azure/batch/job#show) | Recupera i dettagli di un processo Batch specificato.  |
| [az batch task create](https://docs.microsoft.com/cli/azure/batch/task#create) | Aggiunge che un toohello di attività specificato processo Batch.  |
| [az batch task show](https://docs.microsoft.com/cli/azure/batch/task#show) | Recupera i dettagli di hello di un'attività da hello specificato processo Batch.  |
| [az batch task list](https://docs.microsoft.com/cli/azure/batch/task#list) | Vengono elencate le attività di hello associate al processo specificato hello.  |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).

Ulteriori esempi di script Batch CLI sono reperibile in hello [documentazione CLI di Azure Batch](../batch-cli-samples.md).
