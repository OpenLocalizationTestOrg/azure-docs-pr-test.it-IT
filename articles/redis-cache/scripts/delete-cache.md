---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Eliminare una cache Redis di Azure | Microsoft Docs
description: Esempio di script dell'interfaccia della riga di comando di Azure - Eliminare una cache Redis di Azure
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 7beded7a-d2c9-43a6-b3b4-b8079c11de4a
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: f959823b3a7c5b0262f693ecad1e6efc4eec4f35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="delete-an-azure-redis-cache"></a><span data-ttu-id="03738-103">Eliminare una cache Redis di Azure</span><span class="sxs-lookup"><span data-stu-id="03738-103">Delete an Azure Redis Cache</span></span>

<span data-ttu-id="03738-104">In questo scenario viene illustrato come eliminare una cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="03738-104">In this scenario, you learn how to delete an Azure Redis Cache.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="03738-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="03738-105">Sample script</span></span>

<span data-ttu-id="03738-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/delete-cache/delete-cache.sh "Cache Redis di Azure")]</span><span class="sxs-lookup"><span data-stu-id="03738-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/delete-cache/delete-cache.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="03738-107">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="03738-107">Script explanation</span></span>

<span data-ttu-id="03738-108">Questo script usa i comandi seguenti per eliminare un'istanza della cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="03738-108">This script uses the following commands to delete an Azure Redis Cache instance.</span></span> <span data-ttu-id="03738-109">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="03738-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="03738-110">Comando</span><span class="sxs-lookup"><span data-stu-id="03738-110">Command</span></span> | <span data-ttu-id="03738-111">Note</span><span class="sxs-lookup"><span data-stu-id="03738-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="03738-112">eliminazione di redis az</span><span class="sxs-lookup"><span data-stu-id="03738-112">az redis delete</span></span>](https://docs.microsoft.com/cli/azure/redis#delete) | <span data-ttu-id="03738-113">Eliminare un'istanza della cache Redis.</span><span class="sxs-lookup"><span data-stu-id="03738-113">Delete Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="03738-114">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="03738-114">Next steps</span></span>

<span data-ttu-id="03738-115">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="03738-115">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="03738-116">Altri esempi di script dell'interfaccia della riga di comando della Cache Redis di Azure sono disponibili nella [documentazione della Cache Redis di Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="03738-116">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>