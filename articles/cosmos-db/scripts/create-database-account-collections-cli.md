---
title: Creare un account API di Azure Cosmos DB DocumentDB, un database e una raccolta con lo script dell'interfaccia della riga di comando di Azure | Microsoft Docs
description: Creare un account API di Azure Cosmos DB DocumentDB, un database e una raccolta con un esempio di script dell'interfaccia della riga di comando di Azure
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 06/06/2017
ms.author: mimig
ms.openlocfilehash: 28f99d56404e47adcd375d9f3106cc234469cbfd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-create-an-documentdb-api-account-using-cli"></a><span data-ttu-id="57286-103">Azure Cosmos DB: creare un account API di DocumentDB con l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="57286-103">Azure Cosmos DB: Create an DocumentDB API account using CLI</span></span>

<span data-ttu-id="57286-104">Questo script dell'interfaccia della riga di comando di Azure di esempio permette di creare un account API di Azure Cosmos DB DocumentDB, un database e una raccolta.</span><span class="sxs-lookup"><span data-stu-id="57286-104">This sample CLI script creates an Azure Cosmos DB DocumentDB API account, database, and collection.</span></span>  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="57286-105">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="57286-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="57286-106">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="57286-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="57286-107">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="57286-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="57286-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="57286-108">Sample script</span></span>

<span data-ttu-id="57286-109">[!code-azurecli-interactive[principale](../../../cli_scripts/cosmosdb/create-cosmosdb-account-database/create-cosmosdb-account-database.sh?highlight=15-35 "Creare un account API di Azure Cosmos DB DocumentDB, un database e una raccolta")]</span><span class="sxs-lookup"><span data-stu-id="57286-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/create-cosmosdb-account-database/create-cosmosdb-account-database.sh?highlight=15-35 "Create an Azure Cosmos DB DocumentDB API account, database, and collection")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="57286-110">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="57286-110">Clean up deployment</span></span>

<span data-ttu-id="57286-111">Dopo l'esecuzione dello script di esempio, è possibile usare il comando seguente per rimuovere il gruppo di risorse e tutte le risorse ad esso associate.</span><span class="sxs-lookup"><span data-stu-id="57286-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="57286-112">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="57286-112">Script explanation</span></span>

<span data-ttu-id="57286-113">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="57286-113">This script uses the following commands.</span></span> <span data-ttu-id="57286-114">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="57286-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="57286-115">Comando</span><span class="sxs-lookup"><span data-stu-id="57286-115">Command</span></span> | <span data-ttu-id="57286-116">Note</span><span class="sxs-lookup"><span data-stu-id="57286-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="57286-117">az group create</span><span class="sxs-lookup"><span data-stu-id="57286-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="57286-118">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="57286-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="57286-119">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="57286-119">az cosmosdb create</span></span>](/cli/azure/cosmosdb#create) | <span data-ttu-id="57286-120">Crea un account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="57286-120">Creates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="57286-121">az group delete</span><span class="sxs-lookup"><span data-stu-id="57286-121">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="57286-122">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="57286-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="57286-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="57286-123">Next steps</span></span>

<span data-ttu-id="57286-124">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="57286-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="57286-125">Altri esempi di script dell'interfaccia della riga di comando di Azure Cosmos DB sono disponibili nella [documentazione dell'interfaccia della riga di comando di Azure Cosmos DB](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="57286-125">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
