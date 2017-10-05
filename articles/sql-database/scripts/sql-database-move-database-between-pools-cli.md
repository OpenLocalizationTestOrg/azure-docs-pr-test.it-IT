---
title: Script di esempio dell'interfaccia della riga di comando di Azure per lo spostamento di un database SQL in un pool elastico SQL | Microsoft Docs
description: Script di esempio dell'interfaccia della riga di comando di Azure per lo spostamento di un database SQL in un pool elastico SQL
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
ms.openlocfilehash: 1dc31a0b20f36e28a58896ed63a5e0395ae1d3af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-cli-to-move-an-azure-sql-database-in-a-sql-elastic-pool"></a><span data-ttu-id="ed290-103">Usare l'interfaccia della riga di comando per spostare un database SQL di Azure in un pool elastico SQL</span><span class="sxs-lookup"><span data-stu-id="ed290-103">Use CLI to move an Azure SQL database in a SQL elastic pool</span></span>

<span data-ttu-id="ed290-104">Questo script di esempio dell'interfaccia della riga di comando di Azure crea due pool elastici e sposta un database SQL di Azure da un pool elastico all'altro, quindi sposta un database all'esterno di un pool elastico in un livello di prestazioni a database singolo di Azure.</span><span class="sxs-lookup"><span data-stu-id="ed290-104">This Azure CLI script example creates two elastic pools and moves an Azure SQL database from one SQL elastic pool into another SQL elastic pool, and then moves the database out of elastic pool to a single Azure database performance level.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ed290-105">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="ed290-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ed290-106">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="ed290-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="ed290-107">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ed290-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="ed290-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="ed290-108">Sample script</span></span>

<span data-ttu-id="ed290-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Spostare database tra pool")]</span><span class="sxs-lookup"><span data-stu-id="ed290-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Move database between pools")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="ed290-110">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="ed290-110">Clean up deployment</span></span>

<span data-ttu-id="ed290-111">Dopo l'esecuzione dello script di esempio, è possibile usare il comando seguente per rimuovere il gruppo di risorse e tutte le risorse ad esso associate.</span><span class="sxs-lookup"><span data-stu-id="ed290-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ed290-112">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="ed290-112">Script explanation</span></span>

<span data-ttu-id="ed290-113">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="ed290-113">This script uses the following commands.</span></span> <span data-ttu-id="ed290-114">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="ed290-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ed290-115">Comando</span><span class="sxs-lookup"><span data-stu-id="ed290-115">Command</span></span> | <span data-ttu-id="ed290-116">Note</span><span class="sxs-lookup"><span data-stu-id="ed290-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ed290-117">az group create</span><span class="sxs-lookup"><span data-stu-id="ed290-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ed290-118">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="ed290-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ed290-119">az sql server create</span><span class="sxs-lookup"><span data-stu-id="ed290-119">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="ed290-120">Crea un server logico che ospita un database o un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="ed290-120">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="ed290-121">az sql elastic-pools create</span><span class="sxs-lookup"><span data-stu-id="ed290-121">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="ed290-122">Crea un pool elastico all'interno di un server logico.</span><span class="sxs-lookup"><span data-stu-id="ed290-122">Creates an elastic pool within the logical server.</span></span> |
| [<span data-ttu-id="ed290-123">az sql db create</span><span class="sxs-lookup"><span data-stu-id="ed290-123">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="ed290-124">Crea un database in un server logico come database singolo o in pool.</span><span class="sxs-lookup"><span data-stu-id="ed290-124">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="ed290-125">az sql db update</span><span class="sxs-lookup"><span data-stu-id="ed290-125">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="ed290-126">Aggiorna le proprietà del database o sposta un database all'interno, all'esterno o tra pool elastici.</span><span class="sxs-lookup"><span data-stu-id="ed290-126">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="ed290-127">az group delete</span><span class="sxs-lookup"><span data-stu-id="ed290-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="ed290-128">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="ed290-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ed290-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ed290-129">Next steps</span></span>

<span data-ttu-id="ed290-130">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ed290-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ed290-131">Per altri esempi di script dell'interfaccia della riga di comando per database SQL, vedere la [documentazione del database SQL di Azure](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ed290-131">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>


