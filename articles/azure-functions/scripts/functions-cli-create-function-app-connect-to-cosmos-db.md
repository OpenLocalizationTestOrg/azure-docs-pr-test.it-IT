---
title: Creare una funzione di Azure che si connette a un Azure Cosmos DB | Microsoft Docs
description: Esempio di script dell'interfaccia della riga di comando - Creare una funzione di Azure che si connette a un Azure Cosmos DB
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: ba7e934f71824493f29b001cea6dd1c567ef3414
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-that-connects-to-an-azure-cosmos-db"></a><span data-ttu-id="4aa43-103">Creare una funzione di Azure che si connette a un database Azure Cosmos DB | Documentazione Microsoft</span><span class="sxs-lookup"><span data-stu-id="4aa43-103">Create an Azure Function that connects to an Azure Cosmos DB</span></span>

<span data-ttu-id="4aa43-104">Questo script di esempio crea un'app per le funzioni di Azure e si connette a un database Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4aa43-104">This sample script creates an Azure Function App and connects to an Azure Cosmos DB database.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4aa43-105">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="4aa43-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="4aa43-106">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="4aa43-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="4aa43-107">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4aa43-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="4aa43-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="4aa43-108">Sample script</span></span>

<span data-ttu-id="4aa43-109">In questo esempio si crea un'app per le funzioni di Azure e si aggiunge un endpoint Cosmos DB e la chiave di accesso alle impostazioni dell'app.</span><span class="sxs-lookup"><span data-stu-id="4aa43-109">This sample creates an Azure Function app and adds a Cosmos DB endpoint and access key to app settings.</span></span>

<span data-ttu-id="4aa43-110">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Creare una funzione di Azure che si connette a un database Azure Cosmos DB")]</span><span class="sxs-lookup"><span data-stu-id="4aa43-110">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Create an Azure Function that connects to an Azure Cosmos DB")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="4aa43-111">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="4aa43-111">Clean up deployment</span></span>

<span data-ttu-id="4aa43-112">Dopo l'esecuzione dello script di esempio, eseguire il comando seguente per rimuovere il gruppo di risorse e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="4aa43-112">After the script sample has been run, the follow command can be used to remove the resource group and all related resources.</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="4aa43-113">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="4aa43-113">Script explanation</span></span>

<span data-ttu-id="4aa43-114">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="4aa43-114">This script uses the following commands.</span></span> <span data-ttu-id="4aa43-115">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="4aa43-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4aa43-116">Comando</span><span class="sxs-lookup"><span data-stu-id="4aa43-116">Command</span></span> | <span data-ttu-id="4aa43-117">Note</span><span class="sxs-lookup"><span data-stu-id="4aa43-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4aa43-118">az login</span><span class="sxs-lookup"><span data-stu-id="4aa43-118">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="4aa43-119">Accedere ad Azure.</span><span class="sxs-lookup"><span data-stu-id="4aa43-119">Login to Azure.</span></span> |
| [<span data-ttu-id="4aa43-120">az group create</span><span class="sxs-lookup"><span data-stu-id="4aa43-120">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="4aa43-121">Creare un gruppo di risorse con una posizione</span><span class="sxs-lookup"><span data-stu-id="4aa43-121">Create a resource group with location</span></span> |
| [<span data-ttu-id="4aa43-122">az storage account create</span><span class="sxs-lookup"><span data-stu-id="4aa43-122">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="4aa43-123">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="4aa43-123">Create a storage account</span></span> |
| [<span data-ttu-id="4aa43-124">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="4aa43-124">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="4aa43-125">Creare una nuova app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="4aa43-125">Create a new function app</span></span> |
| [<span data-ttu-id="4aa43-126">az documentdb create</span><span class="sxs-lookup"><span data-stu-id="4aa43-126">az documentdb create</span></span>](https://docs.microsoft.com/cli/azure/documentdb#create) | <span data-ttu-id="4aa43-127">Crea un database DocumentDB</span><span class="sxs-lookup"><span data-stu-id="4aa43-127">Create documentdb database</span></span> |
| [<span data-ttu-id="4aa43-128">az group delete</span><span class="sxs-lookup"><span data-stu-id="4aa43-128">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="4aa43-129">Eseguire la pulizia</span><span class="sxs-lookup"><span data-stu-id="4aa43-129">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4aa43-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4aa43-130">Next steps</span></span>

<span data-ttu-id="4aa43-131">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4aa43-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4aa43-132">Altri esempi di script dell'interfaccia della riga di comando di Funzioni di Azure sono disponibili nella [documentazione di Funzioni di Azure](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4aa43-132">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>




