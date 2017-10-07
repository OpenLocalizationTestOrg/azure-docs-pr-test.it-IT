---
title: aaaAzure CLI Script di esempio - Gestione pool in Batch | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Gestione dei pool in Batch
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
ms.openlocfilehash: 6c9ca9515565aff42752231a080943be8e4c810b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a>Gestione dei pool di Azure Batch con l'interfaccia della riga di comando di Azure

Questi script vengono illustrate alcune delle strumenti hello disponibili in hello Azure CLI toocreate e gestire pool di nodi di calcolo nel servizio Azure Batch hello.

> [!NOTE]
> i comandi di Hello in questo esempio creano macchine virtuali di Azure. Macchine virtuali in esecuzione trarrà account tooyour addebiti. toominimize questi addebiti, eliminare le macchine virtuali hello dopo averli: esempio hello in esecuzione. Vedere [Eseguire la pulizia dei pool](#clean-up-pools).

È possibile configurare i pool di Batch in due modi: con una configurazione Servizi cloud (solo Windows) o con una configurazoine Macchina virtuale (Windows e Linux). script di esempio Hello seguenti mostrano come toocreate pool con entrambe le configurazioni.

## <a name="prerequisites"></a>Prerequisiti

- Installazione hello CLI di Azure utilizzando istruzioni hello fornite nella hello [Guida all'installazione di Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), se non è già stato fatto.
- Creare un account Batch, se non è già disponibile. Vedere [creare un account Batch con hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) per uno script di esempio che crea un account.
- Se non è ancora fatto, configurare un'applicazione toorun da un'attività di avvio. Vedere [aggiunta applicazioni tooAzure Batch con Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) per uno script di esempio che crea un'applicazione e carica un tooAzure pacchetto di applicazione.

## <a name="pool-with-cloud-service-configuration-sample-script"></a>Script di esempio per un pool con configurazione Servizi cloud

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]

## <a name="pool-with-virtual-machine-configuration-sample-script"></a>Script di esempio per un pool con configurazione Macchina virtuale

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]

## <a name="clean-up-pools"></a>Eseguire la pulizia dei pool

Dopo aver eseguito hello di sopra di script di esempio, eseguire hello seguente pool hello toodelete di comando.
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza i seguenti comandi toocreate hello e modificare i pool di Batch.
Ogni comando nella documentazione di hello tabella collegamenti toocommand specifica.

| Comando | Note |
|---|---|
| [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) | Eseguire l'autenticazione con un account Batch.  |
| [az batch application summary list](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | Elencare le applicazioni disponibili hello in hello account Batch.  |
| [az batch pool create](https://docs.microsoft.com/cli/azure/batch/pool#create) | Creare un pool di macchine virtuali.  |
| [az batch pool set](https://docs.microsoft.com/cli/azure/batch/pool#set) | Aggiornare le proprietà di un pool.  |
| [az batch pool node-agent-skus list](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | Elencare gli SKU agente nodo disponibili e le informazioni dell'immagine.  |
| [az batch pool resize](https://docs.microsoft.com/cli/azure/batch/pool#resize) | Numero di hello di ridimensionamento di macchine virtuali in esecuzione in hello specificato pool.  |
| [az batch pool show](https://docs.microsoft.com/cli/azure/batch/pool#show) | Visualizzare le proprietà di hello di un pool.  |
| [az batch pool delete](https://docs.microsoft.com/cli/azure/batch/pool#delete) | Eliminare hello specificato pool.  |
| [az batch pool autoscale enable](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | Abilitare la scalabilità automatica in un pool e applicare una formula.  |
| [az batch pool autoscale disable](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | Disabilitare la scalabilità automatica in un pool.  |
| [az batch node list](https://docs.microsoft.com/cli/azure/batch/node#list) | Elencare tutti il nodo di calcolo hello in hello specificato pool.  |
| [az batch node reboot](https://docs.microsoft.com/cli/azure/batch/node#reboot) | Riavviare il nodo di calcolo specificata di hello.  |
| [az batch node delete](https://docs.microsoft.com/cli/azure/batch/node#delete) | I nodi di hello elencato Delete da hello specificati pool.  |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).

Ulteriori esempi di script Batch CLI sono reperibile in hello [documentazione CLI di Azure Batch](../batch-cli-samples.md).

