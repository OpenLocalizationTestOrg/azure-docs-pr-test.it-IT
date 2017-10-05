---
title: 'Script dell''interfaccia della riga di comando di Azure: creare un firewall per Azure Cosmos DB | Microsoft Docs'
description: 'Esempio di script dell''interfaccia della riga di comando di Azure: creazione di un firewall per Azure Cosmos DB'
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: sammvcple
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 06/02/2017
ms.author: mimig
ms.openlocfilehash: 51f61901e1b1615e48582690dea701a01a56ebca
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-create-a-firewall-using-the-azure-cli"></a><span data-ttu-id="ac29b-103">Azure Cosmos DB: creare un firewall con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="ac29b-103">Azure Cosmos DB: Create a firewall using the Azure CLI</span></span>

<span data-ttu-id="ac29b-104">Questo esempio di script dell'interfaccia della riga di comando consente di creare un criterio firewall per qualsiasi tipo di account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ac29b-104">This sample CLI script creates a firewall policy for any kind of Azure Cosmos DB account.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ac29b-105">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="ac29b-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ac29b-106">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="ac29b-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="ac29b-107">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ac29b-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="ac29b-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="ac29b-108">Sample script</span></span>

<span data-ttu-id="ac29b-109">[!code-azurecli-interactive[principale](../../../cli_scripts/cosmosdb/secure-cosmosdb-create-firewall/secure-cosmosdb-create-firewall.sh?highlight=38-42 "Creare un firewall Azure Cosmos DB")]</span><span class="sxs-lookup"><span data-stu-id="ac29b-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/secure-cosmosdb-create-firewall/secure-cosmosdb-create-firewall.sh?highlight=38-42 "Create an Azure Cosmos DB firewall")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="ac29b-110">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="ac29b-110">Clean up deployment</span></span>

<span data-ttu-id="ac29b-111">Dopo l'esecuzione dello script di esempio, è possibile usare il comando seguente per rimuovere il gruppo di risorse e tutte le risorse ad esso associate.</span><span class="sxs-lookup"><span data-stu-id="ac29b-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ac29b-112">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="ac29b-112">Script explanation</span></span>

<span data-ttu-id="ac29b-113">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="ac29b-113">This script uses the following commands.</span></span> <span data-ttu-id="ac29b-114">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="ac29b-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ac29b-115">Comando</span><span class="sxs-lookup"><span data-stu-id="ac29b-115">Command</span></span> | <span data-ttu-id="ac29b-116">Note</span><span class="sxs-lookup"><span data-stu-id="ac29b-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ac29b-117">az group create</span><span class="sxs-lookup"><span data-stu-id="ac29b-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ac29b-118">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="ac29b-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ac29b-119">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="ac29b-119">az cosmosdb create</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#create) | <span data-ttu-id="ac29b-120">Crea un account Azure CosmosDB.</span><span class="sxs-lookup"><span data-stu-id="ac29b-120">Creates an Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="ac29b-121">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="ac29b-121">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="ac29b-122">Aggiorna un account Azure CosmosDB per includere le impostazioni del firewall.</span><span class="sxs-lookup"><span data-stu-id="ac29b-122">Updates an Azure CosmosDB account to include firewall settings.</span></span> |
| [<span data-ttu-id="ac29b-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="ac29b-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="ac29b-124">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="ac29b-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ac29b-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ac29b-125">Next steps</span></span>

<span data-ttu-id="ac29b-126">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ac29b-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ac29b-127">Altri esempi di script dell'interfaccia della riga di comando di Azure Cosmos DB sono disponibili nella [documentazione dell'interfaccia della riga di comando di Azure Cosmos DB](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ac29b-127">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
