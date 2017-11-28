---
title: pool elastico SQL database SQL di Azure esempio spostamento aaaCLI | Documenti Microsoft
description: Azure CLI esempio script toomove un database SQL in un pool elastico SQL
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
ms.date: 07/05/2017
ms.author: janeng
ms.openlocfilehash: 841eb57d2d49612c3fadd3a6424a2b0309c69719
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toomove-an-azure-sql-database-in-a-sql-elastic-pool"></a><span data-ttu-id="154eb-103">Utilizzare toomove CLI un database SQL di Azure in un pool elastico SQL</span><span class="sxs-lookup"><span data-stu-id="154eb-103">Use CLI toomove an Azure SQL database in a SQL elastic pool</span></span>

<span data-ttu-id="154eb-104">In questo esempio di script CLI di Azure crea due pool elastico e sposta un database SQL di Azure da un pool elastico SQL in un altro pool elastico SQL e quindi si sposta il database di hello all'esterno di livello di prestazioni di pool elastico tooa singolo database di Azure.</span><span class="sxs-lookup"><span data-stu-id="154eb-104">This Azure CLI script example creates two elastic pools and moves an Azure SQL database from one SQL elastic pool into another SQL elastic pool, and then moves hello database out of elastic pool tooa single Azure database performance level.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="154eb-105">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="154eb-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="154eb-106">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="154eb-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="154eb-107">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="154eb-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="154eb-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="154eb-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="154eb-109">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="154eb-109">Clean up deployment</span></span>

<span data-ttu-id="154eb-110">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello e tutte le risorse associate.</span><span class="sxs-lookup"><span data-stu-id="154eb-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="154eb-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="154eb-111">Script explanation</span></span>

<span data-ttu-id="154eb-112">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="154eb-112">This script uses hello following commands.</span></span> <span data-ttu-id="154eb-113">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="154eb-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="154eb-114">Comando</span><span class="sxs-lookup"><span data-stu-id="154eb-114">Command</span></span> | <span data-ttu-id="154eb-115">Note</span><span class="sxs-lookup"><span data-stu-id="154eb-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="154eb-116">az group create</span><span class="sxs-lookup"><span data-stu-id="154eb-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="154eb-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="154eb-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="154eb-118">az sql server create</span><span class="sxs-lookup"><span data-stu-id="154eb-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="154eb-119">Crea un server logico che ospita un database o un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="154eb-119">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="154eb-120">az sql elastic-pools create</span><span class="sxs-lookup"><span data-stu-id="154eb-120">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="154eb-121">Crea un pool elastico all'interno di server logico hello.</span><span class="sxs-lookup"><span data-stu-id="154eb-121">Creates an elastic pool within hello logical server.</span></span> |
| [<span data-ttu-id="154eb-122">az sql db create</span><span class="sxs-lookup"><span data-stu-id="154eb-122">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="154eb-123">Crea un database in un server logico come database singolo o in pool.</span><span class="sxs-lookup"><span data-stu-id="154eb-123">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="154eb-124">az sql db update</span><span class="sxs-lookup"><span data-stu-id="154eb-124">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="154eb-125">Aggiorna le proprietà del database o sposta un database all'interno, all'esterno o tra pool elastici.</span><span class="sxs-lookup"><span data-stu-id="154eb-125">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="154eb-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="154eb-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="154eb-127">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="154eb-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="154eb-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="154eb-128">Next steps</span></span>

<span data-ttu-id="154eb-129">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="154eb-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="154eb-130">Ulteriori esempi di script SQL Database CLI sono reperibile in hello [documentazione relativa al Database di SQL Azure](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="154eb-130">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>


