---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Ottenere i dettagli di un'istanza di Cache Redis di Azure | Documentazione Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Ottenere i dettagli di un'istanza di Cache Redis di Azure
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 155924e6-00d5-4a8c-ba99-5189f300464a
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: 9f4eb32227bd8a68837eabd58b9d058bc4995d17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-details-of-an-azure-redis-cache"></a><span data-ttu-id="f26b6-103">Ottiene i dettagli di una Cache Redis di Azure</span><span class="sxs-lookup"><span data-stu-id="f26b6-103">Get details of an Azure Redis Cache</span></span>

<span data-ttu-id="f26b6-104">In questo scenario, informazioni su come recuperare i dettagli di un'istanza di Cache Redis di Azure, incluso il relativo stato di provisioning.</span><span class="sxs-lookup"><span data-stu-id="f26b6-104">In this scenario, you learn how to retrieve the details of an Azure Redis Cache instance, including its provisioning status.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="f26b6-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="f26b6-105">Sample script</span></span>

<span data-ttu-id="f26b6-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/show-cache/show-cache.sh "Cache Redis di Azure")]</span><span class="sxs-lookup"><span data-stu-id="f26b6-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/show-cache/show-cache.sh "Azure Redis Cache")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="f26b6-107">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="f26b6-107">Script explanation</span></span>

<span data-ttu-id="f26b6-108">Questo script usa i comandi seguenti per recuperare i dettagli di un'istanza di Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="f26b6-108">This script uses the following commands to retrieve the details of an Azure Redis Cache instance.</span></span> <span data-ttu-id="f26b6-109">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="f26b6-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f26b6-110">Comando</span><span class="sxs-lookup"><span data-stu-id="f26b6-110">Command</span></span> | <span data-ttu-id="f26b6-111">Note</span><span class="sxs-lookup"><span data-stu-id="f26b6-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f26b6-112">az redis show</span><span class="sxs-lookup"><span data-stu-id="f26b6-112">az redis show</span></span>](https://docs.microsoft.com/cli/azure/redis#show) | <span data-ttu-id="f26b6-113">Recupera i dettagli di un'istanza di Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="f26b6-113">Retrieve details of an Azure Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="f26b6-114">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f26b6-114">Next steps</span></span>

<span data-ttu-id="f26b6-115">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f26b6-115">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f26b6-116">Altri esempi di script dell'interfaccia della riga di comando della Cache Redis di Azure sono disponibili nella [documentazione della Cache Redis di Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f26b6-116">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>