---
title: aaaAzure CLI Script di esempio - creare una Cache Redis di Azure | Documenti Microsoft
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
ms.openlocfilehash: 85b007a426fbd4752034ec8663835963d140dd75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-redis-cache"></a><span data-ttu-id="cac02-103">Creare una cache Redis di Azure</span><span class="sxs-lookup"><span data-stu-id="cac02-103">Create an Azure Redis Cache</span></span>

<span data-ttu-id="cac02-104">In questo scenario viene illustrato come toocreate un Redis di Azure memorizzano nella Cache.</span><span class="sxs-lookup"><span data-stu-id="cac02-104">In this scenario, you learn how toocreate an Azure Redis Cache.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="cac02-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="cac02-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/create-cache/create-cache.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="cac02-106">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="cac02-106">Script explanation</span></span>

<span data-ttu-id="cac02-107">Questo script utilizza hello toocreate i comandi seguenti a un gruppo di risorse e una cache redis.</span><span class="sxs-lookup"><span data-stu-id="cac02-107">This script uses hello following commands toocreate a resource group and a redis cache.</span></span> <span data-ttu-id="cac02-108">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="cac02-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="cac02-109">Comando</span><span class="sxs-lookup"><span data-stu-id="cac02-109">Command</span></span> | <span data-ttu-id="cac02-110">Note</span><span class="sxs-lookup"><span data-stu-id="cac02-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cac02-111">az group create</span><span class="sxs-lookup"><span data-stu-id="cac02-111">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="cac02-112">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="cac02-112">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="cac02-113">az redis create</span><span class="sxs-lookup"><span data-stu-id="cac02-113">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="cac02-114">Creare un'istanza di Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="cac02-114">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="cac02-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cac02-115">Next steps</span></span>

<span data-ttu-id="cac02-116">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cac02-116">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="cac02-117">Ulteriori esempi di script di Azure Redis Cache CLI sono reperibile in hello [documentazione Cache Redis di Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="cac02-117">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
