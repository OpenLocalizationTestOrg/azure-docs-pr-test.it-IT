---
title: "aaaAzure CLI Script: consente di creare un criterio di failover per la disponibilità elevata | Documenti Microsoft"
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
ms.openlocfilehash: 9076f4ef23fceb4208c934c57ac6899f0b58ffd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-failover-policy-for-high-availability-using-hello-azure-cli"></a><span data-ttu-id="2b7c3-103">Creare un criterio di failover per la disponibilità elevata utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="2b7c3-103">Create a failover policy for high availability using hello Azure CLI</span></span>

<span data-ttu-id="2b7c3-104">Questo esempio di script dell'interfaccia della riga di comando crea un account Azure Cosmos DB e lo configura per la disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="2b7c3-104">This sample CLI script creates an Azure Cosmos DB account, and then configures it for high availability.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2b7c3-105">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="2b7c3-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="2b7c3-106">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="2b7c3-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="2b7c3-107">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2b7c3-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="2b7c3-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="2b7c3-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/high-availability-cosmosdb-configure-failover/high-availability-cosmosdb-configure-failover.sh?highlight=23-27 "Create an Azure Cosmos DB failover policy")]

## <a name="clean-up-deployment"></a><span data-ttu-id="2b7c3-109">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="2b7c3-109">Clean up deployment</span></span>

<span data-ttu-id="2b7c3-110">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello e tutte le risorse associate.</span><span class="sxs-lookup"><span data-stu-id="2b7c3-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="2b7c3-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="2b7c3-111">Script explanation</span></span>

<span data-ttu-id="2b7c3-112">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="2b7c3-112">This script uses hello following commands.</span></span> <span data-ttu-id="2b7c3-113">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="2b7c3-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2b7c3-114">Comando</span><span class="sxs-lookup"><span data-stu-id="2b7c3-114">Command</span></span> | <span data-ttu-id="2b7c3-115">Note</span><span class="sxs-lookup"><span data-stu-id="2b7c3-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2b7c3-116">az group create</span><span class="sxs-lookup"><span data-stu-id="2b7c3-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="2b7c3-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="2b7c3-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2b7c3-118">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="2b7c3-118">az cosmosdb create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="2b7c3-119">Crea un account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2b7c3-119">Creates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="2b7c3-120">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="2b7c3-120">az cosmosdb update</span></span>](/cli/azure/cosmosdb#update) | <span data-ttu-id="2b7c3-121">Aggiorna un account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2b7c3-121">Updates Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="2b7c3-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="2b7c3-122">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="2b7c3-123">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="2b7c3-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2b7c3-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2b7c3-124">Next steps</span></span>

<span data-ttu-id="2b7c3-125">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2b7c3-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2b7c3-126">Ulteriori esempi di script di Azure Cosmos DB CLI sono reperibile in hello [documentazione CLI di Azure Cosmos DB](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2b7c3-126">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
