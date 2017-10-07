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
# <a name="how-toouse-azure-redis-cache-with-java"></a>Come toouse Cache Redis di Azure con Java
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.JS](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Azure consente di Cache Redis accedere tooa dedicato Redis cache gestita da Microsoft. È possibile accedere alla cache da qualsiasi applicazione in Microsoft Azure.

In questo argomento viene illustrato come tooget iniziare con una Cache Redis di Azure utilizzando Java.

## <a name="prerequisites"></a>Prerequisiti
[Jedis](https://github.com/xetorthio/jedis) : client Java per Redis

In questa esercitazione viene utilizzato Jedis, ma è possibile utilizzare qualsiasi cliente Java elencato in [http://redis.io/clients](http://redis.io/clients).

## <a name="create-a-redis-cache-on-azure"></a>Creare una cache Redis in Azure
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a>Recuperare le chiavi di accesso e sul nome host hello
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a>La connessione della cache toohello in modo protetto con SSL
Hello build più recente di [jedis](https://github.com/xetorthio/jedis) forniscono supporto per la connessione della Cache Redis tooAzure mediante SSL. Hello di esempio seguente viene illustrato come tooconnect tooAzure Cache Redis tramite hello endpoint SSL di 6380. Sostituire `<name>` con nome hello della cache e `<key>` con la chiave primaria o secondaria come descritto in hello precedente [recuperare le chiavi di accesso e sul nome host hello](#retrieve-the-host-name-and-access-keys) sezione.

    boolean useSsl = true;
    /* In this line, replace <name> with your cache name: */
    JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */

> [!NOTE]
> porta non SSL Hello è disabilitata per le nuove istanze di Cache Redis di Azure. Se si utilizza un altro client che non supporta SSL, vedere [come tooenable hello porta non SSL](cache-configure.md#access-ports).
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a>Aggiungere un elemento toohello nella cache e recuperarlo
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


## <a name="next-steps"></a>Passaggi successivi
* [Abilitare la diagnostica della cache](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) in modo da poter [monitoraggio](https://msdn.microsoft.com/library/azure/dn763945.aspx) hello integrità della cache.
* Lettura hello ufficiale [Redis documentazione](http://redis.io/documentation).
