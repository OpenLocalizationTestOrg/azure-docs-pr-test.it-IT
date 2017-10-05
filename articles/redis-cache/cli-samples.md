---
title: Esempi dell'interfaccia della riga di comando di Azure per Cache Redis | Microsoft Docs
description: Esempi dell'interfaccia della riga di comando di Azure per Cache Redis di Azure.
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 8d2de145-50c0-4f76-bf8f-fdf679f03698
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: a3debf3380b57faa5b7b30f612698fe6de5b7067
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cli-samples-for-azure-redis-cache"></a><span data-ttu-id="0c7df-103">Esempi dell'interfaccia della riga di comando di Azure per Cache Redis di Azure</span><span class="sxs-lookup"><span data-stu-id="0c7df-103">Azure CLI Samples for Azure Redis Cache</span></span>

<span data-ttu-id="0c7df-104">La tabella seguente include collegamenti a script Bash compilati tramite l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="0c7df-104">The following table includes links to bash scripts built using the Azure CLI.</span></span>

| | |
|---|---|
|<span data-ttu-id="0c7df-105">**Creare cache**</span><span class="sxs-lookup"><span data-stu-id="0c7df-105">**Create cache**</span></span>||
| [<span data-ttu-id="0c7df-106">Creare una cache</span><span class="sxs-lookup"><span data-stu-id="0c7df-106">Create a cache</span></span>](./scripts/create-cache.md) | <span data-ttu-id="0c7df-107">Crea un gruppo di risorse e una Cache Redis di Azure di base.</span><span class="sxs-lookup"><span data-stu-id="0c7df-107">Creates a resource group and a basic tier Azure Redis Cache.</span></span> |
| [<span data-ttu-id="0c7df-108">Creare una cache premium con il clustering</span><span class="sxs-lookup"><span data-stu-id="0c7df-108">Create a premium cache with clustering</span></span>](./scripts/create-premium-cache-cluster.md) | <span data-ttu-id="0c7df-109">Crea un gruppo di risorse e una cache premium con clustering abilitato.</span><span class="sxs-lookup"><span data-stu-id="0c7df-109">Creates a resource group and a premium tier cache with clustering enabled.</span></span>|
| [<span data-ttu-id="0c7df-110">Ottenere i dettagli della cache</span><span class="sxs-lookup"><span data-stu-id="0c7df-110">Get cache details</span></span>](./scripts/show-cache.md) | <span data-ttu-id="0c7df-111">Ottiene i dettagli di un'istanza di Cache Redis di Azure, incluso lo stato del provisioning.</span><span class="sxs-lookup"><span data-stu-id="0c7df-111">Gets details of an Azure Redis Cache instance, including provisioning status.</span></span> |
| [<span data-ttu-id="0c7df-112">Ottenere il nome host, le porte e le chiavi</span><span class="sxs-lookup"><span data-stu-id="0c7df-112">Get the hostname, ports, and keys</span></span>](./scripts/cache-keys-ports.md) | <span data-ttu-id="0c7df-113">Ottiene il nome host, le porte e le chiavi per un'istanza di Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="0c7df-113">Gets the hostname, ports, and keys for an Azure Redis Cache instance.</span></span> |
|<span data-ttu-id="0c7df-114">**App Web e cache**</span><span class="sxs-lookup"><span data-stu-id="0c7df-114">**Web app plus cache**</span></span>||
| [<span data-ttu-id="0c7df-115">Connettere un'App Web a una cache Redis</span><span class="sxs-lookup"><span data-stu-id="0c7df-115">Connect a web app to a redis cache</span></span>](./../app-service-web/scripts/app-service-cli-app-service-redis.md) | <span data-ttu-id="0c7df-116">Crea un'App Web di Azure e una Cache Redis, quindi aggiunge i dettagli della connessione Redis alle impostazioni dell'app.</span><span class="sxs-lookup"><span data-stu-id="0c7df-116">Creates an Azure web app and a redis cache, then adds the redis connection details to the app settings.</span></span> |
|<span data-ttu-id="0c7df-117">**Eliminare cache**</span><span class="sxs-lookup"><span data-stu-id="0c7df-117">**Delete cache**</span></span>||
| [<span data-ttu-id="0c7df-118">Eliminare una cache</span><span class="sxs-lookup"><span data-stu-id="0c7df-118">Delete a cache</span></span>](./scripts/delete-cache.md) | <span data-ttu-id="0c7df-119">Elimina un'istanza di Cache Redis di Azure</span><span class="sxs-lookup"><span data-stu-id="0c7df-119">Deletes an Azure Redis Cache instance</span></span>  |
| | |

<span data-ttu-id="0c7df-120">Per altre informazioni sull'interfaccia della riga di comando di Azure 2.0, vedere [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (Installare l'interfaccia della riga di comando di Azure 2.0) e [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) (Introduzione all'interfaccia della riga di comando di Azure 2.0).</span><span class="sxs-lookup"><span data-stu-id="0c7df-120">For more information about Azure CLI 2.0, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) and [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>