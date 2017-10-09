---
title: i log aaaStreaming e console
description: Informazioni su console e log in streaming
author: btardif
manager: erikre
editor: 
services: app-service\web
documentationcenter: 
ms.assetid: 3e50a287-781b-4c6a-8c53-eec261889d7a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/12/2016
ms.author: byvinyal
ms.openlocfilehash: bb4b8ce5358da12041e164dfff8f43790dd67924
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-logs-and-hello-console"></a>I log di streaming e hello Console
## <a name="streaming-logs"></a>Log in streaming
Hello **portale di Azure** fornisce un visualizzatore log di streaming integrato che consente di visualizzare gli eventi di traccia dal **servizio App** App in tempo reale.  

L'impostazione di questa funzionalità richiede alcuni semplici passaggi:

* Scrittura delle tracce nel codice
* Abilitazione dei **log di diagnostica** dell'applicazione per l'app
* Flusso di hello vista da incorporato hello **i log di Streaming** dell'interfaccia utente in hello **portale di Azure**.

### <a name="how-toowrite-traces-in-your-code"></a>Come toowrite tracce nel codice
La scrittura delle tracce nel codice è facile.  In c# è semplice come la scrittura di hello seguente codice:

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

classe Trace Hello si trova nello spazio dei nomi System. Diagnostics hello.

In un'app node.js è possibile scrivere questo codice tooachieve hello stesso risultato:

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-tooenable-and-view-hello-streaming-logs"></a>Come tooenable e visualizzazione hello i log di streaming
![][BrowseSitesScreenshot] La diagnostica viene abilitata a livello di singola app. Prima di tutto esplorare toohello sito tooenable questa funzionalità.  

![][DiagnosticsLogs]Dal menu impostazioni, scorrere verso il basso toohello **monitoraggio** sezione e fare clic su **(1) i log di diagnostica**. Quindi **(2) abilita** **registrazione delle applicazioni (file System)** o **(blob) registrazione delle applicazioni** hello **livello** opzione consente di modificare hello livello di gravità di toocapture tracce. Se si cerca solo tooget familiarità con la funzione hello, impostare il livello di hello troppo**Verbose** tooensure tutte le istruzioni di traccia vengono raccolte.

Fare clic su **salvare** nella parte superiore di hello di blade hello e si è pronti tooview log.

> [!NOTE]
> hello superiore Hello **livello di gravità** hello ulteriori risorse sono toolog utilizzato e hello generate altre tracce. Assicurarsi che **livello di gravità** è configurato toohello corretto livello di dettaglio per una produzione o siti a traffico elevato. 
> 
> 

![][StreamingLogsScreenshot]hello tooview **i log di streaming** all'interno di hello portale di Azure, fare clic sul **flusso del Log (1)** anche in hello **monitoraggio** sezione del menu Impostazioni hello. Se l'app è attiva la scrittura di istruzioni di traccia, dovresti vederli hello **streaming (2) registra l'interfaccia utente** quasi in tempo reale.

## <a name="console"></a>Console
Hello **portale di Azure** fornisce console accesso tooyour app. È possibile esplorare il file system dell'app ed eseguire script Powershell/cmd. Sono legati da hello delle stesse autorizzazioni impostate come codice dell'app in esecuzione durante l'esecuzione di comandi della console. Esecuzione di script che richiedono autorizzazioni elevate o di directory tooprotected di accesso è bloccato.  

![][ConsoleScreenshot]Dal menu impostazioni, scorrere verso il basso troppo**gli strumenti di sviluppo** sezione e fare clic su **(1) Console** hello e **(2) console** dell'interfaccia utente apre toohello destra.

familiarità con hello tooget **console**, provare i comandi di base come:

`````````````````````````
dir
`````````````````````````

`````````````````````````
cd
`````````````````````````

<!-- Images. -->
[DiagnosticsLogs]: ./media/web-sites-streaming-logs-and-console/diagnostic-logs.png
[BrowseSitesScreenshot]: ./media/web-sites-streaming-logs-and-console/browse-sites.png
[StreamingLogsScreenshot]: ./media/web-sites-streaming-logs-and-console/streaming-logs.png
[ConsoleScreenshot]: ./media/web-sites-streaming-logs-and-console/console.png
