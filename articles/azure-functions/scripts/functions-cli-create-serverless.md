---
title: aaaAzure CLI Script di esempio - creare un'App di funzione per l'esecuzione senza | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare un'app per le funzioni per l'esecuzione senza server
services: functions
documentationcenter: functions
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0e221db6-ee2d-4e16-9bf6-a456cd05b6e7
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 04/11/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 7ec872b642e50827896a73a9e43bcc87233e15c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-for-serverless-execution"></a>Creare un'app per le funzioni per l'esecuzione senza server

Questo script di esempio crea un'app per le funzioni di Azure che è un contenitore per le funzioni. Hello funzione App viene creata utilizzando hello [piano il consumo](../functions-scale.md#consumption-plan), che è ideale per basata sugli eventi senza server dei carichi di lavoro.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script di esempio

Questo script crea un'app di Azure funzione usando hello [piano il consumo](../functions-scale.md#consumption-plan).

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "Create an Azure Function on a consumption plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Spiegazione dello script

Ogni comando in documentazione specifica toocommand hello tabella collegamenti. Questo script utilizza hello seguenti comandi:

| Comando | Note |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [az storage account create](/cli/azure/storage/account#create) | Creare un account di Archiviazione di Azure. |
| [az functionapp create](https://docs.microsoft.com/cli/azure/functionapp#create) | Crea una funzione di Azure. |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).

Ulteriori esempi di script di Azure funzioni CLI sono reperibile in hello [documentazione di Azure funzioni](../functions-cli-samples.md).
