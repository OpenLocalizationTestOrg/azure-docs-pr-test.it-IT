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
# <a name="streaming-logs-and-hello-console"></a><span data-ttu-id="885a5-103">I log di streaming e hello Console</span><span class="sxs-lookup"><span data-stu-id="885a5-103">Streaming Logs and hello Console</span></span>
## <a name="streaming-logs"></a><span data-ttu-id="885a5-104">Log in streaming</span><span class="sxs-lookup"><span data-stu-id="885a5-104">Streaming Logs</span></span>
<span data-ttu-id="885a5-105">Hello **portale di Azure** fornisce un visualizzatore log di streaming integrato che consente di visualizzare gli eventi di traccia dal **servizio App** App in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="885a5-105">hello **Azure portal** provides an integrated streaming log viewer that lets you view tracing events from your **App Service** apps in real time.</span></span>  

<span data-ttu-id="885a5-106">L'impostazione di questa funzionalità richiede alcuni semplici passaggi:</span><span class="sxs-lookup"><span data-stu-id="885a5-106">Setting up this feature requires a few simple steps:</span></span>

* <span data-ttu-id="885a5-107">Scrittura delle tracce nel codice</span><span class="sxs-lookup"><span data-stu-id="885a5-107">Write traces in your code</span></span>
* <span data-ttu-id="885a5-108">Abilitazione dei **log di diagnostica** dell'applicazione per l'app</span><span class="sxs-lookup"><span data-stu-id="885a5-108">Enable Application **Diagnostic Logs** for your app</span></span>
* <span data-ttu-id="885a5-109">Flusso di hello vista da incorporato hello **i log di Streaming** dell'interfaccia utente in hello **portale di Azure**.</span><span class="sxs-lookup"><span data-stu-id="885a5-109">View hello stream from hello built-in **Streaming Logs** UI in hello **Azure portal**.</span></span>

### <a name="how-toowrite-traces-in-your-code"></a><span data-ttu-id="885a5-110">Come toowrite tracce nel codice</span><span class="sxs-lookup"><span data-stu-id="885a5-110">How toowrite traces in your code</span></span>
<span data-ttu-id="885a5-111">La scrittura delle tracce nel codice è facile.</span><span class="sxs-lookup"><span data-stu-id="885a5-111">Writing traces in your code is easy.</span></span>  <span data-ttu-id="885a5-112">In c# è semplice come la scrittura di hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="885a5-112">In C# it's as easy as writing hello following code:</span></span>

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

<span data-ttu-id="885a5-113">classe Trace Hello si trova nello spazio dei nomi System. Diagnostics hello.</span><span class="sxs-lookup"><span data-stu-id="885a5-113">hello Trace class lives in hello System.Diagnostics namespace.</span></span>

<span data-ttu-id="885a5-114">In un'app node.js è possibile scrivere questo codice tooachieve hello stesso risultato:</span><span class="sxs-lookup"><span data-stu-id="885a5-114">In a node.js app you can write this code tooachieve hello same result:</span></span>

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-tooenable-and-view-hello-streaming-logs"></a><span data-ttu-id="885a5-115">Come tooenable e visualizzazione hello i log di streaming</span><span class="sxs-lookup"><span data-stu-id="885a5-115">How tooenable and view hello streaming logs</span></span>
<span data-ttu-id="885a5-116">![][BrowseSitesScreenshot] La diagnostica viene abilitata a livello di singola app.</span><span class="sxs-lookup"><span data-stu-id="885a5-116">![][BrowseSitesScreenshot] Diagnostics are enabled on a per app basis.</span></span> <span data-ttu-id="885a5-117">Prima di tutto esplorare toohello sito tooenable questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="885a5-117">Start by browsing toohello site you would like tooenable this feature on.</span></span>  

<span data-ttu-id="885a5-118">![][DiagnosticsLogs]Dal menu impostazioni, scorrere verso il basso toohello **monitoraggio** sezione e fare clic su **(1) i log di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="885a5-118">![][DiagnosticsLogs] From settings menu, scroll down toohello **Monitoring** section and click on **(1) Diagnostic Logs**.</span></span> <span data-ttu-id="885a5-119">Quindi **(2) abilita** **registrazione delle applicazioni (file System)** o **(blob) registrazione delle applicazioni** hello **livello** opzione consente di modificare hello livello di gravità di toocapture tracce.</span><span class="sxs-lookup"><span data-stu-id="885a5-119">Then **(2) enable** **Application Logging (Filesystem)** or **Application Logging (blob)** hello **Level** option lets you change hello severity level of traces toocapture.</span></span> <span data-ttu-id="885a5-120">Se si cerca solo tooget familiarità con la funzione hello, impostare il livello di hello troppo**Verbose** tooensure tutte le istruzioni di traccia vengono raccolte.</span><span class="sxs-lookup"><span data-stu-id="885a5-120">If you're just trying tooget familiar with hello feature, set hello level too**Verbose** tooensure all of your trace statements are collected.</span></span>

<span data-ttu-id="885a5-121">Fare clic su **salvare** nella parte superiore di hello di blade hello e si è pronti tooview log.</span><span class="sxs-lookup"><span data-stu-id="885a5-121">Click **SAVE** at hello top of hello blade and you're ready tooview logs.</span></span>

> [!NOTE]
> <span data-ttu-id="885a5-122">hello superiore Hello **livello di gravità** hello ulteriori risorse sono toolog utilizzato e hello generate altre tracce.</span><span class="sxs-lookup"><span data-stu-id="885a5-122">hello higher hello **severity level** hello more resources are consumed toolog and hello more traces are produced.</span></span> <span data-ttu-id="885a5-123">Assicurarsi che **livello di gravità** è configurato toohello corretto livello di dettaglio per una produzione o siti a traffico elevato.</span><span class="sxs-lookup"><span data-stu-id="885a5-123">Make sure **severity level** is configured toohello correct verbosity for a production or high traffic site.</span></span> 
> 
> 

<span data-ttu-id="885a5-124">![][StreamingLogsScreenshot]hello tooview **i log di streaming** all'interno di hello portale di Azure, fare clic sul **flusso del Log (1)** anche in hello **monitoraggio** sezione del menu Impostazioni hello.</span><span class="sxs-lookup"><span data-stu-id="885a5-124">![][StreamingLogsScreenshot] tooview hello **streaming logs** from within hello Azure portal, click on **(1) Log Stream** also in hello **Monitoring** section of hello settings menu.</span></span> <span data-ttu-id="885a5-125">Se l'app è attiva la scrittura di istruzioni di traccia, dovresti vederli hello **streaming (2) registra l'interfaccia utente** quasi in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="885a5-125">If your app is actively writing trace statements, then you should see them in hello **(2) streaming logs UI** in near real time.</span></span>

## <a name="console"></a><span data-ttu-id="885a5-126">Console</span><span class="sxs-lookup"><span data-stu-id="885a5-126">Console</span></span>
<span data-ttu-id="885a5-127">Hello **portale di Azure** fornisce console accesso tooyour app.</span><span class="sxs-lookup"><span data-stu-id="885a5-127">hello **Azure portal** provides console access tooyour app.</span></span> <span data-ttu-id="885a5-128">È possibile esplorare il file system dell'app ed eseguire script Powershell/cmd.</span><span class="sxs-lookup"><span data-stu-id="885a5-128">You can explore your app's file system and run powershell/cmd scripts.</span></span> <span data-ttu-id="885a5-129">Sono legati da hello delle stesse autorizzazioni impostate come codice dell'app in esecuzione durante l'esecuzione di comandi della console.</span><span class="sxs-lookup"><span data-stu-id="885a5-129">You are bound by hello same permissions set as your running app code when executing console commands.</span></span> <span data-ttu-id="885a5-130">Esecuzione di script che richiedono autorizzazioni elevate o di directory tooprotected di accesso è bloccato.</span><span class="sxs-lookup"><span data-stu-id="885a5-130">Access tooprotected directories or running scripts that require elevated permissions is blocked.</span></span>  

<span data-ttu-id="885a5-131">![][ConsoleScreenshot]Dal menu impostazioni, scorrere verso il basso troppo**gli strumenti di sviluppo** sezione e fare clic su **(1) Console** hello e **(2) console** dell'interfaccia utente apre toohello destra.</span><span class="sxs-lookup"><span data-stu-id="885a5-131">![][ConsoleScreenshot] From settings menu, scroll down too**Development Tools** section and click on **(1) Console** and hello **(2) console** UI opens toohello right.</span></span>

<span data-ttu-id="885a5-132">familiarità con hello tooget **console**, provare i comandi di base come:</span><span class="sxs-lookup"><span data-stu-id="885a5-132">tooget familiar with hello **console**, try basic commands like:</span></span>

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
