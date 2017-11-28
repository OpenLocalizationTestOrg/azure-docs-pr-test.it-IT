---
title: aaaAzure CLI Script di esempio - creare una Cache Redis di Azure Premium con clustering | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una cache Redis di Azure Premium con clustering
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 07bcceae-2521-4fe3-b88f-ed833104ddd2
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: ca34d40059b282cb2abc7e3e2b8771226029744c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-premium-azure-redis-cache-with-clustering"></a><span data-ttu-id="122bf-103">Creare una cache Redis di Azure Premium con clustering</span><span class="sxs-lookup"><span data-stu-id="122bf-103">Create a Premium Azure Redis Cache with clustering</span></span>

<span data-ttu-id="122bf-104">In questo scenario viene illustrato come toocreate un livello di 6 GB Premium Cache Redis di Azure con il servizio cluster abilitato e due partizioni.</span><span class="sxs-lookup"><span data-stu-id="122bf-104">In this scenario, you learn how toocreate a 6 GB Premium tier Azure Redis Cache with clustering enabled and two shards.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="122bf-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="122bf-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="122bf-106">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="122bf-106">Script explanation</span></span>

<span data-ttu-id="122bf-107">Questo script utilizza hello seguenti comandi toocreate un gruppo di risorse e una cache redis di livello Premium con Abilita il clustering.</span><span class="sxs-lookup"><span data-stu-id="122bf-107">This script uses hello following commands toocreate a resource group and a Premium tier redis cache with clustering enable.</span></span> <span data-ttu-id="122bf-108">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="122bf-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="122bf-109">Comando</span><span class="sxs-lookup"><span data-stu-id="122bf-109">Command</span></span> | <span data-ttu-id="122bf-110">Note</span><span class="sxs-lookup"><span data-stu-id="122bf-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="122bf-111">az group create</span><span class="sxs-lookup"><span data-stu-id="122bf-111">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="122bf-112">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="122bf-112">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="122bf-113">az redis create</span><span class="sxs-lookup"><span data-stu-id="122bf-113">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="122bf-114">Creare un'istanza di Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="122bf-114">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="122bf-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="122bf-115">Next steps</span></span>

<span data-ttu-id="122bf-116">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="122bf-116">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="122bf-117">Ulteriori esempi di script di Azure Redis Cache CLI sono reperibile in hello [documentazione Cache Redis di Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="122bf-117">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
