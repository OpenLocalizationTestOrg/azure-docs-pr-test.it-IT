---
title: aaaAzure CLI Script di esempio - creare un account Batch | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare un account Batch
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
ms.openlocfilehash: 62b640eebbafdd1081822a638fd0720121ef067a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-cli"></a>Creare un account Batch con hello CLI di Azure

Questo script crea un account Azure Batch e viene illustrato come le varie proprietà dell'account di hello possono eseguire query e aggiornate.

## <a name="prerequisites"></a>Prerequisiti

Installazione hello CLI di Azure utilizzando istruzioni hello fornite nella hello [Guida all'installazione di Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), se non è già stato fatto.

## <a name="batch-account-sample-script"></a>Script di esempio per un account Batch

Quando si crea un account Batch, per impostazione predefinita i relativi nodi calcolo assegnati internamente dal servizio Batch hello. Nodi di calcolo allocato sarà una quota di core separato tooa soggetto e account hello possono essere autenticati tramite le credenziali di autenticazione chiave condivisa o un token di Azure Active deve.

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]

## <a name="batch-account-using-user-subscription-sample-script"></a>Account Batch con lo script di esempio della sottoscrizione utente

È inoltre possibile scegliere toohave Batch creare nodi di calcolo nella sottoscrizione Azure.
Gli account che allocano calcolano nodi nella sottoscrizione devono essere autenticati tramite un token di Azure Active Directory e i nodi di calcolo hello allocati verranno considerato come uno la quota della sottoscrizione. toocreate un account in questa modalità, uno deve specificare un riferimento di chiave dell'insieme di credenziali durante la creazione di account hello.

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]

## <a name="clean-up-deployment"></a>Pulire la distribuzione

Dopo aver eseguito uno di hello sopra gli script di esempio, eseguire hello successivo comando tooremove il gruppo di risorse e tutte le relative risorse (inclusi gli account Batch, gli account di archiviazione di Azure e insiemi di credenziali chiave di Azure).

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza hello seguenti comandi toocreate un gruppo di risorse, l'account di Batch e tutte le relative risorse. Ogni comando nella documentazione di hello tabella collegamenti toocommand specifica.

| Comando | Note |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [az batch account create](https://docs.microsoft.com/cli/azure/batch/account#create) | Crea account Batch hello.  |
| [az batch account set](https://docs.microsoft.com/cli/azure/batch/account#set) | Aggiorna le proprietà di hello account Batch.  |
| [az batch account show](https://docs.microsoft.com/cli/azure/batch/account#show) | Recupera i dettagli di hello specificato l'account Batch.  |
| [az batch account keys list](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | Recupera le chiavi di accesso hello di hello specificato l'account Batch.  |
| [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) | Esegue l'autenticazione con hello specificato per l'interazione di CLI ulteriormente l'account Batch.  |
| [az storage account create](https://docs.microsoft.com/cli/azure/storage/account#create) | Crea un account di archiviazione. |
| [az keyvault create](https://docs.microsoft.com/cli/azure/keyvault#create) | Crea un insieme di credenziali chiave. |
| [az keyvault set-policy](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | Aggiornare i criteri di sicurezza hello dell'insieme di credenziali di chiave specificato hello. |
| [az group delete](https://docs.microsoft.com/cli/azure/group#delete) | Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate. |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).

Ulteriori esempi di script Batch CLI sono reperibile in hello [documentazione CLI di Azure Batch](../batch-cli-samples.md).
