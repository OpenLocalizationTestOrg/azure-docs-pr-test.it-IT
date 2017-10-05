---
title: 'Esempio di script dell''interfaccia della riga di comando di Azure: creare un''istanza di Cache Redis di Azure | Microsoft Docs'
description: 'Esempio di script dell''interfaccia della riga di comando di Azure: creare un''istanza di Cache Redis di Azure'
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: afd7f6e0-9297-4c98-a95e-597be939cef7
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: c6b153d80de4cbf2bec1bc70d67be7befa0c5ec3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-redis-cache"></a><span data-ttu-id="0c679-103">Creare una cache Redis di Azure</span><span class="sxs-lookup"><span data-stu-id="0c679-103">Create an Azure Redis Cache</span></span>

<span data-ttu-id="0c679-104">In questo scenario viene illustrato come creare un'istanza di Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="0c679-104">In this scenario, you learn how to create an Azure Redis Cache.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="0c679-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="0c679-105">Sample script</span></span>

<span data-ttu-id="0c679-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/create-cache/create-cache.sh "Cache Redis di Azure")]</span><span class="sxs-lookup"><span data-stu-id="0c679-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/create-cache/create-cache.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="0c679-107">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="0c679-107">Script explanation</span></span>

<span data-ttu-id="0c679-108">Questo script usa i comandi seguenti per creare un gruppo di risorse e un'istanza di Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="0c679-108">This script uses the following commands to create a resource group and a redis cache.</span></span> <span data-ttu-id="0c679-109">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="0c679-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0c679-110">Comando</span><span class="sxs-lookup"><span data-stu-id="0c679-110">Command</span></span> | <span data-ttu-id="0c679-111">Note</span><span class="sxs-lookup"><span data-stu-id="0c679-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0c679-112">az group create</span><span class="sxs-lookup"><span data-stu-id="0c679-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="0c679-113">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="0c679-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0c679-114">az redis create</span><span class="sxs-lookup"><span data-stu-id="0c679-114">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="0c679-115">Creare un'istanza di Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="0c679-115">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="0c679-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0c679-116">Next steps</span></span>

<span data-ttu-id="0c679-117">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0c679-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="0c679-118">Altri esempi di script dell'interfaccia della riga di comando della Cache Redis di Azure sono disponibili nella [documentazione della Cache Redis di Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0c679-118">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>