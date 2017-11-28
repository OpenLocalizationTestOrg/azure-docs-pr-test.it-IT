---
title: aaaHow toouse Cache Redis di Azure con Node.js | Documenti Microsoft
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
ms.openlocfilehash: dc8732041d2c4e5793e684e0c80b87a1c9d17f34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-nodejs"></a><span data-ttu-id="7657a-103">Come toouse Cache Redis di Azure con Node.js</span><span class="sxs-lookup"><span data-stu-id="7657a-103">How toouse Azure Redis Cache with Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7657a-104">.NET</span><span class="sxs-lookup"><span data-stu-id="7657a-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="7657a-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7657a-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="7657a-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="7657a-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="7657a-107">Java</span><span class="sxs-lookup"><span data-stu-id="7657a-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="7657a-108">Python</span><span class="sxs-lookup"><span data-stu-id="7657a-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="7657a-109">Azure offre Cache Redis è accedere tooa sicura e dedicata cache Redis, gestita da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7657a-109">Azure Redis Cache gives you access tooa secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="7657a-110">È possibile accedere alla cache da qualsiasi applicazione in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7657a-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="7657a-111">In questo argomento viene illustrato come tooget iniziare con una Cache Redis di Azure utilizzando Node.js.</span><span class="sxs-lookup"><span data-stu-id="7657a-111">This topic shows you how tooget started with Azure Redis Cache using Node.js.</span></span> <span data-ttu-id="7657a-112">Per un altro esempio dell'uso di Cache Redis di Azure con Node,js, vedere [Creare un'applicazione di chat Node.js con Socket.IO in un sito Web di Azure](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span><span class="sxs-lookup"><span data-stu-id="7657a-112">For another example of using Azure Redis Cache with Node.js, see [Build a Node.js Chat Application with Socket.IO on an Azure Website](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7657a-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7657a-113">Prerequisites</span></span>
<span data-ttu-id="7657a-114">Installare [node_redis](https://github.com/mranney/node_redis):</span><span class="sxs-lookup"><span data-stu-id="7657a-114">Install [node_redis](https://github.com/mranney/node_redis):</span></span>

    npm install redis

<span data-ttu-id="7657a-115">Questa esercitazione usa [node_redis](https://github.com/mranney/node_redis).</span><span class="sxs-lookup"><span data-stu-id="7657a-115">This tutorial uses [node_redis](https://github.com/mranney/node_redis).</span></span> <span data-ttu-id="7657a-116">Per esempi di utilizzo di altri client di Node.js, vedere documentazione di singoli hello per i client di Node.js hello elencati in [client Redis Node.js](http://redis.io/clients#nodejs).</span><span class="sxs-lookup"><span data-stu-id="7657a-116">For examples of using other Node.js clients, see hello individual documentation for hello Node.js clients listed at [Node.js Redis clients](http://redis.io/clients#nodejs).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="7657a-117">Creare una cache Redis in Azure</span><span class="sxs-lookup"><span data-stu-id="7657a-117">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a><span data-ttu-id="7657a-118">Recuperare le chiavi di accesso e sul nome host hello</span><span class="sxs-lookup"><span data-stu-id="7657a-118">Retrieve hello host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a><span data-ttu-id="7657a-119">La connessione della cache toohello in modo protetto con SSL</span><span class="sxs-lookup"><span data-stu-id="7657a-119">Connect toohello cache securely using SSL</span></span>
<span data-ttu-id="7657a-120">Hello build più recente di [node_redis](https://github.com/mranney/node_redis) forniscono supporto per la connessione della Cache Redis tooAzure mediante SSL.</span><span class="sxs-lookup"><span data-stu-id="7657a-120">hello latest builds of [node_redis](https://github.com/mranney/node_redis) provide support for connecting tooAzure Redis Cache using SSL.</span></span> <span data-ttu-id="7657a-121">Hello di esempio seguente viene illustrato come tooconnect tooAzure Cache Redis tramite hello endpoint SSL di 6380.</span><span class="sxs-lookup"><span data-stu-id="7657a-121">hello following example shows how tooconnect tooAzure Redis Cache using hello SSL endpoint of 6380.</span></span> <span data-ttu-id="7657a-122">Sostituire `<name>` con nome hello della cache e `<key>` con la chiave primaria o secondaria come descritto in hello precedente [recuperare le chiavi di accesso e sul nome host hello](#retrieve-the-host-name-and-access-keys) sezione.</span><span class="sxs-lookup"><span data-stu-id="7657a-122">Replace `<name>` with hello name of your cache and `<key>` with either your primary or secondary key as described in hello previous [Retrieve hello host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> <span data-ttu-id="7657a-123">porta non SSL Hello è disabilitata per le nuove istanze di Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="7657a-123">hello non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="7657a-124">Se si utilizza un altro client che non supporta SSL, vedere [come tooenable hello porta non SSL](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="7657a-124">If you are using a different client that doesn't support SSL, see [How tooenable hello non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a><span data-ttu-id="7657a-125">Aggiungere un elemento toohello nella cache e recuperarlo</span><span class="sxs-lookup"><span data-stu-id="7657a-125">Add something toohello cache and retrieve it</span></span>
<span data-ttu-id="7657a-126">Hello nel seguente esempio viene illustrato come tooconnect tooan Redis di Azure nella Cache di istanza, archiviare e recuperare un elemento dalla cache di hello.</span><span class="sxs-lookup"><span data-stu-id="7657a-126">hello following example shows you how tooconnect tooan Azure Redis Cache instance, and store and retrieve an item from hello cache.</span></span> <span data-ttu-id="7657a-127">Per ulteriori esempi di utilizzo di Redis con hello [node_redis](https://github.com/mranney/node_redis) client, vedere [http://redis.js.org/](http://redis.js.org/).</span><span class="sxs-lookup"><span data-stu-id="7657a-127">For more examples of using Redis with hello [node_redis](https://github.com/mranney/node_redis) client, see [http://redis.js.org/](http://redis.js.org/).</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

<span data-ttu-id="7657a-128">Output:</span><span class="sxs-lookup"><span data-stu-id="7657a-128">Output:</span></span>

    OK
    value


## <a name="next-steps"></a><span data-ttu-id="7657a-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7657a-129">Next steps</span></span>
* <span data-ttu-id="7657a-130">[Abilitare la diagnostica della cache](cache-how-to-monitor.md#enable-cache-diagnostics) in modo da poter [monitoraggio](cache-how-to-monitor.md) hello integrità della cache.</span><span class="sxs-lookup"><span data-stu-id="7657a-130">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) hello health of your cache.</span></span>
* <span data-ttu-id="7657a-131">Lettura hello ufficiale [Redis documentazione](http://redis.io/documentation).</span><span class="sxs-lookup"><span data-stu-id="7657a-131">Read hello official [Redis documentation](http://redis.io/documentation).</span></span>

