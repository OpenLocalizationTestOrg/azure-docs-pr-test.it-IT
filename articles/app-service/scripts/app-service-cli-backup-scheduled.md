---
title: 'Azure CLI Script di esempio: creare un backup pianificato per un''app web | Documenti Microsoft'
description: 'Azure CLI Script di esempio: creare un backup pianificato per un''app web'
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
tags: azure-service-management
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 12/11/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: fe5d2ca6fe5327f40adf134e94cf9b00ad98d243
ms.sourcegitcommit: aaba209b9cea87cb983e6f498e7a820616a77471
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-scheduled-backup-for-a-web-app"></a>Creare un backup pianificato per un'app Web

Questo script di esempio crea un'app web nel servizio App con le relative risorse correlate e quindi crea un backup pianificato per il. 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se si sceglie di installare e utilizzare l'interfaccia CLI in locale, è necessario Azure CLI versione 2.0 o versione successiva. Per trovare la versione, eseguire `az --version`. Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script di esempio

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/backup-scheduled/backup-scheduled.sh?highlight=3-7 "Create a scheduled backup for a web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Spiegazione dello script

Questo script usa i comandi seguenti. Ogni comando della tabella include collegamenti alla documentazione specifica del comando.

| Comando | Note |
|---|---|
| [`az group create`](/cli/azure/group?view=azure-cli-latest#az_group_create) | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [`az storage account create`](/cli/azure/storage/account?view=azure-cli-latest#az_storage_account_create) | Crea un account di archiviazione. |
| [`az storage container create`](/cli/azure/storage/container?view=azure-cli-latest#az_storage_container_create) | Crea un contenitore di Archiviazione di Azure. |
| [`az storage container generate-sas`](/cli/azure/storage/container?view=azure-cli-latest#az_storage_container_generate_sas) | Genera un token di firma di accesso condiviso per un contenitore di archiviazione di Azure.  |
| [`az appservice plan create`](/cli/azure/appservice/plan?view=azure-cli-latest#az_appservice_plan_create) | Consente di creare un piano di servizio app. |
| [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az_webapp_create) | Crea un'App Web di Azure. |
| [`az webapp config backup update`](/cli/azure/webapp/config/backup?view=azure-cli-latest#az_webapp_config_backup_update) | Configura una nuova pianificazione di backup per un'app web. |
| [`az webapp config backup show`](/cli/azure/webapp/config/backup?view=azure-cli-latest#az_webapp_config_backup_show) | Mostra la pianificazione del backup per un'app web. |
| [`az webapp config backup list`](/cli/azure/webapp/config/backup?view=azure-cli-latest#az_webapp_config_backup_list) | Ottiene un elenco di copie di backup per un'app Web. |

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).

Altri esempi di script dell'interfaccia della riga di comando del servizio app sono disponibili nella [documentazione del servizio app di Azure](../app-service-cli-samples.md).
