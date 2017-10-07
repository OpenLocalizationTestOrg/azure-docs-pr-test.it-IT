---
title: aaaHow toouse Cache Redis di Azure con Java | Documenti Microsoft
description: Introduzione all'uso di Cache Redis di Azure con Java
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 29275a5e-2e39-4ef2-804f-7ecc5161eab9
ms.service: cache
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 04/13/2017
ms.author: sdanie
ms.openlocfilehash: 7768e879d71f61585b59cf4bd6634ba3f12e001d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-java"></a><span data-ttu-id="f849f-103">Come toouse Cache Redis di Azure con Java</span><span class="sxs-lookup"><span data-stu-id="f849f-103">How toouse Azure Redis Cache with Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f849f-104">.NET</span><span class="sxs-lookup"><span data-stu-id="f849f-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="f849f-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f849f-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="f849f-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="f849f-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="f849f-107">Java</span><span class="sxs-lookup"><span data-stu-id="f849f-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="f849f-108">Python</span><span class="sxs-lookup"><span data-stu-id="f849f-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="f849f-109">Azure consente di Cache Redis accedere tooa dedicato Redis cache gestita da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f849f-109">Azure Redis Cache gives you access tooa dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="f849f-110">È possibile accedere alla cache da qualsiasi applicazione in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f849f-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="f849f-111">In questo argomento viene illustrato come tooget iniziare con una Cache Redis di Azure utilizzando Java.</span><span class="sxs-lookup"><span data-stu-id="f849f-111">This topic shows you how tooget started with Azure Redis Cache using Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f849f-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f849f-112">Prerequisites</span></span>
<span data-ttu-id="f849f-113">[Jedis](https://github.com/xetorthio/jedis) : client Java per Redis</span><span class="sxs-lookup"><span data-stu-id="f849f-113">[Jedis](https://github.com/xetorthio/jedis) - Java client for Redis</span></span>

<span data-ttu-id="f849f-114">In questa esercitazione viene utilizzato Jedis, ma è possibile utilizzare qualsiasi cliente Java elencato in [http://redis.io/clients](http://redis.io/clients).</span><span class="sxs-lookup"><span data-stu-id="f849f-114">This tutorial uses Jedis, but you can use any Java client listed at [http://redis.io/clients](http://redis.io/clients).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="f849f-115">Creare una cache Redis in Azure</span><span class="sxs-lookup"><span data-stu-id="f849f-115">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a><span data-ttu-id="f849f-116">Recuperare le chiavi di accesso e sul nome host hello</span><span class="sxs-lookup"><span data-stu-id="f849f-116">Retrieve hello host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a><span data-ttu-id="f849f-117">La connessione della cache toohello in modo protetto con SSL</span><span class="sxs-lookup"><span data-stu-id="f849f-117">Connect toohello cache securely using SSL</span></span>
<span data-ttu-id="f849f-118">Hello build più recente di [jedis](https://github.com/xetorthio/jedis) forniscono supporto per la connessione della Cache Redis tooAzure mediante SSL.</span><span class="sxs-lookup"><span data-stu-id="f849f-118">hello latest builds of [jedis](https://github.com/xetorthio/jedis) provide support for connecting tooAzure Redis Cache using SSL.</span></span> <span data-ttu-id="f849f-119">Hello di esempio seguente viene illustrato come tooconnect tooAzure Cache Redis tramite hello endpoint SSL di 6380.</span><span class="sxs-lookup"><span data-stu-id="f849f-119">hello following example shows how tooconnect tooAzure Redis Cache using hello SSL endpoint of 6380.</span></span> <span data-ttu-id="f849f-120">Sostituire `<name>` con nome hello della cache e `<key>` con la chiave primaria o secondaria come descritto in hello precedente [recuperare le chiavi di accesso e sul nome host hello](#retrieve-the-host-name-and-access-keys) sezione.</span><span class="sxs-lookup"><span data-stu-id="f849f-120">Replace `<name>` with hello name of your cache and `<key>` with either your primary or secondary key as described in hello previous [Retrieve hello host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

    boolean useSsl = true;
    /* In this line, replace <name> with your cache name: */
    JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */

> [!NOTE]
> <span data-ttu-id="f849f-121">porta non SSL Hello è disabilitata per le nuove istanze di Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="f849f-121">hello non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="f849f-122">Se si utilizza un altro client che non supporta SSL, vedere [come tooenable hello porta non SSL](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="f849f-122">If you are using a different client that doesn't support SSL, see [How tooenable hello non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a><span data-ttu-id="f849f-123">Aggiungere un elemento toohello nella cache e recuperarlo</span><span class="sxs-lookup"><span data-stu-id="f849f-123">Add something toohello cache and retrieve it</span></span>
    package com.mycompany.app;
    import redis.clients.jedis.Jedis;
    import redis.clients.jedis.JedisShardInfo;

    public class App
    {
      public static void main( String[] args )
      {
        boolean useSsl = true;
        /* In this line, replace <name> with your cache name: */
        JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
        shardInfo.setPassword("<key>"); /* Use your access key. */
        Jedis jedis = new Jedis(shardInfo);
        jedis.set("foo", "bar");
        String value = jedis.get("foo");
      }
    }


## <a name="next-steps"></a><span data-ttu-id="f849f-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f849f-124">Next steps</span></span>
* <span data-ttu-id="f849f-125">[Abilitare la diagnostica della cache](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) in modo da poter [monitoraggio](https://msdn.microsoft.com/library/azure/dn763945.aspx) hello integrità della cache.</span><span class="sxs-lookup"><span data-stu-id="f849f-125">[Enable cache diagnostics](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) so you can [monitor](https://msdn.microsoft.com/library/azure/dn763945.aspx) hello health of your cache.</span></span>
* <span data-ttu-id="f849f-126">Lettura hello ufficiale [Redis documentazione](http://redis.io/documentation).</span><span class="sxs-lookup"><span data-stu-id="f849f-126">Read hello official [Redis documentation](http://redis.io/documentation).</span></span>
