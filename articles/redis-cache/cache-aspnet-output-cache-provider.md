---
title: aaaCache Provider della Cache di Output ASP.NET
description: Informazioni su come Output della pagina ASP.NET toocache usando Cache Redis di Azure
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 78469a66-0829-484f-8660-b2598ec60fbf
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/14/2017
ms.author: sdanie
ms.openlocfilehash: fc38cc657604b351f55ad8febac383783ac29700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a>Provider di cache di output ASP.NET per la Cache Redis di Azure
Hello redis-Provider della Cache di Output è un meccanismo di memorizzazione out-of-process per i dati della cache di output. Tali dati sono specificamente utilizzati per le risposte HTTP complete (memorizzazione nella cache di output delle pagine). Hello provider si collega hello nuovo output cache provider punto di estendibilità che è stato introdotto in ASP.NET 4.

Ciao toouse redis-Provider della Cache di Output, configurare prima la cache e quindi configurare l'applicazione ASP.NET mediante pacchetto NuGet del Provider della Cache Output Redis hello. Questo argomento fornisce indicazioni sulla configurazione del hello toouse applicazione redis-Provider della Cache di Output. Per altre informazioni sulla creazione e sulla configurazione di un'istanza della Cache Redis di Azure, vedere [Creare una cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).

## <a name="store-aspnet-page-output-in-hello-cache"></a>Archiviare l'output delle pagine ASP.NET nella cache di hello
Fare clic su un'applicazione client in Visual Studio usando pacchetto NuGet lo stato della sessione di Cache Redis hello, tooconfigure **Gestione pacchetti NuGet**, **Package Manager Console** da hello **strumenti** menu.

Esecuzione hello il seguente comando da hello `Package Manager Console` finestra.
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

pacchetto NuGet del Provider della Cache Output Redis Hello presenta una dipendenza sul pacchetto Stackexchange hello. Se il pacchetto di Stackexchange hello non è presente nel progetto, è installato. Per ulteriori informazioni sul pacchetto NuGet del Provider della Cache Redis Output di hello, vedere hello [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) pagina NuGet.

>[!NOTE]
>In aggiunta toohello sicuro Stackexchange pacchetto, è inoltre disponibile hello stackexchange. Redis non-versione di nome sicuro. Se il progetto utilizza hello sicuro-versione priva di nome stackexchange. Redis che è necessario disinstallarla, in caso contrario si conflitti di denominazione nel progetto. Per altre informazioni su questi pacchetti, vedere [Configurare i client della cache .NET](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).
>
>

Hello NuGet pacchetto Scarica e aggiunge hello necessari riferimenti ad assembly e aggiunge hello seguente sezione nel file Web. config. In questa sezione di configurazione necessari hello per hello di toouse l'applicazione ASP.NET redis-Provider della Cache di Output.

```xml
<caching>
  <outputCachedefault Provider="MyRedisOutputCache">
    <providers>
      <!--
      <add name="MyRedisOutputCache"
        host = "127.0.0.1" [String]
        port = "" [number]
        accessKey = "" [String]
        ssl = "false" [true|false]
        databaseId = "0" [number]
        applicationName = "" [String]
        connectionTimeoutInMilliseconds = "5000" [number]
        operationTimeoutInMilliseconds = "5000" [number]
      />
      -->
      <add name="MyRedisOutputCache" type="Microsoft.Web.Redis.RedisOutputCacheProvider" host="127.0.0.1" accessKey="" ssl="false"/>
    </providers>
  </outputCache>
</caching>
```

Hello commentato sezione viene fornito un esempio di attributi di hello e le impostazioni di esempio per ogni attributo.

Configurare gli attributi di hello con i valori hello del pannello della cache nel portale di Microsoft Azure hello e hello altri valori in base alle esigenze. Per istruzioni sull'accesso alle proprietà della cache, vedere [Configurare le impostazioni di Cache Redis di Azure](cache-configure.md#configure-redis-cache-settings).

* **host** : specificare l'endpoint della cache.
* **porta** : utilizzare la porta non SSL o la porta SSL, a seconda delle impostazioni ssl hello.
* **accessKey** : utilizzare una chiave primaria o secondaria di hello per la cache.
* **SSL** : true se si desidera toosecure di comunicazioni cache/client con ssl; in caso contrario, false. Essere la porta corretta che toospecify hello.
  * porta non SSL Hello è disabilitata per impostazione predefinita per le nuove cache. Specificare true per questo hello toouse impostazione porta SSL. Per ulteriori informazioni sull'abilitazione della porta non SSL hello, vedere hello [porte di accesso](cache-configure.md#access-ports) sezione hello [configurare una cache](cache-configure.md) argomento.
* **databaseId** – toouse quali database per la cache di dati di output specificato. Se non specificato, viene utilizzato il valore predefinito hello pari a 0.
* **applicationName**: le chiavi vengono archiviate in Redis come `<AppName>_<SessionId>_Data`. Questo schema di denominazione consente più hello tooshare di applicazioni stessa chiave. Questo parametro è facoltativo e se non lo si specifica, verrà usato un valore predefinito.
* **connectionTimeoutInMilliseconds** : questa impostazione consente connectTimeout hello toooverride impostazione nel client stackexchange. Redis hello. Se non specificato, viene utilizzato connectTimeout impostazione hello pari a 5000. Per altre informazioni, vedere [Modello di configurazione StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).
* **operationTimeoutInMilliseconds** : questa impostazione consente toooverride hello syncTimeout impostazione nel client stackexchange. Redis hello. Se non specificato, viene utilizzato hello syncTimeout impostazione predefinita di 1000. Per altre informazioni, vedere [Modello di configurazione StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).

Aggiungere una pagina tooeach direttiva OutputCache per i quali si desidera toocache output di hello.

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

Nell'esempio precedente hello hello memorizzati nella cache pagina dati restano nella cache di hello per 60 secondi, e una versione diversa della pagina hello viene memorizzato nella cache per ogni combinazione di parametri. Per ulteriori informazioni sulla direttiva OutputCache hello, vedere [ @OutputCache ](http://go.microsoft.com/fwlink/?linkid=320837).

Una volta completati questi passaggi, l'applicazione è configurata toouse hello redis-Provider della Cache di Output.

## <a name="next-steps"></a>Passaggi successivi
Estrarre hello [Provider di stato sessione ASP.NET per Cache Redis di Azure](cache-aspnet-session-state-provider.md).

