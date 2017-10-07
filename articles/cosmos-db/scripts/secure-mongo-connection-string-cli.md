---
title: stringa di connessione CLI Script Get Azure Cosmos DB per le app di MongoDB aaaAzure | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Ottenere la stringa di connessione di Azure Cosmos DB per app MongoDB
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
ms.openlocfilehash: 9b0a4bf020039c9bf9554b4199a279622c15a15d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-an-azure-cosmos-db-connection-string-for-mongodb-apps-using-hello-azure-cli"></a><span data-ttu-id="1c6de-103">Ottenere una stringa di connessione di database di Azure Cosmos per le applicazioni di MongoDB mediante hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="1c6de-103">Get an Azure Cosmos DB connection string for MongoDB apps using hello Azure CLI</span></span>

<span data-ttu-id="1c6de-104">In questo esempio ottiene una stringa di connessione database Cosmos di Azure per le applicazioni di MongoDB utilizzando hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="1c6de-104">This sample gets an Azure Cosmos DB connection string for MongoDB apps using hello Azure CLI.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1c6de-105">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="1c6de-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="1c6de-106">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="1c6de-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="1c6de-107">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1c6de-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="1c6de-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="1c6de-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/secure-cosmosdb-get-mongodb-connection-string/secure-cosmosdb-get-mongodb-connection-string.sh?highlight=36-39 "Get Azure Cosmos DB connection string for MongoDB apps")]

## <a name="clean-up-deployment"></a><span data-ttu-id="1c6de-109">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="1c6de-109">Clean up deployment</span></span>

<span data-ttu-id="1c6de-110">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello e tutte le risorse associate.</span><span class="sxs-lookup"><span data-stu-id="1c6de-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="1c6de-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="1c6de-111">Script explanation</span></span>

<span data-ttu-id="1c6de-112">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="1c6de-112">This script uses hello following commands.</span></span> <span data-ttu-id="1c6de-113">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="1c6de-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1c6de-114">Comando</span><span class="sxs-lookup"><span data-stu-id="1c6de-114">Command</span></span> | <span data-ttu-id="1c6de-115">Note</span><span class="sxs-lookup"><span data-stu-id="1c6de-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1c6de-116">az group create</span><span class="sxs-lookup"><span data-stu-id="1c6de-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="1c6de-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="1c6de-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1c6de-118">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="1c6de-118">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="1c6de-119">Aggiorna un account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1c6de-119">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="1c6de-120">az cosmosdb list-connection-strings</span><span class="sxs-lookup"><span data-stu-id="1c6de-120">az cosmosdb list-connection-strings</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#list-connection-strings) | <span data-ttu-id="1c6de-121">Ottiene la stringa di connessione hello per conto di hello.</span><span class="sxs-lookup"><span data-stu-id="1c6de-121">Gets hello connection string for hello account.</span></span>|
| [<span data-ttu-id="1c6de-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="1c6de-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="1c6de-123">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="1c6de-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1c6de-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1c6de-124">Next steps</span></span>

<span data-ttu-id="1c6de-125">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1c6de-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="1c6de-126">Ulteriori esempi di script di Azure Cosmos DB CLI sono reperibile in hello [documentazione CLI di Azure Cosmos DB](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1c6de-126">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
