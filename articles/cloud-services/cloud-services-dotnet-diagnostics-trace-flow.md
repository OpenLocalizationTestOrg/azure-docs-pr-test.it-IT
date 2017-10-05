---
title: Tracciare il flusso in un'applicazione di Servizi cloud con Diagnostica di Azure | Documentazione Microsoft
description: Aggiungere messaggi di traccia a un'applicazione Azure per consentire operazioni di debug, misurazione delle prestazioni, monitoraggio, analisi del traffico e molto altro.
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
ms.openlocfilehash: 35b4a4270846c54a1ca760e803ef7adba60cf03b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="trace-the-flow-of-a-cloud-services-application-with-azure-diagnostics"></a><span data-ttu-id="b16cc-103">Tracciare il flusso in un'applicazione di Servizi cloud con Diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="b16cc-103">Trace the flow of a Cloud Services application with Azure Diagnostics</span></span>
<span data-ttu-id="b16cc-104">Tracciare è una delle azioni a cui è possibile ricorrere per monitorare l'esecuzione di un'applicazione mentre è attiva.</span><span class="sxs-lookup"><span data-stu-id="b16cc-104">Tracing is a way for you to monitor the execution of your application while it is running.</span></span> <span data-ttu-id="b16cc-105">È possibile usare le classi [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx) e [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) per registrare informazioni sull'esecuzione dell'applicazione ed eventuali errori in file di log, file di testo o altri dispositivi per un'analisi successiva.</span><span class="sxs-lookup"><span data-stu-id="b16cc-105">You can use the [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), and [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) classes to record information about errors and application execution in logs, text files, or other devices for later analysis.</span></span> <span data-ttu-id="b16cc-106">Per altre informazioni sulle funzionalità di traccia, vedere l'articolo sulle modalità per [tracciare e instrumentare applicazioni](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span><span class="sxs-lookup"><span data-stu-id="b16cc-106">For more information about tracing, see [Tracing and Instrumenting Applications](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span></span>

## <a name="use-trace-statements-and-trace-switches"></a><span data-ttu-id="b16cc-107">Usare istruzioni e opzioni di traccia</span><span class="sxs-lookup"><span data-stu-id="b16cc-107">Use trace statements and trace switches</span></span>
<span data-ttu-id="b16cc-108">Per implementare funzionalità di traccia in un'applicazione di Servizi cloud, è possibile aggiungere [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) alla configurazione dell'applicazione ed effettuare chiamate a System.Diagnostics.Trace o System.Diagnostics.Debug nel codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b16cc-108">Implement tracing in your Cloud Services application by adding the [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) to the application configuration and making calls to System.Diagnostics.Trace or System.Diagnostics.Debug in your application code.</span></span> <span data-ttu-id="b16cc-109">Usare il file di configurazione *app.config* per i ruoli di lavoro e *web.config* per i ruoli Web.</span><span class="sxs-lookup"><span data-stu-id="b16cc-109">Use the configuration file *app.config* for worker roles and the *web.config* for web roles.</span></span> <span data-ttu-id="b16cc-110">Quando si crea un nuovo servizio ospitato usando un modello di Visual Studio, Diagnostica di Azure viene automaticamente aggiunto al progetto e DiagnosticMonitorTraceListener viene aggiunto al file di configurazione appropriato per i ruoli aggiunti.</span><span class="sxs-lookup"><span data-stu-id="b16cc-110">When you create a new hosted service using a Visual Studio template, Azure Diagnostics is automatically added to the project and the DiagnosticMonitorTraceListener is added to the appropriate configuration file for the roles that you add.</span></span>

<span data-ttu-id="b16cc-111">Per informazioni sull'inserimento di istruzioni di traccia, vedere la [procedura per aggiungere istruzioni di traccia al codice di un'applicazione](https://msdn.microsoft.com/library/zd83saa2.aspx).</span><span class="sxs-lookup"><span data-stu-id="b16cc-111">For information on placing trace statements, see [How to: Add Trace Statements to Application Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>

<span data-ttu-id="b16cc-112">Inserendo [opzioni di traccia](https://msdn.microsoft.com/library/3at424ac.aspx) nel codice, è possibile controllare se la traccia viene eseguita e con quale copertura.</span><span class="sxs-lookup"><span data-stu-id="b16cc-112">By placing [Trace Switches](https://msdn.microsoft.com/library/3at424ac.aspx) in your code, you can control whether tracing occurs and how extensive it is.</span></span> <span data-ttu-id="b16cc-113">In questo modo, è possibile monitorare lo stato dell'applicazione in un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="b16cc-113">This lets you monitor the status of your application in a production environment.</span></span> <span data-ttu-id="b16cc-114">Questo aspetto è particolarmente importante in un'applicazione aziendale che usa più componenti in esecuzione su più computer.</span><span class="sxs-lookup"><span data-stu-id="b16cc-114">This is especially important in a business application that uses multiple components running on multiple computers.</span></span> <span data-ttu-id="b16cc-115">Per altre informazioni, vedere la [procedura per configurare opzioni di traccia](https://msdn.microsoft.com/library/t06xyy08.aspx).</span><span class="sxs-lookup"><span data-stu-id="b16cc-115">For more information, see [How to: Configure Trace Switches](https://msdn.microsoft.com/library/t06xyy08.aspx).</span></span>

## <a name="configure-the-trace-listener-in-an-azure-application"></a><span data-ttu-id="b16cc-116">Configurare il listener di traccia in un'applicazione Azure</span><span class="sxs-lookup"><span data-stu-id="b16cc-116">Configure the trace listener in an Azure application</span></span>
<span data-ttu-id="b16cc-117">Quando si usano le classi Traccia, Debug e TraceSource, è necessario impostare dei "listener" per raccogliere e registrare i messaggi inviati.</span><span class="sxs-lookup"><span data-stu-id="b16cc-117">Trace, Debug and TraceSource, require you set up "listeners" to collect and record the messages that are sent.</span></span> <span data-ttu-id="b16cc-118">I listener raccolgono, archiviano e indirizzano i messaggi di traccia,</span><span class="sxs-lookup"><span data-stu-id="b16cc-118">Listeners collect, store, and route tracing messages.</span></span> <span data-ttu-id="b16cc-119">quindi indirizzano l'output di traccia su una destinazione appropriata, ad esempio un log, una finestra o un file di testo.</span><span class="sxs-lookup"><span data-stu-id="b16cc-119">They direct the tracing output to an appropriate target, such as a log, window, or text file.</span></span> <span data-ttu-id="b16cc-120">Diagnostica di Azure usa la classe [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx).</span><span class="sxs-lookup"><span data-stu-id="b16cc-120">Azure Diagnostics uses the [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) class.</span></span>

<span data-ttu-id="b16cc-121">Prima di completare la procedura seguente, è necessario inizializzare il monitor di diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="b16cc-121">Before you complete the following procedure, you must initialize the Azure diagnostic monitor.</span></span> <span data-ttu-id="b16cc-122">A tale scopo, vedere [Abilitazione di Diagnostica in Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="b16cc-122">To do this, see [Enabling Diagnostics in Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="b16cc-123">Se si usano i modelli disponibili in Visual Studio, la configurazione del listener viene aggiunta automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b16cc-123">Note that if you use the templates that are provided by Visual Studio, the configuration of the listener is added automatically for you.</span></span>

### <a name="add-a-trace-listener"></a><span data-ttu-id="b16cc-124">Aggiungere un listener di traccia</span><span class="sxs-lookup"><span data-stu-id="b16cc-124">Add a trace listener</span></span>
1. <span data-ttu-id="b16cc-125">Aprire il file web.config o app.config, in base al ruolo selezionato.</span><span class="sxs-lookup"><span data-stu-id="b16cc-125">Open the web.config or app.config file for your role.</span></span>
2. <span data-ttu-id="b16cc-126">Aggiungere il codice seguente al file.</span><span class="sxs-lookup"><span data-stu-id="b16cc-126">Add the following code to the file.</span></span> <span data-ttu-id="b16cc-127">Modificare l'attributo Version impostando il numero di versione dell'assembly a cui si fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="b16cc-127">Change the Version attribute to use the version number of the assembly you are referencing.</span></span> <span data-ttu-id="b16cc-128">La versione dell'assembly non cambia necessariamente con ogni versione di Azure SDK a meno che non vengano resi disponibili aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="b16cc-128">The assembly version does not necessarily change with each Azure SDK release unless there are updates to it.</span></span>
   
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
   > <span data-ttu-id="b16cc-129">Accertarsi di avere un riferimento progetto all'assembly Microsoft.WindowsAzure.Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="b16cc-129">Make sure you have a project reference to the Microsoft.WindowsAzure.Diagnostics assembly.</span></span> <span data-ttu-id="b16cc-130">Aggiornare il numero di versione nel file xml precedente in base alla versione dell'assembly di riferimento Microsoft.WindowsAzure.Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="b16cc-130">Update the version number in the xml above to match the version of the referenced Microsoft.WindowsAzure.Diagnostics assembly.</span></span>
   > 
   > 
3. <span data-ttu-id="b16cc-131">Salvare il file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="b16cc-131">Save the config file.</span></span>

<span data-ttu-id="b16cc-132">Per altre informazioni sui listener, vedere l'articolo sui [listener di traccia](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span><span class="sxs-lookup"><span data-stu-id="b16cc-132">For more information about listeners, see [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span></span>

<span data-ttu-id="b16cc-133">Dopo aver completato i passaggi necessari per aggiungere il listener, è possibile aggiungere istruzioni di traccia al codice.</span><span class="sxs-lookup"><span data-stu-id="b16cc-133">After you complete the steps to add the listener, you can add trace statements to your code.</span></span>

### <a name="to-add-trace-statement-to-your-code"></a><span data-ttu-id="b16cc-134">Per aggiungere un'istruzione di traccia al codice</span><span class="sxs-lookup"><span data-stu-id="b16cc-134">To add trace statement to your code</span></span>
1. <span data-ttu-id="b16cc-135">Aprire un file di origine per l'applicazione,</span><span class="sxs-lookup"><span data-stu-id="b16cc-135">Open a source file for your application.</span></span> <span data-ttu-id="b16cc-136">ad esempio il file <RoleName>.cs per il ruolo di lavoro o il ruolo Web.</span><span class="sxs-lookup"><span data-stu-id="b16cc-136">For example, the <RoleName>.cs file for the worker role or web role.</span></span>
2. <span data-ttu-id="b16cc-137">Aggiungere l'istruzione using seguente, se non è già presente:</span><span class="sxs-lookup"><span data-stu-id="b16cc-137">Add the following using statement if it has not already been added:</span></span>
    ```
        using System.Diagnostics;
    ```
3. <span data-ttu-id="b16cc-138">Aggiungere istruzioni di traccia nei punti in cui si desidera acquisire informazioni sullo stato dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b16cc-138">Add Trace statements where you want to capture information about the state of your application.</span></span> <span data-ttu-id="b16cc-139">È possibile usare vari metodi per formattare l'output dell'istruzione di traccia.</span><span class="sxs-lookup"><span data-stu-id="b16cc-139">You can use a variety of methods to format the output of the Trace statement.</span></span> <span data-ttu-id="b16cc-140">Per altre informazioni, vedere la [procedura per aggiungere istruzioni di traccia al codice dell'applicazione](https://msdn.microsoft.com/library/zd83saa2.aspx).</span><span class="sxs-lookup"><span data-stu-id="b16cc-140">For more information, see [How to: Add Trace Statements to Application Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>
4. <span data-ttu-id="b16cc-141">Salvare il file di origine.</span><span class="sxs-lookup"><span data-stu-id="b16cc-141">Save the source file.</span></span>

