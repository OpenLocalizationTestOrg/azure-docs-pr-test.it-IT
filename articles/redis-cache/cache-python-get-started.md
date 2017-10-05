---
title: Come usare Cache Redis di Azure con Python | Documentazione Microsoft
description: Introduzione all'uso di Cache Redis di Azure con Python
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: v-lincan
ms.assetid: f186202c-fdad-4398-af8c-aee91ec96ba3
ms.service: cache
ms.devlang: python
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/10/2017
ms.author: sdanie
ms.openlocfilehash: cdbee52574d0ffbe82ef3dc98f2848f4d00ba2ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-redis-cache-with-python"></a><span data-ttu-id="05776-103">Come usare Cache Redis di Azure con Python</span><span class="sxs-lookup"><span data-stu-id="05776-103">How to use Azure Redis Cache with Python</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="05776-104">.NET</span><span class="sxs-lookup"><span data-stu-id="05776-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="05776-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="05776-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="05776-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="05776-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="05776-107">Java</span><span class="sxs-lookup"><span data-stu-id="05776-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="05776-108">Python</span><span class="sxs-lookup"><span data-stu-id="05776-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="05776-109">Questo argomento descrive come usare Cache Redis di Azure con Python.</span><span class="sxs-lookup"><span data-stu-id="05776-109">This topic shows you how to get started with Azure Redis Cache using Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05776-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="05776-110">Prerequisites</span></span>
<span data-ttu-id="05776-111">Installare [redis-py](https://github.com/andymccurdy/redis-py).</span><span class="sxs-lookup"><span data-stu-id="05776-111">Install [redis-py](https://github.com/andymccurdy/redis-py).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="05776-112">Creare una cache Redis in Azure</span><span class="sxs-lookup"><span data-stu-id="05776-112">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-the-host-name-and-access-keys"></a><span data-ttu-id="05776-113">Recuperare il nome host e le chiavi di accesso</span><span class="sxs-lookup"><span data-stu-id="05776-113">Retrieve the host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="enable-the-non-ssl-endpoint"></a><span data-ttu-id="05776-114">Abilitare l'endpoint non SSL</span><span class="sxs-lookup"><span data-stu-id="05776-114">Enable the non-SSL endpoint</span></span>
<span data-ttu-id="05776-115">Alcuni client Redis non supportano SSL e per impostazione predefinita la [porta non SSL è disabilitata per le nuove istanze della cache Redis di Azure](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="05776-115">Some Redis clients don't support SSL, and by default the [non-SSL port is disabled for new Azure Redis Cache instances](cache-configure.md#access-ports).</span></span> <span data-ttu-id="05776-116">Al momento della stesura di questo articolo, il client [redis-py](https://github.com/andymccurdy/redis-py) non supporta SSL.</span><span class="sxs-lookup"><span data-stu-id="05776-116">At the time of this writing, the [redis-py](https://github.com/andymccurdy/redis-py) client doesn't support SSL.</span></span> 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-non-ssl-port.md)]

## <a name="add-something-to-the-cache-and-retrieve-it"></a><span data-ttu-id="05776-117">Aggiungere dati alla cache e recuperarli</span><span class="sxs-lookup"><span data-stu-id="05776-117">Add something to the cache and retrieve it</span></span>
    >>> import redis
    >>> r = redis.StrictRedis(host='<name>.redis.cache.windows.net',
          port=6380, db=0, password='<key>', ssl=True)
    >>> r.set('foo', 'bar')
    True
    >>> r.get('foo')
    b'bar'


<span data-ttu-id="05776-118">Sostituire `<name>` con il nome della cache e `key` con la chiave di accesso.</span><span class="sxs-lookup"><span data-stu-id="05776-118">Replace `<name>` with your cache name and `key` with your access key.</span></span>

<!--Image references-->
[1]: ./media/cache-python-get-started/redis-cache-new-cache-menu.png
[2]: ./media/cache-python-get-started/redis-cache-cache-create.png
