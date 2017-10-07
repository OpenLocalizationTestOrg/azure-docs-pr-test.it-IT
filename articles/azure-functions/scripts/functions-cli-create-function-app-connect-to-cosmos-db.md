---
title: una funzione di Azure che si connette tooan Azure Cosmos DB aaaCreate | Documenti Microsoft
description: 'Azure CLI Script di esempio: creare una funzione di Azure che si connette tooan Azure Cosmos DB'
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: 0fbc1ebec2dfd480e0cf3ca64f9febcec8af9a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-that-connects-tooan-azure-cosmos-db"></a>Creare una funzione di Azure che si connette tooan Azure Cosmos DB

Questo script di esempio crea un'App di Azure (funzione) e si connette il database di Azure Cosmos DB tooan.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script di esempio

In questo esempio crea un'app di Azure (funzione) e aggiunge un impostazioni tooapp chiave Cosmos DB endpoint e l'accesso.

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Create an Azure Function that connects tooan Azure Cosmos DB")]

## <a name="clean-up-deployment"></a>Pulire la distribuzione

Dopo l'esecuzione di script di esempio hello, comando seguire hello può essere utilizzato tooremove gruppo di risorse hello e tutte risorse correlate.

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza hello i comandi seguenti. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [az login](https://docs.microsoft.com/cli/azure/#login) | Account di accesso tooAzure. |
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Creare un gruppo di risorse con una posizione |
| [az storage account create](https://docs.microsoft.com/cli/azure/storage/account) | Creare un account di archiviazione |
| [az functionapp create](https://docs.microsoft.com/cli/azure/functionapp#create) | Creare una nuova app per le funzioni |
| [az documentdb create](https://docs.microsoft.com/cli/azure/documentdb#create) | Crea un database DocumentDB |
| [az group delete](https://docs.microsoft.com/cli/azure/group#delete) | Eseguire la pulizia |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).

Ulteriori esempi di script di Azure funzioni CLI sono reperibile in hello [documentazione di Azure funzioni](../functions-cli-samples.md).




