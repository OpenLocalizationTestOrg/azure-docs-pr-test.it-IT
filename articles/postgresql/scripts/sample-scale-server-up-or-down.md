---
title: aaa "Database Azure Script scala CLI di Azure per PostgreSQL | Documenti di Microsoft"
description: "Azure CLI Script di esempio - Database Azure scalabilità a livello di prestazioni diverse PostgreSQL server tooa dopo l'esecuzione di query metriche hello."
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: 678b28941dbb4334cb374d4888991a00b44966b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-scale-a-single-postgresql-server-using-azure-cli"></a>Monitorare e scalare un singolo server PostgreSQL tramite l'interfaccia della riga di comando di Azure
Questo script di esempio CLI ridimensiona un singolo Database di Azure a livello di prestazioni diverse PostgreSQL server tooa dopo l'esecuzione di query metriche hello. 

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script di esempio
In questo esempio, modificare hello evidenziato righe toocustomize hello admin username e password. Sostituire l'id sottoscrizione hello utilizzato nei comandi di monitoraggio az hello con il proprio id sottoscrizione.[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Create and scale Azure Database for PostgreSQL.")]

## <a name="clean-up-deployment"></a>Pulire la distribuzione
Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello e tutte le risorse associate.
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/delete-postgresql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a>Spiegazione dello script
Questo script utilizza hello i comandi seguenti. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| **Comando** | **Note** |
|---|---|
| [az group create](/cli/azure/group#create) | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [az postgres server create](/cli/azure/postgres/server#create) | Crea un server PostgreSQL che ospita i database hello. |
| [az monitor metrics list](/cli/azure/monitor/metrics#list) | Elenco hello valore metrico per le risorse di hello. |
| [az group delete](/cli/azure/group#delete) | Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate. |

## <a name="next-steps"></a>Passaggi successivi
- Altre informazioni su hello CLI di Azure: [documentazione CLI di Azure](/cli/azure/overview)
- Provare a eseguire altri script: [esempi dell'interfaccia della riga di comando di Azure per il database di Azure per PostgreSQL](../sample-scripts-azure-cli.md)
- Altre informazioni sul ridimensionamento: [Livelli di servizio](../concepts-service-tiers.md) e [Unità di calcolo e unità di archiviazione](../concepts-compute-unit-and-storage.md)
