---
title: aaa "CLI di Azure Script - creazione di un Database di Azure per PostgreSQL | Documenti di Microsoft"
description: Script dell'interfaccia della riga di comando di Azure - Crea un singolo database di Azure per il server PostgreSQL e configura una regola di firewall a livello di server.
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: bbe31f77283aa4a3bb36d1fd9171c280594a8267
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-server-and-configure-a-firewall-rule-using-hello-azure-cli"></a>Creare un Database di Azure per server PostgreSQL e configurare una regola del firewall utilizzando hello CLI di Azure
Questo esempio di script dell'interfaccia della riga di comando di Azure crea un singolo database di Azure per il server PostgreSQL e configura una regola di firewall a livello di server. Una volta script hello è stato eseguito correttamente, server PostgreSQL hello accessibili da tutti i servizi di Azure e l'indirizzo IP configurato hello.

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script di esempio
In questo esempio, modificare hello evidenziato righe toocustomize hello admin username e password.
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/create-postgresql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for PostgreSQL, and server-level firewall rule.")]

## <a name="clean-up-deployment"></a>Pulire la distribuzione
Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello e tutte le risorse associate.
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/delete-postgresql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a>Spiegazione dello script
Questo script utilizza hello i comandi seguenti. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| **Comando** | **Note** |
|---|---|
| [az group create](/cli/azure/group#create) | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [az postgres server create](/cli/azure/postgres/server#create) | Crea un server PostgreSQL che ospita i database hello. |
| [az postgres server firewall create](/cli/azure/postgres/server/firewall-rule#create) | Crea un server di toohello accesso tooallow regola del firewall e di database sottostanti, dall'intervallo di indirizzi IP hello immesso. |
| [az group delete](/cli/azure/group#delete) | Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate. |

## <a name="next-steps"></a>Passaggi successivi
- Altre informazioni su hello CLI di Azure: [documentazione CLI di Azure](/cli/azure/overview)
- Provare a eseguire altri script: [esempi dell'interfaccia della riga di comando di Azure per il database di Azure per PostgreSQL](../sample-scripts-azure-cli.md)
