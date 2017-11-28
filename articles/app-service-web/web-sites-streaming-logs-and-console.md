---
title: Log di streaming e console
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
ms.openlocfilehash: 120ce6b115820728b9f853e9ff349beb0ef29c9d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="streaming-logs-and-the-console"></a><span data-ttu-id="a5392-103">Log di streaming e console</span><span class="sxs-lookup"><span data-stu-id="a5392-103">Streaming Logs and the Console</span></span>
## <a name="streaming-logs"></a><span data-ttu-id="a5392-104">Log in streaming</span><span class="sxs-lookup"><span data-stu-id="a5392-104">Streaming Logs</span></span>
<span data-ttu-id="a5392-105">Il **portale di Azure** offre un visualizzatore log di streaming integrato che consente di visualizzare gli eventi di traccia dalle app del **servizio app** in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="a5392-105">The **Azure portal** provides an integrated streaming log viewer that lets you view tracing events from your **App Service** apps in real time.</span></span>  

<span data-ttu-id="a5392-106">L'impostazione di questa funzionalità richiede alcuni semplici passaggi:</span><span class="sxs-lookup"><span data-stu-id="a5392-106">Setting up this feature requires a few simple steps:</span></span>

* <span data-ttu-id="a5392-107">Scrittura delle tracce nel codice</span><span class="sxs-lookup"><span data-stu-id="a5392-107">Write traces in your code</span></span>
* <span data-ttu-id="a5392-108">Abilitazione dei **log di diagnostica** dell'applicazione per l'app</span><span class="sxs-lookup"><span data-stu-id="a5392-108">Enable Application **Diagnostic Logs** for your app</span></span>
* <span data-ttu-id="a5392-109">Visualizzare il flusso dall'interfaccia utente dei **log in streaming** predefiniti nel **portale Azure**.</span><span class="sxs-lookup"><span data-stu-id="a5392-109">View the stream from the built-in **Streaming Logs** UI in the **Azure portal**.</span></span>

### <a name="how-to-write-traces-in-your-code"></a><span data-ttu-id="a5392-110">Come scrivere le tracce nel codice</span><span class="sxs-lookup"><span data-stu-id="a5392-110">How to write traces in your code</span></span>
<span data-ttu-id="a5392-111">La scrittura delle tracce nel codice è facile.</span><span class="sxs-lookup"><span data-stu-id="a5392-111">Writing traces in your code is easy.</span></span>  <span data-ttu-id="a5392-112">In C# è sufficiente scrivere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="a5392-112">In C# it's as easy as writing the following code:</span></span>

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

<span data-ttu-id="a5392-113">La classe Trace risiede nello spazio dei nomi System.Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="a5392-113">The Trace class lives in the System.Diagnostics namespace.</span></span>

<span data-ttu-id="a5392-114">In una app node.js è possibile scrivere il codice seguente per ottenere lo stesso risultato:</span><span class="sxs-lookup"><span data-stu-id="a5392-114">In a node.js app you can write this code to achieve the same result:</span></span>

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-to-enable-and-view-the-streaming-logs"></a><span data-ttu-id="a5392-115">Come abilitare e visualizzare i log in streaming</span><span class="sxs-lookup"><span data-stu-id="a5392-115">How to enable and view the streaming logs</span></span>
<span data-ttu-id="a5392-116">![][BrowseSitesScreenshot] La diagnostica viene abilitata a livello di singola app.</span><span class="sxs-lookup"><span data-stu-id="a5392-116">![][BrowseSitesScreenshot] Diagnostics are enabled on a per app basis.</span></span> <span data-ttu-id="a5392-117">Eseguire l'avvio passando al sito per cui si vuole abilitare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a5392-117">Start by browsing to the site you would like to enable this feature on.</span></span>  

<span data-ttu-id="a5392-118">![][DiagnosticsLogs] Dal menu Impostazioni eseguire lo scorrimento verso il basso fino alla sezione di **monitoraggio** e fare clic su **(1) Log di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="a5392-118">![][DiagnosticsLogs] From settings menu, scroll down to the **Monitoring** section and click on **(1) Diagnostic Logs**.</span></span> <span data-ttu-id="a5392-119">Quindi **(2) abilitare** **Registrazione applicazioni (file system)** o **Registrazione applicazioni (BLOB)**. L'opzione **Livello** consente di modificare il livello di gravità delle tracce da acquisire.</span><span class="sxs-lookup"><span data-stu-id="a5392-119">Then **(2) enable** **Application Logging (Filesystem)** or **Application Logging (blob)** The **Level** option lets you change the severity level of traces to capture.</span></span> <span data-ttu-id="a5392-120">Impostare il livello su **Dettagliato** se si sta solo acquisendo familiarità con la funzionalità, poiché questa impostazione garantirà la registrazione di tutte le istruzioni di traccia.</span><span class="sxs-lookup"><span data-stu-id="a5392-120">If you're just trying to get familiar with the feature, set the level to **Verbose** to ensure all of your trace statements are collected.</span></span>

<span data-ttu-id="a5392-121">Fare clic su **SAVE** nella parte superiore del blade per visualizzare i log.</span><span class="sxs-lookup"><span data-stu-id="a5392-121">Click **SAVE** at the top of the blade and you're ready to view logs.</span></span>

> [!NOTE]
> <span data-ttu-id="a5392-122">Più è alto il **livello di gravità**, più risorse si consumano per eseguire il log e più tracce si ottengono.</span><span class="sxs-lookup"><span data-stu-id="a5392-122">The higher the **severity level** the more resources are consumed to log and the more traces are produced.</span></span> <span data-ttu-id="a5392-123">Assicurarsi che **livello di gravità** sia configurato per il livello di dettaglio corretto per un sito a traffico elevato o di produzione.</span><span class="sxs-lookup"><span data-stu-id="a5392-123">Make sure **severity level** is configured to the correct verbosity for a production or high traffic site.</span></span> 
> 
> 

<span data-ttu-id="a5392-124">![][StreamingLogsScreenshot] Per visualizzare i **log in streaming** dall'interno del portale di Azure fare clic su **(1) Flusso di registrazione** anche nella sezione di **monitoraggio** del menu Impostazioni.</span><span class="sxs-lookup"><span data-stu-id="a5392-124">![][StreamingLogsScreenshot] To view the **streaming logs** from within the Azure portal, click on **(1) Log Stream** also in the **Monitoring** section of the settings menu.</span></span> <span data-ttu-id="a5392-125">Se l'app sta scrivendo attivamente istruzioni di traccia, saranno visibili nella **(2) interfaccia utente dei log in streaming** in tempo quasi reale.</span><span class="sxs-lookup"><span data-stu-id="a5392-125">If your app is actively writing trace statements, then you should see them in the **(2) streaming logs UI** in near real time.</span></span>

## <a name="console"></a><span data-ttu-id="a5392-126">Console</span><span class="sxs-lookup"><span data-stu-id="a5392-126">Console</span></span>
<span data-ttu-id="a5392-127">Il **portale di Azure** fornisce accesso all'app mediante console.</span><span class="sxs-lookup"><span data-stu-id="a5392-127">The **Azure portal** provides console access to your app.</span></span> <span data-ttu-id="a5392-128">È possibile esplorare il file system dell'app ed eseguire script Powershell/cmd.</span><span class="sxs-lookup"><span data-stu-id="a5392-128">You can explore your app's file system and run powershell/cmd scripts.</span></span> <span data-ttu-id="a5392-129">Quando si eseguono i comandi della console, si opera con le stesse autorizzazioni impostate per il codice dell'app in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a5392-129">You are bound by the same permissions set as your running app code when executing console commands.</span></span> <span data-ttu-id="a5392-130">L'accesso alle directory protette o l'esecuzione di script che richiedono autorizzazioni elevate è bloccato.</span><span class="sxs-lookup"><span data-stu-id="a5392-130">Access to protected directories or running scripts that require elevated permissions is blocked.</span></span>  

<span data-ttu-id="a5392-131">![][ConsoleScreenshot] Dal menu Impostazioni scorrere verso il basso fino alla sezione **Strumenti di sviluppo** e fare clic su **(1) Console**; a destra viene aperta l'interfaccia utente della **(2) console**.</span><span class="sxs-lookup"><span data-stu-id="a5392-131">![][ConsoleScreenshot] From settings menu, scroll down to **Development Tools** section and click on **(1) Console** and the **(2) console** UI opens to the right.</span></span>

<span data-ttu-id="a5392-132">Per acquisire familiarità con la **console**, provare ad eseguire i comandi di base come:</span><span class="sxs-lookup"><span data-stu-id="a5392-132">To get familiar with the **console**, try basic commands like:</span></span>

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
