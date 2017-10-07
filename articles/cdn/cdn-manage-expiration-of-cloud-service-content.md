---
title: aaaManage scadenza del contenuto web nella rete CDN di Azure | Documenti Microsoft
description: Informazioni su come toomanage scadenza del contenuto di Azure Web App o servizi basati su Cloud, ASP.NET o IIS nella rete CDN di Azure.
services: cdn
documentationcenter: .NET
author: zhangmanling
manager: erikre
editor: 
ms.assetid: bef53fcc-bb13-4002-9324-9edee9da8288
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: a0154236c3893b627f4480e0688f555964862556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-expiration-of-azure-web-appscloud-services-aspnet-or-iis-content-in-azure-cdn"></a>Gestire la scadenza del contenuto di app Web o servizi cloud di Azure, ASP.NET o IIS nella rete CDN di Azure
> [!div class="op_single_selector"]
> * [App Web/Servizi cloud di Azure, ASP.NET o IIS](cdn-manage-expiration-of-cloud-service-content.md)
> * [Servizio BLOB del servizio di archiviazione di Azure](cdn-manage-expiration-of-blob-content.md)
> 
> 

I file provenienti da un server Web di origine accessibile pubblicamente possono essere memorizzati nella cache della rete CDN di Azure fino allo scadere della relativa durata (TTL).  Hello durata (TTL) è determinato dal hello [ *Cache-Control* intestazione](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in risposta hello HTTP dal server di origine hello.  Questo articolo viene descritto come tooset `Cache-Control` intestazioni per le app Web di Azure, servizi Cloud di Azure, le applicazioni e siti di Internet Information Services, che sono configurati in modo analogo.

> [!TIP]
> È non possibile scegliere tooset alcuna durata (TTL) su un file.  In tal caso, la rete CDN di Azure applica automaticamente una durata (TTL) predefinita di sette giorni.
> 
> Per ulteriori informazioni sul funzionamento toospeed toofiles di accesso e altre risorse di rete CDN di Azure, vedere hello [Panoramica della rete CDN di Azure](cdn-overview.md).
> 
> 

## <a name="setting-cache-control-headers-in-configuration"></a>Impostazione delle intestazioni Cache-Control nella configurazione
Per il contenuto statico, ad esempio immagini e fogli di stile, è possibile controllare la frequenza di aggiornamento hello modificando hello **applicationHost. config** o **Web. config** file per l'applicazione web.  Hello **system.webServer\staticContent\clientCache** elemento nel file di configurazione hello imposterà hello `Cache-Control` intestazione per il contenuto. Per **Web. config**, hello configurazione impostazioni avranno effetto su tutti gli elementi nella cartella di hello e tutte le sottocartelle, a meno che non viene sottoposto a override a livello di hello sottocartella.  Ad esempio, è possibile impostare un valore predefinito time-to-live in hello radice toohave tutto il contenuto statico memorizzato nella cache per 3 giorni, ma è presente una sottocartella con più variabile contenuto con le impostazioni della cache di 6 ore.  Per **applicationHost. config**, tutte le applicazioni hello sito verranno modificate, ma può essere sottoposto a override in **Web. config** file hello applicazioni.

Hello codice XML seguente viene illustrato un esempio dell'impostazione **clientCache** toospecify una durata massima di 3 giorni:  

```xml
<configuration>
    <system.webServer>
        <staticContent>
            <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00" />
        </staticContent>
    </system.webServer>
</configuration>
```

Specifica di **UseMaxAge** aggiunge un `Cache-Control: max-age=<nnn>` risposta toohello intestazione in base al valore di hello specificato in hello **CacheControlMaxAge** attributo. formato Hello di timespan hello è per hello **cacheControlMaxAge** attributo <days>.<hours>:<min>:<sec>. Per ulteriori informazioni su hello **clientCache** nodo, vedere [nella Cache del Client <clientCache> ](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).  

## <a name="setting-cache-control-headers-in-code"></a>Impostazione delle intestazioni Cache-Control nel codice
Per le applicazioni ASP.NET, è possibile impostare il comportamento della cache di hello CDN a livello di programmazione dall'impostazione hello **HttpResponse** proprietà. Per ulteriori informazioni su hello **HttpResponse** proprietà, vedere [proprietà HttpResponse cache](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) e [classe HttpCachePolicy](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).  

Se si desidera il contenuto dell'applicazione di cache tooprogrammatically in ASP.NET, assicurarsi che il contenuto di hello viene contrassegnato come inseribile nella cache impostando HttpCacheability troppo*pubblica*. Assicurarsi anche che sia impostato un validator della cache. validator della cache di Hello può essere una data ultima modifica timestamp impostato chiamando SetLastModified o un valore etag impostato chiamando SetETag. Facoltativamente, è anche possibile specificare una data di scadenza della cache chiamando SetExpires oppure affidarsi euristica hello predefinita della cache descritta in precedenza in questo documento.  

Ad esempio, toocache contenuto per un'ora, aggiungere il seguente hello:  

```csharp
// Set hello caching parameters.
Response.Cache.SetExpires(DateTime.Now.AddHours(1));
Response.Cache.SetCacheability(HttpCacheability.Public);
Response.Cache.SetLastModified(DateTime.Now);
```

## <a name="next-steps"></a>Passaggi successivi
* [Dettagli sugli hello **clientCache** elemento](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)
* [Leggere la documentazione di hello per hello **HttpResponse** proprietà](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 
* [Leggere la documentazione di hello per hello **classe HttpCachePolicy**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).  

