---
title: Come usare Cache Redis di Azure con Node.js | Documentazione Microsoft
description: Introduzione all'uso di Cache Redis di Azure con Node.js e node_redis.
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: v-lincan
ms.assetid: 06fddc95-8029-4a8d-83f5-ebd5016891d9
ms.service: cache
ms.devlang: nodejs
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/10/2017
ms.author: sdanie
ms.openlocfilehash: 530191637b1aa91ee1d7fe5b5bb032c60983f7dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-redis-cache-with-nodejs"></a><span data-ttu-id="65128-103">Come usare Cache Redis di Azure con Node.js</span><span class="sxs-lookup"><span data-stu-id="65128-103">How to use Azure Redis Cache with Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="65128-104">.NET</span><span class="sxs-lookup"><span data-stu-id="65128-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="65128-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="65128-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="65128-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="65128-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="65128-107">Java</span><span class="sxs-lookup"><span data-stu-id="65128-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="65128-108">Python</span><span class="sxs-lookup"><span data-stu-id="65128-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="65128-109">Cache Redis di Azure consente di accedere a una cache Redis sicura e dedicata, gestita da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="65128-109">Azure Redis Cache gives you access to a secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="65128-110">È possibile accedere alla cache da qualsiasi applicazione in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="65128-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="65128-111">Questo argomento descrive come usare Cache Redis di Azure con Node.js.</span><span class="sxs-lookup"><span data-stu-id="65128-111">This topic shows you how to get started with Azure Redis Cache using Node.js.</span></span> <span data-ttu-id="65128-112">Per un altro esempio dell'uso di Cache Redis di Azure con Node,js, vedere [Creare un'applicazione di chat Node.js con Socket.IO in un sito Web di Azure](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span><span class="sxs-lookup"><span data-stu-id="65128-112">For another example of using Azure Redis Cache with Node.js, see [Build a Node.js Chat Application with Socket.IO on an Azure Website](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65128-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="65128-113">Prerequisites</span></span>
<span data-ttu-id="65128-114">Installare [node_redis](https://github.com/mranney/node_redis):</span><span class="sxs-lookup"><span data-stu-id="65128-114">Install [node_redis](https://github.com/mranney/node_redis):</span></span>

    npm install redis

<span data-ttu-id="65128-115">Questa esercitazione usa [node_redis](https://github.com/mranney/node_redis).</span><span class="sxs-lookup"><span data-stu-id="65128-115">This tutorial uses [node_redis](https://github.com/mranney/node_redis).</span></span> <span data-ttu-id="65128-116">Per esempi relativi all'uso di altri client Node.js, vedere la documentazione specifica dei client Node.js disponibile in [Node.js Redis clients](http://redis.io/clients#nodejs)(Client Redis Node.js).</span><span class="sxs-lookup"><span data-stu-id="65128-116">For examples of using other Node.js clients, see the individual documentation for the Node.js clients listed at [Node.js Redis clients](http://redis.io/clients#nodejs).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="65128-117">Creare una cache Redis in Azure</span><span class="sxs-lookup"><span data-stu-id="65128-117">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-the-host-name-and-access-keys"></a><span data-ttu-id="65128-118">Recuperare il nome host e le chiavi di accesso</span><span class="sxs-lookup"><span data-stu-id="65128-118">Retrieve the host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-to-the-cache-securely-using-ssl"></a><span data-ttu-id="65128-119">Connettersi in modo sicuro alla cache usando SSL</span><span class="sxs-lookup"><span data-stu-id="65128-119">Connect to the cache securely using SSL</span></span>
<span data-ttu-id="65128-120">Le build più recenti di [node_redis](https://github.com/mranney/node_redis) offrono il supporto per la connessione a Cache Redis di Azure con SSL.</span><span class="sxs-lookup"><span data-stu-id="65128-120">The latest builds of [node_redis](https://github.com/mranney/node_redis) provide support for connecting to Azure Redis Cache using SSL.</span></span> <span data-ttu-id="65128-121">L'esempio seguente mostra come connettersi a Cache Redis di Azure usando l'endpoint SSL 6380.</span><span class="sxs-lookup"><span data-stu-id="65128-121">The following example shows how to connect to Azure Redis Cache using the SSL endpoint of 6380.</span></span> <span data-ttu-id="65128-122">Sostituire `<name>` con il nome della cache e `<key>` con la chiave primaria o secondaria, come illustrato nella sezione [Recuperare il nome host e le chiavi di accesso](#retrieve-the-host-name-and-access-keys) precedente.</span><span class="sxs-lookup"><span data-stu-id="65128-122">Replace `<name>` with the name of your cache and `<key>` with either your primary or secondary key as described in the previous [Retrieve the host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> <span data-ttu-id="65128-123">Per le nuove istanze della Cache Redis di Azure la porta non SSL è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="65128-123">The non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="65128-124">Se si usa un client diverso che non supporta SSL, vedere [Come abilitare la porta non SSL](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="65128-124">If you are using a different client that doesn't support SSL, see [How to enable the non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-to-the-cache-and-retrieve-it"></a><span data-ttu-id="65128-125">Aggiungere dati alla cache e recuperarli</span><span class="sxs-lookup"><span data-stu-id="65128-125">Add something to the cache and retrieve it</span></span>
<span data-ttu-id="65128-126">L'esempio seguente mostra come connettersi a un'istanza di Cache Redis di Azure e come archiviare e recuperare un elemento dalla cache.</span><span class="sxs-lookup"><span data-stu-id="65128-126">The following example shows you how to connect to an Azure Redis Cache instance, and store and retrieve an item from the cache.</span></span> <span data-ttu-id="65128-127">Per altri esempi relativi all'uso di Redis con il client [node_redis](https://github.com/mranney/node_redis), vedere [http://redis.js.org/](http://redis.js.org/).</span><span class="sxs-lookup"><span data-stu-id="65128-127">For more examples of using Redis with the [node_redis](https://github.com/mranney/node_redis) client, see [http://redis.js.org/](http://redis.js.org/).</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

<span data-ttu-id="65128-128">Output:</span><span class="sxs-lookup"><span data-stu-id="65128-128">Output:</span></span>

    OK
    value


## <a name="next-steps"></a><span data-ttu-id="65128-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="65128-129">Next steps</span></span>
* <span data-ttu-id="65128-130">[Abilitare la diagnostica della cache](cache-how-to-monitor.md#enable-cache-diagnostics) per [monitorare](cache-how-to-monitor.md) l'integrità della cache.</span><span class="sxs-lookup"><span data-stu-id="65128-130">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) the health of your cache.</span></span>
* <span data-ttu-id="65128-131">Leggere la [documentazione ufficiale di Redis](http://redis.io/documentation).</span><span class="sxs-lookup"><span data-stu-id="65128-131">Read the official [Redis documentation](http://redis.io/documentation).</span></span>

