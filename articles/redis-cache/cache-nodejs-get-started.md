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
# <a name="how-toouse-azure-redis-cache-with-nodejs"></a>Come toouse Cache Redis di Azure con Node.js
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.JS](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Azure offre Cache Redis è accedere tooa sicura e dedicata cache Redis, gestita da Microsoft. È possibile accedere alla cache da qualsiasi applicazione in Microsoft Azure.

In questo argomento viene illustrato come tooget iniziare con una Cache Redis di Azure utilizzando Node.js. Per un altro esempio dell'uso di Cache Redis di Azure con Node,js, vedere [Creare un'applicazione di chat Node.js con Socket.IO in un sito Web di Azure](../app-service-web/web-sites-nodejs-chat-app-socketio.md).

## <a name="prerequisites"></a>Prerequisiti
Installare [node_redis](https://github.com/mranney/node_redis):

    npm install redis

Questa esercitazione usa [node_redis](https://github.com/mranney/node_redis). Per esempi di utilizzo di altri client di Node.js, vedere documentazione di singoli hello per i client di Node.js hello elencati in [client Redis Node.js](http://redis.io/clients#nodejs).

## <a name="create-a-redis-cache-on-azure"></a>Creare una cache Redis in Azure
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a>Recuperare le chiavi di accesso e sul nome host hello
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a>La connessione della cache toohello in modo protetto con SSL
Hello build più recente di [node_redis](https://github.com/mranney/node_redis) forniscono supporto per la connessione della Cache Redis tooAzure mediante SSL. Hello di esempio seguente viene illustrato come tooconnect tooAzure Cache Redis tramite hello endpoint SSL di 6380. Sostituire `<name>` con nome hello della cache e `<key>` con la chiave primaria o secondaria come descritto in hello precedente [recuperare le chiavi di accesso e sul nome host hello](#retrieve-the-host-name-and-access-keys) sezione.

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> porta non SSL Hello è disabilitata per le nuove istanze di Cache Redis di Azure. Se si utilizza un altro client che non supporta SSL, vedere [come tooenable hello porta non SSL](cache-configure.md#access-ports).
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a>Aggiungere un elemento toohello nella cache e recuperarlo
Hello nel seguente esempio viene illustrato come tooconnect tooan Redis di Azure nella Cache di istanza, archiviare e recuperare un elemento dalla cache di hello. Per ulteriori esempi di utilizzo di Redis con hello [node_redis](https://github.com/mranney/node_redis) client, vedere [http://redis.js.org/](http://redis.js.org/).

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

Output:

    OK
    value


## <a name="next-steps"></a>Passaggi successivi
* [Abilitare la diagnostica della cache](cache-how-to-monitor.md#enable-cache-diagnostics) in modo da poter [monitoraggio](cache-how-to-monitor.md) hello integrità della cache.
* Lettura hello ufficiale [Redis documentazione](http://redis.io/documentation).

