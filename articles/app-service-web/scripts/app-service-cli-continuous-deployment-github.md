---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Creare un'App Web con distribuzione continua da GitHub | Microsoft Docs
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare un'App Web con distribuzione continua da GitHub
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0205c991-0989-4ca3-bb41-237dcc964460
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: a12085a7a8146c22d6b079381542d4fe3a8e6e87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a>Creare un'App Web con distribuzione continua da GitHub

Questo script di esempio crea un'App Web nel servizio app con le relative risorse correlate e quindi configura la distribuzione continua da un archivio GitHub. Per la distribuzione GitHub senza distribuzione continua, vedere [Creare un'App Web e distribuire il codice da GitHub](app-service-cli-deploy-github.md). In questo esempio sono necessari gli elementi seguenti:

* Repository GitHub contenente il codice dell'applicazione, con le relative autorizzazioni di amministratore.
* [Token di accesso personale](https://help.github.com/articles/creating-an-access-token-for-command-line-use) per il proprio account GitHub.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure. Eseguire `az --version` per trovare la versione. Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script di esempio

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "Creare un'App Web con distribuzione continua da GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Spiegazione dello script

Questo script usa i comandi seguenti. Ogni comando della tabella include collegamenti alla documentazione specifica del comando.

| Comando | Note |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Consente di creare un piano di servizio app. |
| [az webapp create](https://docs.microsoft.com/cli/azure/webapp#create) | Crea un'App Web di Azure. |
| [az webapp deployment source config](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | Associa un'App Web di Azure con un archivio Git o Mercurial. |
| [az webapp browse](https://docs.microsoft.com/cli/azure/webapp#browse) | Apre un'App Web di Azure in un browser. |

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).

Altri esempi di script dell'interfaccia della riga di comando del servizio app sono disponibili nella [documentazione del servizio app di Azure](../app-service-cli-samples.md).
