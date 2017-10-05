---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Recuperare il nome host, le porte e le chiavi per Cache Redis di Azure | Microsoft Docs
description: Esempio di script dell'interfaccia della riga di comando di Azure - Recuperare il nome host, le porte e le chiavi per un'istanza di Cache Redis di Azure
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
ms.openlocfilehash: cd9adc784bceb0fff5e7c2bbee2be0950c51c8f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-hostname-ports-and-keys-for-azure-redis-cache"></a><span data-ttu-id="379f9-103">Recuperare il nome host, le porte e le chiavi per Cache Redis di Azure</span><span class="sxs-lookup"><span data-stu-id="379f9-103">Get the hostname, ports, and keys for Azure Redis Cache</span></span>

<span data-ttu-id="379f9-104">In questo scenario si apprenderà come recuperare il nome host, le porte e le chiavi utilizzati per connettersi a un'istanza di Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="379f9-104">In this scenario, you learn how to retrieve the hostname, ports, and keys used to connect to an Azure Redis Cache instance.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="379f9-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="379f9-105">Sample script</span></span>

<span data-ttu-id="379f9-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Cache Redis di Azure")]</span><span class="sxs-lookup"><span data-stu-id="379f9-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis Cache")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="379f9-107">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="379f9-107">Script explanation</span></span>

<span data-ttu-id="379f9-108">Questo script utilizza i comandi seguenti per recuperare il nome host, le chiavi e le porte di un'istanza di Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="379f9-108">This script uses the following commands to retrieve the hostname, keys, and ports of an Azure Redis Cache instance.</span></span> <span data-ttu-id="379f9-109">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="379f9-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="379f9-110">Comando</span><span class="sxs-lookup"><span data-stu-id="379f9-110">Command</span></span> | <span data-ttu-id="379f9-111">Note</span><span class="sxs-lookup"><span data-stu-id="379f9-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="379f9-112">az redis show</span><span class="sxs-lookup"><span data-stu-id="379f9-112">az redis show</span></span>](https://docs.microsoft.com/cli/azure/redis#show) | <span data-ttu-id="379f9-113">Recupera i dettagli di un'istanza di Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="379f9-113">Retrieve details of an Azure Redis Cache instance.</span></span> |
| [<span data-ttu-id="379f9-114">az redis list-keys</span><span class="sxs-lookup"><span data-stu-id="379f9-114">az redis list-keys</span></span>](https://docs.microsoft.com/cli/azure/redis#list-keys) | <span data-ttu-id="379f9-115">Recupera le chiavi di accesso per un'istanza di Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="379f9-115">Retrieve access keys for an Azure Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="379f9-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="379f9-116">Next steps</span></span>

<span data-ttu-id="379f9-117">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="379f9-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="379f9-118">Altri esempi di script dell'interfaccia della riga di comando della Cache Redis di Azure sono disponibili nella [documentazione della Cache Redis di Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="379f9-118">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>