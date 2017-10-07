---
title: esempio di aaaCLI ridimensiona un Database SQL Azure di pool elastico SQL | Documenti Microsoft
description: Azure CLI esempio script tooscale un pool elastico SQL nel Database di SQL Azure
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 436128b8183213f78b9abc2ec46efe2a3ed3c37c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-tooscale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="e22a0-103">Utilizzare tooscale CLI un pool elastico SQL nel Database di SQL Azure</span><span class="sxs-lookup"><span data-stu-id="e22a0-103">Use CLI tooscale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="e22a0-104">Questo script di esempio dell'interfaccia della riga di comando di Azure crea pool elastici SQL, sposta i database in pool e modifica i livelli di prestazioni del pool elastico.</span><span class="sxs-lookup"><span data-stu-id="e22a0-104">This Azure CLI script example creates SQL elastic pools, moves pooled databases, and changes elastic pool performance levels.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e22a0-105">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="e22a0-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e22a0-106">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="e22a0-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="e22a0-107">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e22a0-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="e22a0-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="e22a0-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e22a0-109">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="e22a0-109">Clean up deployment</span></span>

<span data-ttu-id="e22a0-110">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello e tutte le risorse associate.</span><span class="sxs-lookup"><span data-stu-id="e22a0-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="e22a0-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="e22a0-111">Script explanation</span></span>

<span data-ttu-id="e22a0-112">Questo script utilizza hello seguenti comandi toocreate un gruppo di risorse, server logico, Database SQL e le regole del firewall.</span><span class="sxs-lookup"><span data-stu-id="e22a0-112">This script uses hello following commands toocreate a resource group, logical server, SQL Database, and firewall rules.</span></span> <span data-ttu-id="e22a0-113">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="e22a0-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e22a0-114">Comando</span><span class="sxs-lookup"><span data-stu-id="e22a0-114">Command</span></span> | <span data-ttu-id="e22a0-115">Note</span><span class="sxs-lookup"><span data-stu-id="e22a0-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e22a0-116">az group create</span><span class="sxs-lookup"><span data-stu-id="e22a0-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e22a0-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="e22a0-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e22a0-118">az sql server create</span><span class="sxs-lookup"><span data-stu-id="e22a0-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="e22a0-119">Crea un server logico che gli host hello Database SQL.</span><span class="sxs-lookup"><span data-stu-id="e22a0-119">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="e22a0-120">az sql elastic-pools create</span><span class="sxs-lookup"><span data-stu-id="e22a0-120">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="e22a0-121">Crea un pool di database elastico all'interno di server logico hello.</span><span class="sxs-lookup"><span data-stu-id="e22a0-121">Creates an elastic database pool within hello logical server.</span></span> |
| [<span data-ttu-id="e22a0-122">az sql db create</span><span class="sxs-lookup"><span data-stu-id="e22a0-122">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="e22a0-123">Crea hello Database di SQL server logico hello.</span><span class="sxs-lookup"><span data-stu-id="e22a0-123">Creates hello SQL Database in hello logical server.</span></span> |
| [<span data-ttu-id="e22a0-124">az sql elastic-pools update</span><span class="sxs-lookup"><span data-stu-id="e22a0-124">az sql elastic-pools update</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#update) | <span data-ttu-id="e22a0-125">Aggiorna un pool di database elastico, in questo hello modifiche esempio assegnato eDTU.</span><span class="sxs-lookup"><span data-stu-id="e22a0-125">Updates an elastic database pool, in this example changes hello assigned eDTU.</span></span> |
| [<span data-ttu-id="e22a0-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="e22a0-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="e22a0-127">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="e22a0-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e22a0-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e22a0-128">Next steps</span></span>

<span data-ttu-id="e22a0-129">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e22a0-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e22a0-130">Ulteriori esempi di script SQL Database CLI sono reperibile in hello [documentazione relativa al Database di SQL Azure](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e22a0-130">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
