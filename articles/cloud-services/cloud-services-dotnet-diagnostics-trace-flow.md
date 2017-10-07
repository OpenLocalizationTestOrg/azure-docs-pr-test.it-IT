---
title: flusso di hello aaaTrace in un'applicazione di servizi Cloud con diagnostica di Azure | Documenti Microsoft
description: Aggiungere il debug di traccia messaggi tooan applicazione Azure toohelp, misurazione delle prestazioni, monitoraggio, analisi del traffico e altro ancora.
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 09934772-cc07-4fd2-ba88-b224ca192f8e
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/20/2016
ms.author: robb
ms.openlocfilehash: d2ed7b5997ae1d298115b4ce593bb5051a9a0c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="trace-hello-flow-of-a-cloud-services-application-with-azure-diagnostics"></a><span data-ttu-id="74831-103">Flusso di hello traccia di un'applicazione di servizi Cloud con diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="74831-103">Trace hello flow of a Cloud Services application with Azure Diagnostics</span></span>
<span data-ttu-id="74831-104">La traccia è un modo per si toomonitor hello esecuzione dell'applicazione mentre è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="74831-104">Tracing is a way for you toomonitor hello execution of your application while it is running.</span></span> <span data-ttu-id="74831-105">È possibile utilizzare hello [Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), e [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) classi toorecord informazioni sugli errori e esecuzione dell'applicazione in log, file di testo o altri dispositivi per l'analisi successiva.</span><span class="sxs-lookup"><span data-stu-id="74831-105">You can use hello [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), and [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) classes toorecord information about errors and application execution in logs, text files, or other devices for later analysis.</span></span> <span data-ttu-id="74831-106">Per altre informazioni sulle funzionalità di traccia, vedere l'articolo sulle modalità per [tracciare e instrumentare applicazioni](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span><span class="sxs-lookup"><span data-stu-id="74831-106">For more information about tracing, see [Tracing and Instrumenting Applications](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span></span>

## <a name="use-trace-statements-and-trace-switches"></a><span data-ttu-id="74831-107">Usare istruzioni e opzioni di traccia</span><span class="sxs-lookup"><span data-stu-id="74831-107">Use trace statements and trace switches</span></span>
<span data-ttu-id="74831-108">Traccia di implementare nell'applicazione di servizi Cloud mediante l'aggiunta di hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) toohello configurazione dell'applicazione e rendendo chiama tooSystem.Diagnostics.Trace o debug nel codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="74831-108">Implement tracing in your Cloud Services application by adding hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) toohello application configuration and making calls tooSystem.Diagnostics.Trace or System.Diagnostics.Debug in your application code.</span></span> <span data-ttu-id="74831-109">Utilizza il file di configurazione hello *app* per i ruoli di lavoro e hello *Web. config* per i ruoli web.</span><span class="sxs-lookup"><span data-stu-id="74831-109">Use hello configuration file *app.config* for worker roles and hello *web.config* for web roles.</span></span> <span data-ttu-id="74831-110">Quando si crea un nuovo servizio ospitato con un modello di Visual Studio, diagnostica Azure viene aggiunto automaticamente il progetto toohello e hello DiagnosticMonitorTraceListener viene aggiunto il file di configurazione appropriato toohello per ruoli hello da aggiungere.</span><span class="sxs-lookup"><span data-stu-id="74831-110">When you create a new hosted service using a Visual Studio template, Azure Diagnostics is automatically added toohello project and hello DiagnosticMonitorTraceListener is added toohello appropriate configuration file for hello roles that you add.</span></span>

<span data-ttu-id="74831-111">Per informazioni sull'inserimento delle istruzioni di traccia, vedere [procedura: aggiungere istruzioni di traccia tooApplication codice](https://msdn.microsoft.com/library/zd83saa2.aspx).</span><span class="sxs-lookup"><span data-stu-id="74831-111">For information on placing trace statements, see [How to: Add Trace Statements tooApplication Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>

<span data-ttu-id="74831-112">Inserendo [opzioni di traccia](https://msdn.microsoft.com/library/3at424ac.aspx) nel codice, è possibile controllare se la traccia viene eseguita e con quale copertura.</span><span class="sxs-lookup"><span data-stu-id="74831-112">By placing [Trace Switches](https://msdn.microsoft.com/library/3at424ac.aspx) in your code, you can control whether tracing occurs and how extensive it is.</span></span> <span data-ttu-id="74831-113">Ciò consente di monitorare lo stato di hello dell'applicazione in un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="74831-113">This lets you monitor hello status of your application in a production environment.</span></span> <span data-ttu-id="74831-114">Questo aspetto è particolarmente importante in un'applicazione aziendale che usa più componenti in esecuzione su più computer.</span><span class="sxs-lookup"><span data-stu-id="74831-114">This is especially important in a business application that uses multiple components running on multiple computers.</span></span> <span data-ttu-id="74831-115">Per altre informazioni, vedere la [procedura per configurare opzioni di traccia](https://msdn.microsoft.com/library/t06xyy08.aspx).</span><span class="sxs-lookup"><span data-stu-id="74831-115">For more information, see [How to: Configure Trace Switches](https://msdn.microsoft.com/library/t06xyy08.aspx).</span></span>

## <a name="configure-hello-trace-listener-in-an-azure-application"></a><span data-ttu-id="74831-116">Configurare il listener di traccia di hello in un'applicazione Azure</span><span class="sxs-lookup"><span data-stu-id="74831-116">Configure hello trace listener in an Azure application</span></span>
<span data-ttu-id="74831-117">Traccia, Debug e TraceSource, è necessario impostare "listener" toocollect e messaggi hello record che vengono inviati.</span><span class="sxs-lookup"><span data-stu-id="74831-117">Trace, Debug and TraceSource, require you set up "listeners" toocollect and record hello messages that are sent.</span></span> <span data-ttu-id="74831-118">I listener raccolgono, archiviano e indirizzano i messaggi di traccia,</span><span class="sxs-lookup"><span data-stu-id="74831-118">Listeners collect, store, and route tracing messages.</span></span> <span data-ttu-id="74831-119">Indicano hello traccia output tooan destinazione appropriata, ad esempio un log, una finestra o un file di testo.</span><span class="sxs-lookup"><span data-stu-id="74831-119">They direct hello tracing output tooan appropriate target, such as a log, window, or text file.</span></span> <span data-ttu-id="74831-120">Diagnostica di Azure Usa hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) classe.</span><span class="sxs-lookup"><span data-stu-id="74831-120">Azure Diagnostics uses hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) class.</span></span>

<span data-ttu-id="74831-121">Prima di completare la seguente procedura hello, è necessario inizializzare hello monitoraggio diagnostica Azure.</span><span class="sxs-lookup"><span data-stu-id="74831-121">Before you complete hello following procedure, you must initialize hello Azure diagnostic monitor.</span></span> <span data-ttu-id="74831-122">toodo questa operazione, vedere [abilitazione di diagnostica Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="74831-122">toodo this, see [Enabling Diagnostics in Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="74831-123">Si noti che se si utilizzano i modelli di hello forniti da Visual Studio, hello configurazione del listener hello viene aggiunta automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="74831-123">Note that if you use hello templates that are provided by Visual Studio, hello configuration of hello listener is added automatically for you.</span></span>

### <a name="add-a-trace-listener"></a><span data-ttu-id="74831-124">Aggiungere un listener di traccia</span><span class="sxs-lookup"><span data-stu-id="74831-124">Add a trace listener</span></span>
1. <span data-ttu-id="74831-125">Aprire il file Web. config o App. config di hello per il ruolo.</span><span class="sxs-lookup"><span data-stu-id="74831-125">Open hello web.config or app.config file for your role.</span></span>
2. <span data-ttu-id="74831-126">Aggiungere i seguenti file di codice toohello hello.</span><span class="sxs-lookup"><span data-stu-id="74831-126">Add hello following code toohello file.</span></span> <span data-ttu-id="74831-127">Modificare hello versione attributo toouse hello numero di versione dell'assembly hello che viene fatto riferimento.</span><span class="sxs-lookup"><span data-stu-id="74831-127">Change hello Version attribute toouse hello version number of hello assembly you are referencing.</span></span> <span data-ttu-id="74831-128">versione dell'assembly Hello non necessariamente modificato con ogni versione di Azure SDK a meno che non sono presenti aggiornamenti tooit.</span><span class="sxs-lookup"><span data-stu-id="74831-128">hello assembly version does not necessarily change with each Azure SDK release unless there are updates tooit.</span></span>
   
    ```
    <system.diagnostics>
        <trace>
            <listeners>
                <add type="Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener,
                  Microsoft.WindowsAzure.Diagnostics,
                  Version=2.8.0.0,
                  Culture=neutral,
                  PublicKeyToken=31bf3856ad364e35"
                  name="AzureDiagnostics">
                    <filter type="" />
                </add>
            </listeners>
        </trace>
    </system.diagnostics>
    ```
   > [!IMPORTANT]
   > <span data-ttu-id="74831-129">Assicurarsi di avere un toohello di riferimento di progetto Microsoft.WindowsAzure.Diagnostics assembly.</span><span class="sxs-lookup"><span data-stu-id="74831-129">Make sure you have a project reference toohello Microsoft.WindowsAzure.Diagnostics assembly.</span></span> <span data-ttu-id="74831-130">Numero di versione di aggiornamento hello in xml hello precedente versione di hello toomatch di hello riferimento Microsoft.WindowsAzure.Diagnostics assembly.</span><span class="sxs-lookup"><span data-stu-id="74831-130">Update hello version number in hello xml above toomatch hello version of hello referenced Microsoft.WindowsAzure.Diagnostics assembly.</span></span>
   > 
   > 
3. <span data-ttu-id="74831-131">Salvare il file di configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="74831-131">Save hello config file.</span></span>

<span data-ttu-id="74831-132">Per altre informazioni sui listener, vedere l'articolo sui [listener di traccia](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span><span class="sxs-lookup"><span data-stu-id="74831-132">For more information about listeners, see [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span></span>

<span data-ttu-id="74831-133">Dopo aver completato i listener di hello passaggi tooadd hello, è possibile aggiungere codice tooyour istruzioni di traccia.</span><span class="sxs-lookup"><span data-stu-id="74831-133">After you complete hello steps tooadd hello listener, you can add trace statements tooyour code.</span></span>

### <a name="tooadd-trace-statement-tooyour-code"></a><span data-ttu-id="74831-134">codice di tooyour tooadd traccia istruzione</span><span class="sxs-lookup"><span data-stu-id="74831-134">tooadd trace statement tooyour code</span></span>
1. <span data-ttu-id="74831-135">Aprire un file di origine per l'applicazione,</span><span class="sxs-lookup"><span data-stu-id="74831-135">Open a source file for your application.</span></span> <span data-ttu-id="74831-136">Ad esempio, hello <RoleName>file con estensione cs per il ruolo di lavoro hello o web.</span><span class="sxs-lookup"><span data-stu-id="74831-136">For example, hello <RoleName>.cs file for hello worker role or web role.</span></span>
2. <span data-ttu-id="74831-137">Aggiungere il seguente hello utilizzando l'istruzione se non è già stata aggiunta:</span><span class="sxs-lookup"><span data-stu-id="74831-137">Add hello following using statement if it has not already been added:</span></span>
    ```
        using System.Diagnostics;
    ```
3. <span data-ttu-id="74831-138">Aggiungere istruzioni di traccia in cui si desiderano toocapture informazioni sullo stato di hello dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="74831-138">Add Trace statements where you want toocapture information about hello state of your application.</span></span> <span data-ttu-id="74831-139">È possibile utilizzare un'ampia gamma di output di hello tooformat metodi di hello istruzione di traccia.</span><span class="sxs-lookup"><span data-stu-id="74831-139">You can use a variety of methods tooformat hello output of hello Trace statement.</span></span> <span data-ttu-id="74831-140">Per ulteriori informazioni, vedere [procedura: aggiungere istruzioni di traccia tooApplication codice](https://msdn.microsoft.com/library/zd83saa2.aspx).</span><span class="sxs-lookup"><span data-stu-id="74831-140">For more information, see [How to: Add Trace Statements tooApplication Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>
4. <span data-ttu-id="74831-141">Salvare il file di origine hello.</span><span class="sxs-lookup"><span data-stu-id="74831-141">Save hello source file.</span></span>

