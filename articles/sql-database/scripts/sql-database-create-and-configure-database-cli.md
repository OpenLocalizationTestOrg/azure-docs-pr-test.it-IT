---
title: aaaCLI esempio-creazione di un database SQL di Azure | Documenti Microsoft
description: CLI esempio script toocreate un database SQL Azure
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 0d54e284e19f16387813e24d7beb7ab048a39263
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toocreate-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="ebb78-103">Utilizzare toocreate CLI un singolo database di SQL Azure e configurare una regola del firewall</span><span class="sxs-lookup"><span data-stu-id="ebb78-103">Use CLI toocreate a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="ebb78-104">Questo script di esempio dell'interfaccia della riga di comando di Azure crea un database SQL di Azure e configura una regola del firewall a livello di server.</span><span class="sxs-lookup"><span data-stu-id="ebb78-104">This Azure CLI script example creates an Azure SQL database and configure a server-level firewall rule.</span></span> <span data-ttu-id="ebb78-105">Una volta script hello è stato eseguito correttamente, l'indirizzo IP configurato hello che database SQL sono accessibili da tutti i servizi di Azure e hello.</span><span class="sxs-lookup"><span data-stu-id="ebb78-105">Once hello script has been successfully run, hello SQL Database can be accessed from all Azure services and hello configured IP address.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ebb78-106">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="ebb78-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ebb78-107">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="ebb78-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="ebb78-108">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ebb78-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="ebb78-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="ebb78-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ebb78-110">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="ebb78-110">Clean up deployment</span></span>

<span data-ttu-id="ebb78-111">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello e tutte le risorse associate.</span><span class="sxs-lookup"><span data-stu-id="ebb78-111">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ebb78-112">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="ebb78-112">Script explanation</span></span>

<span data-ttu-id="ebb78-113">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="ebb78-113">This script uses hello following commands.</span></span> <span data-ttu-id="ebb78-114">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="ebb78-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ebb78-115">Comando</span><span class="sxs-lookup"><span data-stu-id="ebb78-115">Command</span></span> | <span data-ttu-id="ebb78-116">Note</span><span class="sxs-lookup"><span data-stu-id="ebb78-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ebb78-117">az group create</span><span class="sxs-lookup"><span data-stu-id="ebb78-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="ebb78-118">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="ebb78-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ebb78-119">az sql server create</span><span class="sxs-lookup"><span data-stu-id="ebb78-119">az sql server create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="ebb78-120">Crea un server logico che gli host hello Database SQL.</span><span class="sxs-lookup"><span data-stu-id="ebb78-120">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="ebb78-121">az sql server firewall create</span><span class="sxs-lookup"><span data-stu-id="ebb78-121">az sql server firewall create</span></span>](/cli/azure/sql/server/firewall-rule#create) | <span data-ttu-id="ebb78-122">Crea un tooall di accesso tooallow regola firewall SQL database nel server di hello dall'intervallo di indirizzi IP hello immesso.</span><span class="sxs-lookup"><span data-stu-id="ebb78-122">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="ebb78-123">az sql db create</span><span class="sxs-lookup"><span data-stu-id="ebb78-123">az sql db create</span></span>](/cli/azure/sql/db#create) | <span data-ttu-id="ebb78-124">Crea hello Database di SQL server logico hello.</span><span class="sxs-lookup"><span data-stu-id="ebb78-124">Creates hello SQL Database in hello logical server.</span></span> |
| [<span data-ttu-id="ebb78-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="ebb78-125">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="ebb78-126">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="ebb78-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ebb78-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ebb78-127">Next steps</span></span>

<span data-ttu-id="ebb78-128">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ebb78-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ebb78-129">Ulteriori esempi di script SQL Database CLI sono reperibile in hello [documentazione relativa al Database di SQL Azure](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ebb78-129">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>

