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
# <a name="create-a-mysql-server-and-configure-a-firewall-rule-using-hello-azure-cli"></a><span data-ttu-id="430ac-103">Creare un server MySQL e configurare una regola del firewall utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="430ac-103">Create a MySQL server and configure a firewall rule using hello Azure CLI</span></span>
<span data-ttu-id="430ac-104">Questo script dell'interfaccia della riga di comando di Azure di esempio crea un singolo database di Azure per il server MySQL e configura una regola di firewall a livello di server.</span><span class="sxs-lookup"><span data-stu-id="430ac-104">This sample CLI script creates an Azure Database for MySQL server and configures a server-level firewall rule.</span></span> <span data-ttu-id="430ac-105">Una volta script hello viene eseguito correttamente, server MySQL hello è accessibile da tutti i servizi di Azure e l'indirizzo IP configurato hello.</span><span class="sxs-lookup"><span data-stu-id="430ac-105">Once hello script runs successfully, hello MySQL server is accessible by all Azure services and hello configured IP address.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="430ac-106">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="430ac-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="430ac-107">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="430ac-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="430ac-108">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="430ac-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="430ac-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="430ac-109">Sample script</span></span>
<span data-ttu-id="430ac-110">In questo esempio, modificare hello evidenziato righe toocustomize hello admin username e password.</span><span class="sxs-lookup"><span data-stu-id="430ac-110">In this sample script, edit hello highlighted lines toocustomize hello admin username and password.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/create-mysql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for MySQL, and server-level firewall rule.")]

## <a name="clean-up-deployment"></a><span data-ttu-id="430ac-111">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="430ac-111">Clean up deployment</span></span>
<span data-ttu-id="430ac-112">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello e tutte le risorse associate.</span><span class="sxs-lookup"><span data-stu-id="430ac-112">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/delete-mysql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="430ac-113">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="430ac-113">Script explanation</span></span>
<span data-ttu-id="430ac-114">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="430ac-114">This script uses hello following commands.</span></span> <span data-ttu-id="430ac-115">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="430ac-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="430ac-116">**Comando**</span><span class="sxs-lookup"><span data-stu-id="430ac-116">**Command**</span></span> | <span data-ttu-id="430ac-117">**Note**</span><span class="sxs-lookup"><span data-stu-id="430ac-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="430ac-118">az group create</span><span class="sxs-lookup"><span data-stu-id="430ac-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="430ac-119">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="430ac-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="430ac-120">az mysql server create</span><span class="sxs-lookup"><span data-stu-id="430ac-120">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="430ac-121">Crea un server di MySQL che ospita i database hello.</span><span class="sxs-lookup"><span data-stu-id="430ac-121">Creates a MySQL server that hosts hello databases.</span></span> |
| [<span data-ttu-id="430ac-122">az mysql server firewall create</span><span class="sxs-lookup"><span data-stu-id="430ac-122">az mysql server firewall create</span></span>](/cli/azure/mysql/server/firewall-rule#create) | <span data-ttu-id="430ac-123">Crea un server di toohello accesso tooallow regola del firewall e di database sottostanti, dall'intervallo di indirizzi IP hello immesso.</span><span class="sxs-lookup"><span data-stu-id="430ac-123">Creates a firewall rule tooallow access toohello server and databases under it from hello entered IP address range.</span></span> |
| [<span data-ttu-id="430ac-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="430ac-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="430ac-125">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="430ac-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="430ac-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="430ac-126">Next steps</span></span>
- <span data-ttu-id="430ac-127">Altre informazioni su hello CLI di Azure: [documentazione CLI di Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="430ac-127">Read more information on hello Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="430ac-128">Provare a eseguire altri script: [esempi dell'interfaccia della riga di comando di Azure per il database di Azure per MySQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="430ac-128">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
