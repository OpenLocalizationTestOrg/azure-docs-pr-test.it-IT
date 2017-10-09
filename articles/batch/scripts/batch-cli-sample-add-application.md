---
title: aaaAzure CLI Script di esempio - aggiungere un'applicazione in Batch | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Aggiungere un'applicazione a Batch
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
ms.openlocfilehash: cb33b3a7b30610011b19954a987995cc5f0257c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="adding-applications-tooazure-batch-with-azure-cli"></a>Aggiunta di applicazioni tooAzure Batch con l'interfaccia CLI di Azure

Questo script viene illustrato come tooset di un'applicazione per l'utilizzo con un pool di Azure Batch o un'attività. tooset di un'applicazione, il file eseguibile, insieme a eventuali dipendenze, in un file zip del pacchetto. In questo eseguibile zip hello di esempio viene chiamato file ' my-applicazione-exe.zip'.

## <a name="prerequisites"></a>Prerequisiti

- Installazione hello CLI di Azure utilizzando istruzioni hello fornite nella hello [Guida all'installazione di Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), se non è già stato fatto.
- Creare un account Batch, se non è già disponibile. Vedere [creare un account Batch con hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) per uno script di esempio che crea un account.

## <a name="sample-script"></a>Script di esempio

[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]

## <a name="clean-up-application"></a>Pulizia dell'applicazione

Dopo aver eseguito hello di sopra di script di esempio, eseguire hello tooremove comandi dopo l'applicazione e tutti i relativi pacchetti applicazione caricata.

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza hello toocreate i comandi seguenti di un'applicazione e caricare un pacchetto di applicazione.
Ogni comando nella documentazione di hello tabella collegamenti toocommand specifica.

| Comando | Note |
|---|---|
| [az batch application create](https://docs.microsoft.com/cli/azure/batch/application#create) | Crea un'applicazione.  |
| [az batch application set](https://docs.microsoft.com/cli/azure/batch/application#set) | Aggiorna le proprietà di un'applicazione.  |
| [az batch application package create](https://docs.microsoft.com/cli/azure/batch/application/package#create) | Aggiunge un toohello pacchetto di applicazione specificato dell'applicazione.  |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).

Ulteriori esempi di script Batch CLI sono reperibile in hello [documentazione CLI di Azure Batch](../batch-cli-samples.md).
