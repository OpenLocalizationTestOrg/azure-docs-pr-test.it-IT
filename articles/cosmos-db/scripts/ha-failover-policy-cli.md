---
title: "Script dell'interfaccia della riga di comando di Azure - Creare un criterio di failover per la disponibilità elevata | Documentazione Microsoft"
description: "Esempio di script dell'interfaccia della riga di comando di Azure - Creare un criterio di failover per la disponibilità elevata"
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
ms.date: 06/02/2017
ms.author: mimig
ms.openlocfilehash: 96083d66cc1a2ef179f9313c1b3ed04162c1c048
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-failover-policy-for-high-availability-using-the-azure-cli"></a><span data-ttu-id="6da19-103">Creare un criterio di failover per la disponibilità elevata con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="6da19-103">Create a failover policy for high availability using the Azure CLI</span></span>

<span data-ttu-id="6da19-104">Questo esempio di script dell'interfaccia della riga di comando crea un account Azure Cosmos DB e lo configura per la disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="6da19-104">This sample CLI script creates an Azure Cosmos DB account, and then configures it for high availability.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6da19-105">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="6da19-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6da19-106">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="6da19-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="6da19-107">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6da19-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="6da19-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="6da19-108">Sample script</span></span>

<span data-ttu-id="6da19-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/high-availability-cosmosdb-configure-failover/high-availability-cosmosdb-configure-failover.sh?highlight=23-27 "Creare un criterio di failover in Azure Cosmos DB")]</span><span class="sxs-lookup"><span data-stu-id="6da19-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/high-availability-cosmosdb-configure-failover/high-availability-cosmosdb-configure-failover.sh?highlight=23-27 "Create an Azure Cosmos DB failover policy")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="6da19-110">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="6da19-110">Clean up deployment</span></span>

<span data-ttu-id="6da19-111">Dopo l'esecuzione dello script di esempio, è possibile usare il comando seguente per rimuovere il gruppo di risorse e tutte le risorse ad esso associate.</span><span class="sxs-lookup"><span data-stu-id="6da19-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="6da19-112">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="6da19-112">Script explanation</span></span>

<span data-ttu-id="6da19-113">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="6da19-113">This script uses the following commands.</span></span> <span data-ttu-id="6da19-114">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="6da19-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6da19-115">Comando</span><span class="sxs-lookup"><span data-stu-id="6da19-115">Command</span></span> | <span data-ttu-id="6da19-116">Note</span><span class="sxs-lookup"><span data-stu-id="6da19-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6da19-117">az group create</span><span class="sxs-lookup"><span data-stu-id="6da19-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="6da19-118">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="6da19-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6da19-119">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="6da19-119">az cosmosdb create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="6da19-120">Crea un account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6da19-120">Creates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="6da19-121">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="6da19-121">az cosmosdb update</span></span>](/cli/azure/cosmosdb#update) | <span data-ttu-id="6da19-122">Aggiorna un account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6da19-122">Updates Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="6da19-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="6da19-123">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="6da19-124">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="6da19-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6da19-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6da19-125">Next steps</span></span>

<span data-ttu-id="6da19-126">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6da19-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6da19-127">Altri esempi di script dell'interfaccia della riga di comando di Azure Cosmos DB sono disponibili nella [documentazione dell'interfaccia della riga di comando di Azure Cosmos DB](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6da19-127">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
