---
title: aaaAzure CLI Script di esempio - hostname hello Get, porte e le chiavi per Cache Redis di Azure | Documenti Microsoft
description: Azure CLI Script di esempio - hostname hello Get, porte e le chiavi per un'istanza di Cache Redis di Azure
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 761eb24e-2ba7-418d-8fc3-431153e69a90
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: e6e794558087d6568438c439e2bf99fc46eeb8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-hostname-ports-and-keys-for-azure-redis-cache"></a><span data-ttu-id="3a860-103">Ottenere hello hostname, porte e le chiavi per Cache Redis di Azure</span><span class="sxs-lookup"><span data-stu-id="3a860-103">Get hello hostname, ports, and keys for Azure Redis Cache</span></span>

<span data-ttu-id="3a860-104">In questo scenario, si informazioni sull'utilizzo delle chiavi, porte e nome host hello tooretrieve istanza di Cache Redis di Azure tooan tooconnect.</span><span class="sxs-lookup"><span data-stu-id="3a860-104">In this scenario, you learn how tooretrieve hello hostname, ports, and keys used tooconnect tooan Azure Redis Cache instance.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="3a860-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="3a860-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis Cache")]


## <a name="script-explanation"></a><span data-ttu-id="3a860-106">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="3a860-106">Script explanation</span></span>

<span data-ttu-id="3a860-107">Questo script utilizza hello seguenti comandi tooretrieve hello hostname, chiavi e le porte di un'istanza di Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="3a860-107">This script uses hello following commands tooretrieve hello hostname, keys, and ports of an Azure Redis Cache instance.</span></span> <span data-ttu-id="3a860-108">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="3a860-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3a860-109">Comando</span><span class="sxs-lookup"><span data-stu-id="3a860-109">Command</span></span> | <span data-ttu-id="3a860-110">Note</span><span class="sxs-lookup"><span data-stu-id="3a860-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3a860-111">az redis show</span><span class="sxs-lookup"><span data-stu-id="3a860-111">az redis show</span></span>](https://docs.microsoft.com/cli/azure/redis#show) | <span data-ttu-id="3a860-112">Recupera i dettagli di un'istanza di Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="3a860-112">Retrieve details of an Azure Redis Cache instance.</span></span> |
| [<span data-ttu-id="3a860-113">az redis list-keys</span><span class="sxs-lookup"><span data-stu-id="3a860-113">az redis list-keys</span></span>](https://docs.microsoft.com/cli/azure/redis#list-keys) | <span data-ttu-id="3a860-114">Recupera le chiavi di accesso per un'istanza di Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="3a860-114">Retrieve access keys for an Azure Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="3a860-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3a860-115">Next steps</span></span>

<span data-ttu-id="3a860-116">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3a860-116">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3a860-117">Ulteriori esempi di script di Azure Redis Cache CLI sono reperibile in hello [documentazione Cache Redis di Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3a860-117">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
