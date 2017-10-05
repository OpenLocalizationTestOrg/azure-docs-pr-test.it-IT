---
title: Esempio dell'interfaccia della riga di comando - Monitorare e ridimensionare un singolo database SQL di Azure | Microsoft Docs
description: Script di esempio dell'interfaccia della riga di comando di Azure per monitorare e ridimensionare un singolo database SQL di Azure
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
ms.openlocfilehash: 01911b85268244a8fddb32aa726f8a870abbaf77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-cli-to-monitor-and-scale-a-single-sql-database"></a><span data-ttu-id="ba0a4-103">Usare l'interfaccia della riga di comando per monitorare e ridimensionare un singolo database SQL</span><span class="sxs-lookup"><span data-stu-id="ba0a4-103">Use CLI to monitor and scale a single SQL database</span></span>

<span data-ttu-id="ba0a4-104">Questo esempio di script dell'interfaccia della riga di comando di Azure ridimensiona un singolo database SQL di Azure per ottenere un livello di prestazioni diverso dopo aver recuperato informazioni sulle dimensioni del database tramite query.</span><span class="sxs-lookup"><span data-stu-id="ba0a4-104">This Azure CLI script example scales a single Azure SQL database to a different performance level after querying the size information of the database.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ba0a4-105">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba0a4-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ba0a4-106">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="ba0a4-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="ba0a4-107">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ba0a4-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="ba0a4-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="ba0a4-108">Sample script</span></span>

<span data-ttu-id="ba0a4-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.sh "Monitorare e ridimensionare database SQL singoli")]</span><span class="sxs-lookup"><span data-stu-id="ba0a4-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.sh "Monitor and scale single SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="ba0a4-110">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="ba0a4-110">Clean up deployment</span></span>

<span data-ttu-id="ba0a4-111">Dopo l'esecuzione dello script di esempio, è possibile usare il comando seguente per rimuovere il gruppo di risorse e tutte le risorse ad esso associate.</span><span class="sxs-lookup"><span data-stu-id="ba0a4-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ba0a4-112">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="ba0a4-112">Script explanation</span></span>

<span data-ttu-id="ba0a4-113">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="ba0a4-113">This script uses the following commands.</span></span> <span data-ttu-id="ba0a4-114">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="ba0a4-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ba0a4-115">Comando</span><span class="sxs-lookup"><span data-stu-id="ba0a4-115">Command</span></span> | <span data-ttu-id="ba0a4-116">Note</span><span class="sxs-lookup"><span data-stu-id="ba0a4-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ba0a4-117">az group create</span><span class="sxs-lookup"><span data-stu-id="ba0a4-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ba0a4-118">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="ba0a4-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ba0a4-119">az sql server create</span><span class="sxs-lookup"><span data-stu-id="ba0a4-119">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="ba0a4-120">Crea un server logico che ospita un database.</span><span class="sxs-lookup"><span data-stu-id="ba0a4-120">Creates a logical server that hosts a database.</span></span> |
| [<span data-ttu-id="ba0a4-121">az sql db show-usage</span><span class="sxs-lookup"><span data-stu-id="ba0a4-121">az sql db show-usage</span></span>](https://docs.microsoft.com/cli/azure/sql/db#show-usage) | <span data-ttu-id="ba0a4-122">Mostra le informazioni sull'utilizzo delle dimensioni per un database.</span><span class="sxs-lookup"><span data-stu-id="ba0a4-122">Shows the size usage information for a database.</span></span> |
| [<span data-ttu-id="ba0a4-123">az sql db update</span><span class="sxs-lookup"><span data-stu-id="ba0a4-123">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="ba0a4-124">Aggiorna le proprietà del database, come il livello di servizio o il livello di prestazioni, oppure sposta un database all'interno, all'esterno o tra pool elastici.</span><span class="sxs-lookup"><span data-stu-id="ba0a4-124">Updates database properties (such as the service tier or performance level) or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="ba0a4-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="ba0a4-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="ba0a4-126">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="ba0a4-126">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="ba0a4-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ba0a4-127">Next steps</span></span>

<span data-ttu-id="ba0a4-128">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ba0a4-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ba0a4-129">Per altri esempi di script dell'interfaccia della riga di comando per database SQL, vedere la [documentazione del database SQL di Azure](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ba0a4-129">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
