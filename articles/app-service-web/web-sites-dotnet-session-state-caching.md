---
title: stato aaaSession con Azure Redis cache in Azure App Service
description: Informazioni su come toouse hello servizio Cache di Azure toosupport ASP.NET sessione dello stato di memorizzazione nella cache.
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
manager: erikre
editor: none
ms.assetid: 4f98d289-2698-464d-85cd-99ec40fad1f2
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 06/27/2016
ms.author: riande
ms.openlocfilehash: f689b6754ea072aa195f822ab6482f4bf2748375
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="session-state-with-azure-redis-cache-in-azure-app-service"></a>Stato della sessione con Cache Redis di Azure in Servizio app di Azure
In questo argomento viene illustrato come toouse hello servizio Cache Redis di Azure per lo stato della sessione.

Se l'app web ASP.NET utilizza lo stato della sessione, è necessario tooconfigure un provider di stato sessione esterno (servizio Cache Redis hello o un provider di stato sessione SQL Server). Se si utilizza lo stato della sessione e non utilizza un provider esterno, sarà limitato tooone istanza dell'app web. Servizio Cache Redis Hello è hello più semplice e rapido tooenable.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a id="createcache"></a>Creare una Cache di hello
Seguire [queste direzioni](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) toocreate cache di hello.

## <a id="configureproject"></a>Aggiungere hello RedisSessionStateProvider NuGet pacchetto tooyour web app
Installare hello NuGet `RedisSessionStateProvider` pacchetto.  Comando che segue di hello utilizzare tooinstall dalla console di gestione pacchetti hello (**strumenti** > **Gestione pacchetti NuGet** > **Package Manager Console**):

  `PM> Install-Package Microsoft.Web.RedisSessionStateProvider`

tooinstall da **strumenti** > **Gestione pacchetti NuGet** > **gestire NugGet pacchetti per la soluzione**, cercare `RedisSessionStateProvider`.

Per ulteriori informazioni, vedere hello [pagina NuGet RedisSessionStateProvider](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) e [client della cache di hello configura](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).

## <a id="configurewebconfig"></a>Modificare il File Web. config hello
Inoltre toomaking assembly fa riferimento per la Cache, il pacchetto NuGet di hello aggiunge voci stub hello *Web. config* file. 

1. Aprire hello *Web. config* e trovare hello hello **sessionState** elemento.
2. Immettere i valori hello per `host`, `accessKey`, `port` (hello porta SSL deve essere 6380) e impostare `SSL` troppo`true`. Questi valori possono essere ottenuti da hello [portale Azure](http://go.microsoft.com/fwlink/?LinkId=529715) pannello per l'istanza di cache. Per ulteriori informazioni, vedere [connessione della cache toohello](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache). Si noti che la porta non SSL di hello è disattivata per impostazione predefinita per le nuove cache. Per ulteriori informazioni sull'abilitazione della porta non SSL hello, vedere hello [porte di accesso](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) sezione hello [configurare una cache in Cache Redis di Azure](https://msdn.microsoft.com/library/azure/dn793612.aspx) argomento. Hello markup seguente viene illustrato hello modifiche toohello *Web. config* file, in modo specifico le modifiche di hello troppo*porta*, *host*, accessKey * e *ssl*.
   
          <system.web>;
            <customErrors mode="Off" />;
            <authentication mode="None" />;
            <compilation debug="true" targetFramework="4.5" />;
            <httpRuntime targetFramework="4.5" />;
            <sessionState mode="Custom" customProvider="RedisSessionProvider">;
              <providers>;  
                  <!--<add name="RedisSessionProvider" 
                    host = "127.0.0.1" [String]
                    port = "" [number]
                    accessKey = "" [String]
                    ssl = "false" [true|false]
                    throwOnError = "true" [true|false]
                    retryTimeoutInMilliseconds = "0" [number]
                    databaseId = "0" [number]
                    applicationName = "" [String]
                  />;-->;
                 <add name="RedisSessionProvider" 
                      type="Microsoft.Web.Redis.RedisSessionStateProvider" 
                      port="6380"
                      host="movie2.redis.cache.windows.net" 
                      accessKey="m7PNV60CrvKpLqMUxosC3dSe6kx9nQ6jP5del8TmADk=" 
                      ssl="true" />;
              <!--<add name="MySessionStateStore" type="Microsoft.Web.Redis.RedisSessionStateProvider" host="127.0.0.1" accessKey="" ssl="false" />;-->;
              </providers>;
            </sessionState>;
          </system.web>;

## <a id="usesessionobject"></a>Utilizzare hello oggetto di sessione nel codice
passaggio finale Hello è toobegin utilizzando l'oggetto sessione hello in codice ASP.NET. Si aggiunge lo stato di toosession oggetti utilizzando hello **Session.Add** metodo. Questo metodo Usa gli elementi di coppie chiave-valore toostore nella cache di stato sessione hello.

    string strValue = "yourvalue";
    Session.Add("yourkey", strValue);

Hello seguente codice recupera il valore dallo stato sessione.

    object objValue = Session["yourkey"];
    if (objValue != null)
       strValue = (string)objValue;    

È inoltre possibile utilizzare oggetti di toocache Cache Redis di hello nell'app web. Per altre informazioni, vedere il blog relativo all' applicazione per filmati [MVC con Cache Redis di Azure in 15 minuti](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).
Per ulteriori informazioni su come toouse lo stato della sessione ASP.NET, vedere [panoramica dello stato della sessione di ASP.NET][ASP.NET Session State Overview].

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

## <a name="whats-changed"></a>Modifiche apportate
* Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)
  
  *Autore: [Rick Anderson](https://twitter.com/RickAndMSFT)*

[installed hello latest]: http://www.windowsazure.com/downloads/?sdk=net  
[ASP.NET Session State Overview]: http://msdn.microsoft.com/library/ms178581.aspx

[NewIcon]: ./media/web-sites-dotnet-session-state-caching/CacheScreenshot_NewButton.png
[NewCacheDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CreateOptions.png
[CacheIcon]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheIcon.png
[NuGetDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_NuGet.png
[OutputConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_OC_WebConfig.png
[CacheConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheConfig.png
[EndpointURL]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_EndpointURL.png
[ManageKeys]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_ManageAccessKeys.png

