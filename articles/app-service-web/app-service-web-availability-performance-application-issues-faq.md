---
title: prestazioni aaaApplication domande frequenti per App web di Azure | Documenti Microsoft
description: "Ottenere risposte toofrequently domande frequenti su disponibilità, prestazioni e i problemi dell'applicazione hello nell'App Web della console di servizio App di Azure."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 7f2383743079e4c630fd548b0efd9993029afe11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-faqs-for-web-apps-in-azure"></a>Domande frequenti sulle prestazioni delle applicazioni in App Web di Azure

In questo articolo ha toofrequently risposte domande frequenti (FAQ) sui problemi di prestazioni dell'applicazione per hello [funzionalità App Web di Azure App Service](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-is-my-app-slow"></a>Perché l'app è lenta?

Supporto di più fattori può contribuire tooslow prestazioni dell'applicazione. Per la procedura di risoluzione dei problemi dettagliata, vedere [Risolvere i problemi di rallentamento delle prestazioni delle app Web](app-service-web-troubleshoot-performance-degradation.md).

## <a name="how-do-i-troubleshoot-a-high-cpu-consumption-scenario"></a>Come si risolvono i problemi di uno scenario con utilizzo elevato di CPU?

In alcuni scenari di utilizzo elevato di CPU, l'app può richiedere realmente più risorse di calcolo. In tal caso, prendere in considerazione scalabilità tooa maggiore livello di servizio in modo un'applicazione hello Ottiene tutte le risorse di hello che necessarie. In altri casi, un utilizzo elevato di CPU può essere causato da un ciclo non valido o da una procedura di codifica. La procedura che consente di ottenere informazioni su cosa provochi un maggiore utilizzo di CPU prevede due parti. Innanzitutto, creare un dump del processo e quindi analizzare i dump del processo hello. Per altre informazioni, vedere [Acquisire e analizzare un file di dump per l'utilizzo elevato di CPU per le app Web](https://blogs.msdn.microsoft.com/asiatech/2016/01/20/how-to-capture-dump-when-intermittent-high-cpu-happens-on-azure-web-app/).

## <a name="how-do-i-troubleshoot-a-high-memory-consumption-scenario"></a>Come si risolvono i problemi di uno scenario con utilizzo elevato di memoria?

In alcuni scenari di utilizzo elevato di memoria, l'app può richiedere realmente più risorse di calcolo. In tal caso, prendere in considerazione scalabilità tooa maggiore livello di servizio in modo un'applicazione hello Ottiene tutte le risorse di hello che necessarie. In altri casi, un bug nel codice hello potrebbe causare una perdita di memoria. Anche una procedura di codifica può provocare un maggiore utilizzo di memoria. La procedura che consente di ottenere informazioni su cosa provochi un utilizzo elevato di memoria prevede due parti. Innanzitutto, creare un dump del processo e quindi analizzare i dump del processo hello. Diagnosi di arresto anomalo del sistema dalla raccolta di estensioni del sito Azure hello è possano eseguire in modo efficiente entrambi questi passaggi. Per altre informazioni, vedere [Acquisire e analizzare un file di dump per l'utilizzo elevato intermittente di memoria per le app Web](https://blogs.msdn.microsoft.com/asiatech/2016/02/02/how-to-capture-and-analyze-dump-for-intermittent-high-memory-on-azure-web-app/).

## <a name="how-do-i-automate-app-service-web-apps-by-using-powershell"></a>Come si automatizzano le app Web del servizio app usando PowerShell?

È possibile utilizzare toomanage i cmdlet di PowerShell e gestire App del servizio web app. Nel post di blog [automatizzare le applicazioni web ospitate nel servizio App di Azure usando PowerShell](https://blogs.msdn.microsoft.com/puneetgupta/2016/03/21/automating-webapps-hosted-in-azure-app-service-through-powershell-arm-way/), viene descritto come toouse basate su Gestione risorse di Azure PowerShell cmdlet tooautomate comuni attività. post di blog Hello include anche il codice di esempio per varie attività di gestione di applicazioni web. Per le descrizioni e la sintassi di tutti i cmdlet delle app Web del servizio app, vedere [AzureRM.Websites](https://docs.microsoft.com/powershell/module/azurerm.websites/?view=azurermps-4.0.0).

## <a name="how-do-i-view-my-web-apps-event-logs"></a>Come si possono visualizzare i registri eventi dell'app Web?

tooview il registro eventi dell'applicazione web:

1. Accedi tooyour [sito Web Kudu](https://*yourwebsitename*.scm.azurewebsites.net).
2. Selezionare menu hello **Debug Console** > **CMD**.
3. Seleziona hello **LogFiles** cartella.
4. i registri eventi tooview, selezionare icona della matita hello troppo Avanti**eventlog.xml**.
5. log hello toodownload, eseguire il cmdlet PowerShell di hello `Save-AzureWebSiteLog -Name webappname`.

## <a name="how-do-i-capture-a-user-mode-memory-dump-of-my-web-app"></a>Come si acquisisce un dump della memoria in modalità utente per l'app Web?

toocapture un dump di memoria dell'app web in modalità utente:

1. Accedi tooyour [sito Web Kudu](https://*yourwebsitename*.scm.azurewebsites.net).
2. Seleziona hello **Process Explorer** menu.
3. Pulsante destro del mouse hello **w3wp.exe** processo o il processo Web.
4. Selezionare **Download Memory Dump (Scarica dump di memoria)** > **Full Dump (Dump completo)**.

## <a name="how-do-i-view-process-level-info-for-my-web-app"></a>Come si visualizzano le informazioni a livello di processo per l'app Web?

Sono disponibili due opzioni per la visualizzazione di informazioni a livello di processo per l'app Web:

*   Nel portale di Azure hello:
    1. Aprire hello **Process Explorer** per l'app web hello.
    2. Dettagli hello toosee, seleziona hello **w3wp.exe** processo.
*   Nella console di Kudu hello:
    1. Accedi tooyour [sito Web Kudu](https://*yourwebsitename*.scm.azurewebsites.net).
    2. Seleziona hello **Process Explorer** menu.
    3. Per hello **w3wp.exe** processo, selezionare **proprietà**.

## <a name="when-i-browse-toomy-app-i-see-error-403---this-web-app-is-stopped-how-do-i-resolve-this"></a>Quando si naviga toomy app, viene visualizzato "Errore 403 - questa app web è stato arrestato." Come posso risolvere il problema?

Questo errore può essere causato da tre condizioni:

* app web Hello ha raggiunto un limite di fatturazione e il sito è stato disabilitato.
* Hello web app è stato arrestato nel portale di hello.
* app web Hello ha raggiunto un limite di quota di risorse che potrebbe riguardare tooa libero o il piano di servizio condiviso scala.

toosee cause errore hello e problema hello tooresolve, hello seguire i passaggi [le applicazioni Web: "Errore 403: questa app web viene arrestato"](https://blogs.msdn.microsoft.com/waws/2016/01/05/azure-web-apps-error-403-this-web-app-is-stopped/).

## <a name="where-can-i-learn-more-about-quotas-and-limits-for-various-app-service-plans"></a>Dove si trovano altre informazioni su quote e limiti per i vari piani del servizio app?

Per informazioni su quote e limiti, vedere [Limiti relativi al servizio app](../azure-subscription-service-limits.md#app-service-limits). 

## <a name="how-do-i-decrease-hello-response-time-for-hello-first-request-after-idle-time"></a>Come ridurre i tempi di risposta hello per la prima richiesta hello dopo il tempo di inattività?

Per impostazione predefinita, le app Web vengono scaricate se restano inattive per un determinato periodo di tempo. In questo modo, il sistema hello consente di risparmiare risorse. svantaggio Hello è hello risposta toohello prima richiesta dopo aver scaricato l'app web hello è più lunga, tooallow hello tooload app web e avviare Gestione delle risposte. Nei piani di servizio Basic e Standard, è possibile attivare hello **Always On** impostazione tookeep hello app sempre caricata. In questo modo si evita tempi di caricamento dopo l'applicazione hello è inattivo. hello toochange **Always On** impostazione:

1. Nel portale di Azure hello, andare tooyour web app.
2. Selezionare **Impostazioni dell'applicazione**.
3. Per **Sempre online** selezionare **Sì**.

## <a name="how-do-i-turned-on-failed-request-tracing"></a>Come si abilita la traccia delle richieste non riuscite?

tooturn nella traccia richieste non riuscite:

1. Nel portale di Azure hello, andare tooyour web app.
3. Selezionare **Tutte le impostazioni** > **Log di diagnostica**.
4. Per **Traccia delle richieste non riuscite** selezionare **Sì**.
5. Selezionare **Salva**.
6. Nel Pannello di app web hello, selezionare **strumenti**.
7. Selezionare **Visual Studio Online**.
8. Se non è hello impostazione **su**selezionare **su**.
9. Selezionare **Vai**.
10. Selezionare **Web.config**.
11. In System. webServer, aggiungere questa configurazione (toocapture un URL specifico):

    ```
    <system.webServer>
    <tracing> <traceFailedRequests>
    <remove path="*api*" />
    <add path="*api*">
    <traceAreas>
    <add provider="ASP" verbosity="Verbose" />
    <add provider="ASPNET" areas="Infrastructure,Module,Page,AppServices" verbosity="Verbose" />
    <add provider="ISAPI Extension" verbosity="Verbose" />
    <add provider="WWW Server" areas="Authentication,Security,Filter,StaticFile,CGI,Compression, Cache,RequestNotifications,Module,FastCGI" verbosity="Verbose" />
    </traceAreas>
    <failureDefinitions statusCodes="200-999" />
    </add> </traceFailedRequests>
    </tracing>
    ```
12. problemi di prestazioni lente tootroubleshoot, aggiungere questa configurazione (se hello acquisizione richiesta richiede più di 30 secondi):
    ```
    <system.webServer>
    <tracing> <traceFailedRequests>
    <remove path="*" />
    <add path="*">
    <traceAreas> <add provider="ASP" verbosity="Verbose" />
    <add provider="ASPNET" areas="Infrastructure,Module,Page,AppServices" verbosity="Verbose" />
    <add provider="ISAPI Extension" verbosity="Verbose" />
    <add provider="WWW Server" areas="Authentication,Security,Filter,StaticFile,CGI,Compression, Cache,RequestNotifications,Module,FastCGI" verbosity="Verbose" />
    </traceAreas>
    <failureDefinitions timeTaken="00:00:30" statusCodes="200-999" />
    </add> </traceFailedRequests>
    </tracing>
    ```
13. hello toodownload non è stato possibile tracce di richieste in hello [portal](https://portal.azure.com), scegliere sito Web tooyour.
15. Select **Strumenti** > **Kudu** > **Vai**.
18. Selezionare menu hello **Debug Console** > **CMD**.
19. Seleziona hello **LogFiles** le cartelle e quindi selezionare hello con un nome che inizia con **W3SVC**.
20. file XML hello toosee, icona della matita hello selezionare.

## <a name="i-see-hello-message-worker-process-requested-recycle-due-toopercent-memory-limit-how-do-i-address-this-issue"></a>Viene visualizzato il messaggio hello "processo di lavoro richiesto riciclo scadenza too'Percent memoria ' limite." Come si risolve questo problema?

Hello disponibili quantità massima di memoria per un processo a 32 bit (anche in un sistema operativo a 64 bit) è 2 GB. Per impostazione predefinita, il processo di lavoro hello è too32 bit nel servizio App (per compatibilità con le applicazioni web legacy).

Considerare il passaggio di bit too64 processi in modo da poter sfruttare hello ulteriore memoria disponibile nel ruolo Web Worker. Questa operazione provoca il riavvio dell'app Web, quindi pianificarla di conseguenza.

Si noti anche che un ambiente a 64 bit richiede il piano di servizio Basic o Standard. I piani Gratuito e Condiviso vengono eseguiti sempre in un ambiente a 32 bit.

Per altre informazioni, vedere [Configurare le app Web nel servizio app](https://docs.microsoft.com/azure/app-service-web/web-sites-configure).

## <a name="why-does-my-request-time-out-after-240-seconds"></a>Perché la richiesta raggiunge il timeout dopo 240 secondi?

Azure Load Balancer ha un'impostazione predefinita di quattro minuti per il timeout di inattività. Si tratta in genere di un limite di tempo di risposta ragionevole per una richiesta Web. Se l'app Web richiede l'elaborazione in background, è consigliabile usare Processi Web di Azure. app web di Azure Hello può chiamare processi Web e ricevere una notifica al termine dell'elaborazione in background. È possibile scegliere tra più metodi per l'uso di Processi Web, tra cui le code e i trigger.

Processi Web è progettato per l'elaborazione in background. In un processo Web non vengono applicati limiti all'elaborazione in background. Per altre informazioni su Processi Web, vedere [Eseguire attività in background con Processi Web](https://docs.microsoft.com/azure/app-service-web/web-sites-create-web-jobs).

## <a name="aspnet-core-applications-that-are-hosted-in-app-service-sometimes-stop-responding-how-do-i-fix-this-issue"></a>A volte le applicazioni ASP.NET Core ospitate nel servizio app si bloccano. Come si risolve il problema?

Un problema noto con versione precedente [versione Kestrel](https://github.com/aspnet/KestrelHttpServer/issues/1182) potrebbe causare un'applicazione ASP.NET Core 1.0 che è ospitata nel servizio App toointermittently il blocco. È anche possibile che questo messaggio: "hello specificato applicazione CGI ha rilevato un processo di hello server terminata di errore e hello".

Il problema è stato risolto in Kestrel versione 1.0.2. Questa versione è incluso nell'aggiornamento ASP.NET Core 1.0.3 hello. tooresolve questo problema, assicurarsi di aggiornare il toouse dipendenze app Kestrel 1.0.2. In alternativa, è possibile utilizzare una delle due soluzioni alternative descritte nel post di blog hello [problemi di prestazioni lente ASP.NET Core 1.0 nelle App del servizio web app](https://blogs.msdn.microsoft.com/waws/2016/12/11/asp-net-core-slow-perf-issues-on-azure-websites).


## <a name="i-cant-find-my-log-files-in-hello-file-structure-of-my-web-app-how-can-i-find-them"></a>Impossibile trovare i file di log nella struttura di file hello dell'applicazione web. Come si possono trovare?

Se si utilizza una funzionalità della Cache locale hello del servizio App, la struttura di cartelle hello di hello LogFiles e le cartelle di dati per l'istanza di servizio App sono interessate. Quando viene utilizzata la Cache locale, le sottocartelle vengono create nell'archivio di hello LogFiles e le cartelle di dati. Utilizzare le sottocartelle Hello hello denominazione modello "identificatore" + timestamp. Ogni sottocartella corrisponde tooa istanza della macchina virtuale in cui hello app web è in esecuzione o è stata eseguita.

toodetermine se si utilizza la Cache locale, verificare il servizio App **le impostazioni dell'applicazione** scheda. Se viene utilizzata la Cache locale, hello impostazione app `WEBSITE_LOCAL_CACHE_OPTION` è troppo`Always`. Per ulteriori informazioni sulla Cache locale, vedere hello [Cenni preliminari sulla Cache locale del servizio App](https://docs.microsoft.com/azure/app-service/app-service-local-cache).

Se non si usa la cache locale e si verifica questo problema, inviare una richiesta di supporto.

## <a name="i-see-hello-message-an-attempt-was-made-tooaccess-a-socket-in-a-way-forbidden-by-its-access-permissions-how-do-i-resolve-this"></a>Viene visualizzato il messaggio hello "è stato eseguito un tentativo effettuato tooaccess un socket in modo non è consentito per le autorizzazioni di accesso." Come posso risolvere il problema?

Questo errore si verifica in genere se l'esaurimento delle connessioni TCP in uscita hello nell'istanza di macchina virtuale hello. Nel servizio App, i limiti vengono applicati per il numero massimo di hello di connessioni in uscita che possono essere eseguiti per ogni istanza di macchina virtuale. Per altre informazioni, vedere [Cross-VM numerical limits](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#cross-vm-numerical-limits) (Limiti numerici tra VM).

Questo errore può verificarsi anche se si tenta di tooaccess un indirizzo locale dall'applicazione. Per altre informazioni, vedere [Local address requests](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#local-address-requests) (Richieste di indirizzi locali).

Per ulteriori informazioni sulle connessioni in uscita in un'applicazione web, vedere hello post di blog su [in uscita di siti Web tooAzure connessioni](http://www.freekpaans.nl/2015/08/starving-outgoing-connections-on-windows-azure-web-sites/).

## <a name="how-do-i-use-visual-studio-tooremote-debug-my-app-service-web-app"></a>Come utilizzare debug di Visual Studio tooremote all'applicazione di servizio App web?

Per una procedura dettagliata che illustra come toodebug app web utilizzando Visual Studio, vedere [remoto di eseguire il debug dell'app web di servizio App](https://blogs.msdn.microsoft.com/benjaminperkins/2016/09/22/remote-debug-your-azure-app-service-web-app/).
