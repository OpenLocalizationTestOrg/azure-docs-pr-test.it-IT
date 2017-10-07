---
title: Provider di stato sessione ASP.NET aaaCache | Documenti Microsoft
description: Informazioni su come stato della sessione ASP.NET toostore usando Cache Redis di Azure
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 192f384c-836a-479a-bb65-8c3e6d6522bb
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 05/01/2017
ms.author: sdanie
ms.openlocfilehash: 9ea84cf67b9314b15dce696f596d399921194510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-session-state-provider-for-azure-redis-cache"></a>Provider di stato della sessione ASP.NET per Cache Redis di Azure
Cache Redis di Azure fornisce un provider di stato della sessione che è possibile utilizzare toostore lo stato della sessione in una cache anziché in memoria o in un Server SQL del database. toouse provider di stato sessione della memorizzazione nella cache di hello, configurare prima la cache e quindi configurare l'applicazione ASP.NET per cache con pacchetto NuGet lo stato della sessione di Cache Redis hello.

È spesso poco pratico in un tooavoid app cloud del mondo reale l'archiviazione di un tipo di stato per una sessione utente, ma alcuni approcci influire negativamente sulle prestazioni e scalabilità più rispetto ad altri. Se è stato toostore, la soluzione migliore hello tookeep hello quantità dello stato di piccole dimensioni e archiviarlo nel cookie. Se ciò non è possibile, hello è lo stato della sessione ASP.NET toouse con un provider di cache distribuita e in memoria. Hello la soluzione peggiore dal punto di vista delle prestazioni e scalabilità consiste toouse un provider di stato sessione sottoposti a backup di database. Questo argomento vengono fornite istruzioni sull'utilizzo di hello Provider di stato sessione ASP.NET per Cache Redis di Azure. Per informazioni sulle altre opzioni dello stato sessione, vedere [Opzioni dello stato della sessione ASP.NET](#aspnet-session-state-options).

## <a name="store-aspnet-session-state-in-hello-cache"></a>Archiviare lo stato della sessione ASP.NET nella cache di hello
Fare clic su un'applicazione client in Visual Studio usando pacchetto NuGet lo stato della sessione di Cache Redis hello, tooconfigure **Gestione pacchetti NuGet**, **Package Manager Console** da hello **strumenti** menu.

Esecuzione hello il seguente comando da hello `Package Manager Console` finestra.
    
```
Install-Package Microsoft.Web.RedisSessionStateProvider
```

> [!IMPORTANT]
> Se si utilizza una funzionalità di clustering dal livello premium hello hello, è necessario utilizzare [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 o versione successiva o un'eccezione viene generata. Lo spostamento too2.0.1 o versione successiva è una modifica sostanziale; Per ulteriori informazioni, vedere [v 2.0.0 dettagli sulle modifiche di rilievo](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details). In fase di hello dell'aggiornamento in questo articolo, versione corrente di hello di questo pacchetto è 2.2.3.
> 
> 

pacchetto NuGet del Provider dello stato sessione Redis Hello presenta una dipendenza sul pacchetto Stackexchange hello. Se il pacchetto di Stackexchange hello non è presente nel progetto, è installato.

>[!NOTE]
>In aggiunta toohello sicuro Stackexchange pacchetto, è inoltre disponibile hello stackexchange. Redis non-versione di nome sicuro. Se il progetto utilizza hello sicuro-versione priva di nome stackexchange. Redis che è necessario disinstallarla, in caso contrario si conflitti di denominazione nel progetto. Per altre informazioni su questi pacchetti, vedere [Configurare i client della cache .NET](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).
>
>

Hello NuGet pacchetto Scarica e aggiunge hello necessari riferimenti ad assembly e aggiunge hello seguente sezione nel file Web. config. In questa sezione di configurazione necessari hello per hello di toouse l'applicazione ASP.NET Provider di stato sessione di Cache Redis.

```xml
<sessionState mode="Custom" customProvider="MySessionStateStore">
    <providers>
    <!--
    <add name="MySessionStateStore"
           host = "127.0.0.1" [String]
        port = "" [number]
        accessKey = "" [String]
        ssl = "false" [true|false]
        throwOnError = "true" [true|false]
        retryTimeoutInMilliseconds = "0" [number]
        databaseId = "0" [number]
        applicationName = "" [String]
        connectionTimeoutInMilliseconds = "5000" [number]
        operationTimeoutInMilliseconds = "5000" [number]
    />
    -->
    <add name="MySessionStateStore" type="Microsoft.Web.Redis.RedisSessionStateProvider" host="127.0.0.1" accessKey="" ssl="false"/>
    </providers>
</sessionState>
```

Hello commentato sezione viene fornito un esempio di attributi di hello e le impostazioni di esempio per ogni attributo.

Configurare gli attributi di hello con i valori hello del pannello della cache nel portale di Microsoft Azure hello e hello altri valori in base alle esigenze. Per istruzioni sull'accesso alle proprietà della cache, vedere [Configurare le impostazioni di Cache Redis di Azure](cache-configure.md#configure-redis-cache-settings).

* **host** : specificare l'endpoint della cache.
* **porta** : utilizzare la porta non SSL o la porta SSL, a seconda delle impostazioni ssl hello.
* **accessKey** : utilizzare una chiave primaria o secondaria di hello per la cache.
* **SSL** : true se si desidera toosecure di comunicazioni cache/client con ssl; in caso contrario, false. Essere la porta corretta che toospecify hello.
  * porta non SSL Hello è disabilitata per impostazione predefinita per le nuove cache. Specificare true per questo hello toouse impostazione porta SSL. Per ulteriori informazioni sull'abilitazione della porta non SSL hello, vedere hello [porte di accesso](cache-configure.md#access-ports) sezione hello [configurare una cache](cache-configure.md) argomento.
* **throwOnError** : true se si desidera toobe un'eccezione generata se è presente un errore oppure false se si desidera hello operazione toofail invisibile all'utente. È possibile cercare un errore controllando la proprietà Microsoft.Web.Redis.RedisSessionStateProvider.LastException statica hello. valore predefinito di Hello è true.
* **retryTimeoutInMilliseconds** : le operazioni non riuscite vengono ritentate durante questo intervallo, specificato in millisecondi. primo tentativo di Hello avviene dopo 20 millisecondi e quindi tentativi vengono ripetuti ogni secondo fino alla scadenza di intervallo retryTimeoutInMilliseconds "hello". Immediatamente dopo questo intervallo, operazione hello viene ripetuta un'ultima volta. Se l'operazione di hello ancora non riesce, hello viene generata nuovamente toohello chiamante, a seconda impostazione throwOnError hello. valore predefinito di Hello è 0, ovvero viene eseguito alcun tentativo.
* **databaseId** : specifica quali toouse database per la cache di dati di output. Se non specificato, viene utilizzato il valore predefinito hello pari a 0.
* **applicationName**: le chiavi vengono archiviate in Redis come `{<Application Name>_<Session ID>}_Data`. Questo schema di denominazione consente a più applicazioni tooshare hello stessa istanza di Redis. Questo parametro è facoltativo e se non lo si specifica, verrà usato un valore predefinito.
* **connectionTimeoutInMilliseconds** : questa impostazione consente connectTimeout hello toooverride impostazione nel client stackexchange. Redis hello. Se non specificato, viene utilizzato connectTimeout impostazione hello pari a 5000. Per altre informazioni, vedere [Modello di configurazione StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).
* **operationTimeoutInMilliseconds** : questa impostazione consente toooverride hello syncTimeout impostazione nel client stackexchange. Redis hello. Se non specificato, viene utilizzato hello syncTimeout impostazione predefinita di 1000. Per altre informazioni, vedere [Modello di configurazione StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).

Per ulteriori informazioni su queste proprietà, vedere originale blog post annuncio hello al [annuncio i Provider di stato sessione ASP.NET per Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx).

Non dimenticare toocomment hello standard InProc sessione stato provider sezione nel file Web. config.

```xml
<!-- <sessionState mode="InProc"
     customProvider="DefaultSessionProvider">
     <providers>
        <add name="DefaultSessionProvider"
              type="System.Web.Providers.DefaultSessionStateProvider,
                    System.Web.Providers, Version=1.0.0.0, Culture=neutral,
                    PublicKeyToken=31bf3856ad364e35"
              connectionStringName="DefaultConnection" />
      </providers>
</sessionState> -->
```

Una volta completati questi passaggi, l'applicazione è configurata toouse hello Provider di stato sessione di Cache Redis. Quando si usa lo stato della sessione nell'applicazione, questo viene archiviato in un'istanza di Cache Redis di Azure.

> [!IMPORTANT]
> Dati memorizzati nella cache di hello devono essere serializzabili, a differenza dei dati di hello che possono essere archiviati in hello predefiniti Provider di stato sessione ASP.NET in memoria. Quando viene utilizzato il Provider di stato sessione per Redis hello, assicurarsi che i tipi di dati hello che vengono archiviati nello stato della sessione siano serializzabili.
> 
> 

## <a name="aspnet-session-state-options"></a>Opzioni dello stato della sessione ASP.NET
* Nel Provider di stato della sessione memoria - questo provider archivia lo stato della sessione hello in memoria. Hello vantaggio derivante dall'utilizzo questo provider è semplice e veloce. Non è però possibile ridimensionare le app Web se si usa il provider in memoria perché non viene distribuito.
* Questo provider: Provider di stato della sessione SQL Server archivia lo stato della sessione hello in Sql Server. Utilizzare questo provider, se si desidera lo stato della sessione hello toostore nell'archivio permanente. È possibile ridimensionare l'app Web, ma l'uso di SQL Server per la sessione ha effetto sulle prestazioni dell'app Web.
* Distribuito In memoria Provider dello stato sessione, ad esempio sessione stato Provider di Cache Redis - fornisce questo provider hello meglio di entrambi. L'app Web può avere un provider di stato della sessione semplice, veloce e scalabile. Poiché questo hello di provider archivia lo stato della sessione in una Cache, l'app ha tootake in considerazione tutti hello caratteristiche associate alla comunicazione con tooa distribuito nella Cache di memoria, ad esempio errori di rete temporanei. Per le procedure consigliate sull'uso della cache, vedere [Informazioni aggiuntive sulla memorizzazione nella cache](../best-practices-caching.md) in Microsoft Patterns & Practices e [Azure Cloud Application Design and Implementation Guidance](https://github.com/mspnp/azure-guidance) (Guida alla progettazione e all'implementazione delle applicazioni cloud di Azure).

Per altre informazioni sullo stato della sessione e altre procedure consigliate, vedere [Procedure consigliate per lo sviluppo Web (compilazione di app reali per il cloud con Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices).

## <a name="next-steps"></a>Passaggi successivi
Estrarre hello [Provider di Cache di Output ASP.NET per Cache Redis di Azure](cache-aspnet-output-cache-provider.md).

