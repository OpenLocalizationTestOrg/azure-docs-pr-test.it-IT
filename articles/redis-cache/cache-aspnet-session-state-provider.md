---
title: Provider di stato della sessione ASP.NET per la cache | Microsoft Docs
description: Informazioni su come archiviare lo stato della sessione ASP.NET con Cache Redis di Azure
services: redis-cache
documentationcenter: na
author: wesmc7777
manager: cfowler
editor: tysonn
ms.assetid: 192f384c-836a-479a-bb65-8c3e6d6522bb
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 05/01/2017
ms.author: wesmc
ms.openlocfilehash: 485375f2f2ffb83b7d0fdeef8daab5880a8bbc27
ms.sourcegitcommit: 2a70752d0987585d480f374c3e2dba0cd5097880
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/19/2018
---
# <a name="aspnet-session-state-provider-for-azure-redis-cache"></a>Provider di stato della sessione ASP.NET per Cache Redis di Azure
Cache Redis di Azure include un provider di stato della sessione che consente di archiviare lo stato della sessione in una cache anziché in memoria o in un database di SQL Server. Per usare il provider di stato della sessione di memorizzazione nella cache, configurare innanzitutto la cache e quindi l'applicazione ASP.NET per la cache usando il pacchetto NuGet dello stato della sessione per Cache Redis.

In un'app reale per il cloud spesso non è facile evitare di archiviare qualche forma di stato per una sessione utente, ma alcuni approcci hanno più effetto di altri sulle prestazioni e sulla scalabilità. Se è necessario archiviare lo stato, la soluzione migliore è mantenere piccola la quantità di stato e archiviarla nei cookie. Se non è fattibile, la seconda miglior soluzione è usare lo stato della sessione ASP.NET con un provider per la cache distribuita in memoria. La soluzione peggiore dal punto di vista delle prestazioni e della scalabilità è usare un provider di stato della sessione supportato da un database. Questo argomento fornisce indicazioni sull'uso del provider di stato della sessione ASP.NET per Cache Redis di Azure. Per informazioni sulle altre opzioni dello stato sessione, vedere [Opzioni dello stato della sessione ASP.NET](#aspnet-session-state-options).

## <a name="store-aspnet-session-state-in-the-cache"></a>Archiviare lo stato della sessione ASP.NET nella cache
Per configurare un'applicazione client in Visual Studio con il pacchetto NuGet Redis Cache Session State, fare clic su **Gestione pacchetti NuGet** e quindi su **Console di Gestione pacchetti** dal menu **Strumenti**.

Eseguire questo comando nella finestra `Package Manager Console`.
    
```
Install-Package Microsoft.Web.RedisSessionStateProvider
```

> [!IMPORTANT]
> Se si sta usando la funzionalità di clustering del livello Premium, è necessario usare [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 o versione successiva. In caso contrario, verrà generata un'eccezione. Il passaggio alla versione 2.0.1 o successiva è una modifica significativa. Per altre informazioni, vedere la pagina relativa ai [dettagli delle modifiche significative della versione 2.2.0](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details). Al momento dell'aggiornamento di questo articolo, la versione corrente del pacchetto è 2.2.3.
> 
> 

Il pacchetto NuGet del provider di stato della sessione Redis ha una dipendenza dal pacchetto StackExchange.Redis.StrongName. Se il pacchetto StackExchange.Redis.StrongName non è presente nel progetto, viene installato.

>[!NOTE]
>Oltre al pacchetto StackExchange.Redis.StrongName con nome sicuro, è disponibile anche la versione StackExchange.Redis priva di nome sicuro. Se il progetto usa la versione di StackExchange.Redis con nome non sicuro, è necessario disinstallarla per evitare conflitti di denominazione nel progetto. Per altre informazioni su questi pacchetti, vedere [Configurare i client della cache .NET](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).
>
>

Il pacchetto NuGet scarica e aggiunge i riferimenti all'assembly richiesto e aggiunge la sezione seguente al file web.config. Questa sezione contiene la configurazione richiesta dall'applicazione ASP.NET per usare il provider di stato della sessione Cache Redis.

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

La sezione commentata fornisce un esempio degli attributi e delle impostazioni di esempio per ogni attributo.

Configurare gli attributi con i valori del pannello Cache nel portale di Microsoft Azure e configurare gli altri valori come desiderato. Per istruzioni sull'accesso alle proprietà della cache, vedere [Configurare le impostazioni di Cache Redis di Azure](cache-configure.md#configure-redis-cache-settings).

* **host** : specificare l'endpoint della cache.
* **port** : usare la porta non SSL o la porta SSL, in base alle impostazioni SSL.
* **accessKey** : usare la chiave primaria o secondaria per la cache.
* **ssl** :  true per proteggere le comunicazioni cache/client con SSL; in caso contrario, false. Assicurarsi di specificare la porta corretta.
  * Per le nuove cache la porta senza SSL è disabilitata per impostazione predefinita. Specificare true per questa impostazione per usare la porta SSL. Per altre informazioni sull'abilitazione della porta senza SSL, vedere la sezione [Porte di accesso](cache-configure.md#access-ports) nell'argomento [Configurare una cache](cache-configure.md).
* **throwOnError**: impostare su true se si vuole che venga generata un'eccezione in caso di errore durante l'operazione; in caso contrario, scegliere false. È possibile verificare la presenza di un errore controllando la proprietà statica Microsoft.Web.Redis.RedisSessionStateProvider.LastException. Il valore predefinito è true.
* **retryTimeoutInMilliseconds** : le operazioni non riuscite vengono ritentate durante questo intervallo, specificato in millisecondi. Il primo tentativo si verifica dopo 20 millisecondi e quelli successivi dopo ogni secondo fino alla scadenza dell'intervallo retryTimeoutInMilliseconds. Immediatamente dopo questo intervallo, l'operazione viene ritentata un'ultima volta. Se l'operazione non riesce ancora, l'eccezione viene generata per il chiamante, in base all'impostazione di throwOnError. Il valore predefinito è 0 che indica nessun tentativo.
* **databaseId** : specifica il database da usare per i dati di output della cache. Se non è specificato alcun valore, verrà usato il valore predefinito 0.
* **applicationName**: le chiavi vengono archiviate in Redis come `{<Application Name>_<Session ID>}_Data`. Questo schema di denominazione consente a più applicazioni di condividere la stessa istanza di Redis. Questo parametro è facoltativo e se non lo si specifica, verrà usato un valore predefinito.
* **connectionTimeoutInMilliseconds** : questa impostazione consente di eseguire l'override dell'impostazione connectTimeout nel client StackExchange.Redis. Se non viene specificato alcun valore, verrà usata l'impostazione di connectTimeout predefinita pari a 5000. Per altre informazioni, vedere [Modello di configurazione StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).
* **operationTimeoutInMilliseconds** : questa impostazione consente di eseguire l'override dell'impostazione syncTimeout nel client StackExchange.Redis. Se non viene specificato alcun valore, verrà usata l'impostazione di syncTimeout predefinita pari a 1000. Per altre informazioni, vedere [Modello di configurazione StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).

Per altre informazioni su queste proprietà, vedere il post di blog originale nell' [annuncio del provider di stato della sessione ASP.NET per Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx).

Non dimenticare di impostare come commento la sezione del provider di stato della sessione InProc standard nel file web.config.

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

Dopo l'esecuzione di questi passaggi, l'applicazione è configurata per l'uso del provider di stato della sessione Cache Redis. Quando si usa lo stato della sessione nell'applicazione, questo viene archiviato in un'istanza di Cache Redis di Azure.

> [!IMPORTANT]
> I dati archiviati nella cache devono essere serializzabili, diversamente dai dati che possono essere archiviati nel provider di stato della sessione ASP.NET in memoria predefinito. Quando il provider di stato della sessione per Redis viene usato, assicurarsi che i tipi di dati da archiviare nello stato della sessione siano serializzabili.
> 
> 

## <a name="aspnet-session-state-options"></a>Opzioni dello stato della sessione ASP.NET
* Provider di stato della sessione in memoria: questo provider archivia lo stato della sessione in memoria. Il vantaggio di usare questo provider è che è semplice e veloce. Non è però possibile ridimensionare le app Web se si usa il provider in memoria perché non viene distribuito.
* Provider di stato della sessione SQL Server: questo provider archivia lo stato della sessione in SQL Server. Usare questo provider per archiviare lo stato della sessione in una risorsa di archiviazione persistente. È possibile ridimensionare l'app Web, ma l'uso di SQL Server per la sessione ha effetto sulle prestazioni dell'app Web.
* Provider di stato della sessione in memoria distribuito, ad esempio provider di stato della sessione di Cache Redis: questo provider offre il meglio di entrambe le soluzioni. L'app Web può avere un provider di stato della sessione semplice, veloce e scalabile. Dal momento che questo provider archivia lo stato della sessione in una cache, l'app deve tenere in considerazione tutte le caratteristiche associate quando comunica con una cache in memoria distribuita, ad esempio in caso di errori di rete temporanei. Per le procedure consigliate sull'uso della cache, vedere [Informazioni aggiuntive sulla memorizzazione nella cache](../best-practices-caching.md) in Microsoft Patterns & Practices e [Azure Cloud Application Design and Implementation Guidance](https://github.com/mspnp/azure-guidance) (Guida alla progettazione e all'implementazione delle applicazioni cloud di Azure).

Per altre informazioni sullo stato della sessione e altre procedure consigliate, vedere [Procedure consigliate per lo sviluppo Web (compilazione di app reali per il cloud con Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices).

## <a name="next-steps"></a>Passaggi successivi
Vedere [Provider di cache di output ASP.NET per la Cache Redis di Azure](cache-aspnet-output-cache-provider.md).

