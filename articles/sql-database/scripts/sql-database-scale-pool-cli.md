---
title: Script di esempio dell'interfaccia della riga di comando di Azure per il ridimensionamento di un pool elastico SQL nel database SQL di Azure | Microsoft Docs
description: Script di esempio dell'interfaccia della riga di comando di Azure per il ridimensionamento di un pool elastico SQL nel database SQL di Azure
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
ms.openlocfilehash: 888d2b7b7c118fede82d39881570a3b3d7b09961
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="use-cli-to-scale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="2b7ef-103">Usare l'interfaccia della riga di comando per ridimensionare un pool elastico SQL nel database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="2b7ef-103">Use CLI to scale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="2b7ef-104">Questo script di esempio dell'interfaccia della riga di comando di Azure crea pool elastici SQL, sposta i database in pool e modifica i livelli di prestazioni del pool elastico.</span><span class="sxs-lookup"><span data-stu-id="2b7ef-104">This Azure CLI script example creates SQL elastic pools, moves pooled databases, and changes elastic pool performance levels.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2b7ef-105">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="2b7ef-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="2b7ef-106">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="2b7ef-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="2b7ef-107">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2b7ef-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="2b7ef-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="2b7ef-108">Sample script</span></span>

<span data-ttu-id="2b7ef-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Spostare database tra pool")]</span><span class="sxs-lookup"><span data-stu-id="2b7ef-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Move database between pools")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="2b7ef-110">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="2b7ef-110">Clean up deployment</span></span>

<span data-ttu-id="2b7ef-111">Dopo l'esecuzione dello script di esempio, è possibile usare il comando seguente per rimuovere il gruppo di risorse e tutte le risorse ad esso associate.</span><span class="sxs-lookup"><span data-stu-id="2b7ef-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="2b7ef-112">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="2b7ef-112">Script explanation</span></span>

<span data-ttu-id="2b7ef-113">Questo script usa i comandi seguenti per creare un gruppo di risorse, un server logico, un database SQL e le regole del firewall.</span><span class="sxs-lookup"><span data-stu-id="2b7ef-113">This script uses the following commands to create a resource group, logical server, SQL Database, and firewall rules.</span></span> <span data-ttu-id="2b7ef-114">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="2b7ef-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2b7ef-115">Comando</span><span class="sxs-lookup"><span data-stu-id="2b7ef-115">Command</span></span> | <span data-ttu-id="2b7ef-116">Note</span><span class="sxs-lookup"><span data-stu-id="2b7ef-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2b7ef-117">az group create</span><span class="sxs-lookup"><span data-stu-id="2b7ef-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="2b7ef-118">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="2b7ef-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2b7ef-119">az sql server create</span><span class="sxs-lookup"><span data-stu-id="2b7ef-119">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="2b7ef-120">Consente di creare un server logico che ospita il database SQL.</span><span class="sxs-lookup"><span data-stu-id="2b7ef-120">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="2b7ef-121">az sql elastic-pools create</span><span class="sxs-lookup"><span data-stu-id="2b7ef-121">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="2b7ef-122">Consente di creare un pool di database elastico all'interno del server logico.</span><span class="sxs-lookup"><span data-stu-id="2b7ef-122">Creates an elastic database pool within the logical server.</span></span> |
| [<span data-ttu-id="2b7ef-123">az sql db create</span><span class="sxs-lookup"><span data-stu-id="2b7ef-123">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="2b7ef-124">Consente di creare il database SQL nel server logico.</span><span class="sxs-lookup"><span data-stu-id="2b7ef-124">Creates the SQL Database in the logical server.</span></span> |
| [<span data-ttu-id="2b7ef-125">az sql elastic-pools update</span><span class="sxs-lookup"><span data-stu-id="2b7ef-125">az sql elastic-pools update</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#update) | <span data-ttu-id="2b7ef-126">Consente di aggiornare un pool di database elastico, in questo esempio modifica l'eDTU assegnato.</span><span class="sxs-lookup"><span data-stu-id="2b7ef-126">Updates an elastic database pool, in this example changes the assigned eDTU.</span></span> |
| [<span data-ttu-id="2b7ef-127">az group delete</span><span class="sxs-lookup"><span data-stu-id="2b7ef-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="2b7ef-128">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="2b7ef-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2b7ef-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2b7ef-129">Next steps</span></span>

<span data-ttu-id="2b7ef-130">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2b7ef-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2b7ef-131">Per altri esempi di script dell'interfaccia della riga di comando per database SQL, vedere la [documentazione del database SQL di Azure](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2b7ef-131">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
