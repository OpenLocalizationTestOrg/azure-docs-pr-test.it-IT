---
title: aaa "CLI di Azure Script - creazione di un Database di Azure per MySQL | Documenti di Microsoft"
description: Questo script dell'interfaccia della riga di comando di Azure di esempio crea un singolo database di Azure per il server MySQL e configura una regola di firewall a livello di server.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: 1d619ee0547efd8275eaf7c1347b6c3427025c3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-mysql-server-and-configure-a-firewall-rule-using-hello-azure-cli"></a>Creare un server MySQL e configurare una regola del firewall utilizzando hello CLI di Azure
Questo script dell'interfaccia della riga di comando di Azure di esempio crea un singolo database di Azure per il server MySQL e configura una regola di firewall a livello di server. Una volta script hello viene eseguito correttamente, server MySQL hello è accessibile da tutti i servizi di Azure e l'indirizzo IP configurato hello.

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script di esempio
In questo esempio, modificare hello evidenziato righe toocustomize hello admin username e password.
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/create-mysql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for MySQL, and server-level firewall rule.")]

## <a name="clean-up-deployment"></a>Pulire la distribuzione
Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello e tutte le risorse associate.
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/delete-mysql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a>Spiegazione dello script
Questo script utilizza hello i comandi seguenti. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| **Comando** | **Note** |
|---|---|
| [az group create](/cli/azure/group#create) | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [az mysql server create](/cli/azure/mysql/server#create) | Crea un server di MySQL che ospita i database hello. |
| [az mysql server firewall create](/cli/azure/mysql/server/firewall-rule#create) | Crea un server di toohello accesso tooallow regola del firewall e di database sottostanti, dall'intervallo di indirizzi IP hello immesso. |
| [az group delete](/cli/azure/group#delete) | Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate. |

## <a name="next-steps"></a>Passaggi successivi
- Altre informazioni su hello CLI di Azure: [documentazione CLI di Azure](/cli/azure/overview).
- Provare a eseguire altri script: [esempi dell'interfaccia della riga di comando di Azure per il database di Azure per MySQL](../sample-scripts-azure-cli.md)
