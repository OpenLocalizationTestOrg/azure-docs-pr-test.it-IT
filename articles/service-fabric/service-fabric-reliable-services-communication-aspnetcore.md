---
title: Comunicazione dei servizi con ASP.NET Core | Microsoft Docs
description: Informazioni su come usare ASP.NET Core in Reliable Services con e senza stato.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 8aa4668d-cbb6-4225-bd2d-ab5925a868f2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 05/02/2017
ms.author: vturecek
ms.openlocfilehash: 8ac4d409f7363e8b4ae98be659a627ac8db8d787
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="aspnet-core-in-service-fabric-reliable-services"></a><span data-ttu-id="7e153-103">ASP.NET Core in Reliable Services di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7e153-103">ASP.NET Core in Service Fabric Reliable Services</span></span>

<span data-ttu-id="7e153-104">ASP.NET Core è un nuovo framework open source e multipiattaforma per la compilazione di applicazioni Internet moderne basate sul cloud, ad esempio app Web, app per IoT e back-end per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="7e153-104">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based Internet-connected applications, such as web apps, IoT apps, and mobile backends.</span></span> 

<span data-ttu-id="7e153-105">Questo articolo è una guida dettagliata per l'hosting dei servizi ASP.NET Core in Reliable Services di Service Fabric mediante il set di pacchetti NuGet **Microsoft.ServiceFabric.AspNetCore.***.</span><span class="sxs-lookup"><span data-stu-id="7e153-105">This article is an in-depth guide to hosting ASP.NET Core services in Service Fabric Reliable Services using the **Microsoft.ServiceFabric.AspNetCore.*** set of NuGet packages.</span></span>

<span data-ttu-id="7e153-106">Per un'esercitazione introduttiva su ASP.NET Core in Service Fabric e istruzioni per la configurazione dell'ambiente di sviluppo, vedere [Compilare un front-end di servizio Web per l'applicazione tramite ASP.NET Core](service-fabric-add-a-web-frontend.md).</span><span class="sxs-lookup"><span data-stu-id="7e153-106">For an introductory tutorial on ASP.NET Core in Service Fabric and instructions on getting your development environment set up, see [Building a web front-end for your application using ASP.NET Core](service-fabric-add-a-web-frontend.md).</span></span>

<span data-ttu-id="7e153-107">La parte restante di questo articolo presuppone che si conosca il funzionamento di ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="7e153-107">The rest of this article assumes you are already familiar with ASP.NET Core.</span></span> <span data-ttu-id="7e153-108">In caso contrario è consigliabile vedere [ASP.NET Core fundamentals overview](https://docs.microsoft.com/aspnet/core/fundamentals/index) (Panoramica sulle nozioni fondamentali di ASP.NET Core).</span><span class="sxs-lookup"><span data-stu-id="7e153-108">If not, we recommend reading through the [ASP.NET Core fundamentals](https://docs.microsoft.com/aspnet/core/fundamentals/index).</span></span>

## <a name="aspnet-core-in-the-service-fabric-environment"></a><span data-ttu-id="7e153-109">ASP.NET Core nell'ambiente Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7e153-109">ASP.NET Core in the Service Fabric environment</span></span>

<span data-ttu-id="7e153-110">Anche se le app ASP.NET Core possono essere eseguite in .NET o nella versione completa di .NET Framework, i servizi di Service Fabric possono essere attualmente eseguiti solo nella versione completa di .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="7e153-110">While ASP.NET Core apps can run on .NET Core or on the full .NET Framework, Service Fabric services currently can only run on the full .NET Framework.</span></span> <span data-ttu-id="7e153-111">Ciò significa che quando si compila un servizio di Service Fabric in ASP.NET Core è comunque necessario usare la versione completa di .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="7e153-111">This means when you build an ASP.NET  Core Service Fabric service, you must still target the full .NET Framework.</span></span>

<span data-ttu-id="7e153-112">ASP.NET Core può essere usato in due modi diversi in Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="7e153-112">ASP.NET Core can be used in two different ways in Service Fabric:</span></span>
 - <span data-ttu-id="7e153-113">**Ospitato come eseguibile guest**.</span><span class="sxs-lookup"><span data-stu-id="7e153-113">**Hosted as a guest executable**.</span></span> <span data-ttu-id="7e153-114">Questa modalità viene usata principalmente per eseguire applicazioni ASP.NET Core esistenti in Service Fabric senza apportare modifiche al codice.</span><span class="sxs-lookup"><span data-stu-id="7e153-114">This is primarily used to run existing ASP.NET Core applications on Service Fabric with no code changes.</span></span>
 - <span data-ttu-id="7e153-115">**Eseguito in un servizio Reliable Services**.</span><span class="sxs-lookup"><span data-stu-id="7e153-115">**Run inside a Reliable Service**.</span></span> <span data-ttu-id="7e153-116">Questa modalità offre una migliore integrazione con il runtime di Service Fabric e consente servizi ASP.NET Core con stato.</span><span class="sxs-lookup"><span data-stu-id="7e153-116">This allows better integration with the Service Fabric runtime and allows stateful ASP.NET Core services.</span></span>

<span data-ttu-id="7e153-117">Il resto di questo articolo illustra come usare ASP.NET Core in un servizio Reliable Services usando i componenti di integrazione ASP.NET Core forniti con Service Fabric SDK.</span><span class="sxs-lookup"><span data-stu-id="7e153-117">The rest of this article explains how to use ASP.NET Core inside a Reliable Service using the ASP.NET Core integration components that ship with the Service Fabric SDK.</span></span> 

## <a name="service-fabric-service-hosting"></a><span data-ttu-id="7e153-118">Hosting di servizi di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7e153-118">Service Fabric service hosting</span></span>

<span data-ttu-id="7e153-119">In Service Fabric, una o più istanze e/o repliche del servizio vengono eseguite in un *processo host del servizio*, un file eseguibile che esegue il codice del servizio.</span><span class="sxs-lookup"><span data-stu-id="7e153-119">In Service Fabric, one or more instances and/or replicas of your service run in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="7e153-120">L'autore del servizio è il proprietario del processo host del servizio, che verrà attivato e monitorato automaticamente da Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7e153-120">You, as a service author, own the service host process and Service Fabric activates and monitors it for you.</span></span>

<span data-ttu-id="7e153-121">La versione tradizionale di ASP.NET, fino a MVC 5, è strettamente associata a IIS tramite System.Web.dll.</span><span class="sxs-lookup"><span data-stu-id="7e153-121">Traditional ASP.NET (up to MVC 5) is tightly coupled to IIS through System.Web.dll.</span></span> <span data-ttu-id="7e153-122">ASP.NET Core fornisce una separazione tra il server Web e l'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="7e153-122">ASP.NET Core provides a separation between the web server and your web application.</span></span> <span data-ttu-id="7e153-123">Ciò consente la portabilità delle applicazioni Web tra server Web diversi e il *self-hosting* dei server Web, vale a dire che è possibile avviare un server Web nel proprio processo, invece di un processo gestito da software del server Web dedicato, ad esempio IIS.</span><span class="sxs-lookup"><span data-stu-id="7e153-123">This allows web applications to be portable between different web servers and also allows web servers to be *self-hosted*, which means you can start a web server in your own process, as opposed to a process that is owned by dedicated web server software such as IIS.</span></span> 

<span data-ttu-id="7e153-124">Per combinare un servizio di Service Fabric e ASP.NET, come eseguibile guest o servizio Reliable Services, è necessario poter avviare ASP.NET all'interno del processo host del servizio.</span><span class="sxs-lookup"><span data-stu-id="7e153-124">In order to combine a Service Fabric service and ASP.NET, either as a guest executable or in a Reliable Service, you must be able to start ASP.NET inside your service host process.</span></span> <span data-ttu-id="7e153-125">Il self-hosting di ASP.NET Core consente di eseguire questa operazione.</span><span class="sxs-lookup"><span data-stu-id="7e153-125">ASP.NET Core self-hosting allows you to do this.</span></span>

## <a name="hosting-aspnet-core-in-a-reliable-service"></a><span data-ttu-id="7e153-126">Hosting di ASP.NET Core in un servizio Reliable Services</span><span class="sxs-lookup"><span data-stu-id="7e153-126">Hosting ASP.NET Core in a Reliable Service</span></span>
<span data-ttu-id="7e153-127">Le applicazioni ASP.NET Core con self-hosting creano in genere un WebHost in un punto di ingresso dell'applicazione, ad esempio il metodo `static void Main()` in `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="7e153-127">Typically, self-hosted ASP.NET Core applications create a WebHost in an application's entry point, such as the `static void Main()` method in `Program.cs`.</span></span> <span data-ttu-id="7e153-128">In questo caso, il ciclo di vita del WebHost è associato al ciclo di vita del processo.</span><span class="sxs-lookup"><span data-stu-id="7e153-128">In this case, the lifecycle of the WebHost is bound to the lifecycle of the process.</span></span>

![Hosting di ASP.NET Core in un processo][0]

<span data-ttu-id="7e153-130">Il punto di ingresso dell'applicazione non è tuttavia la posizione corretta per creare un WebHost in un servizio Reliable Services, perché il punto di ingresso dell'applicazione viene usato solo per registrare un tipo di servizio con il runtime di Service Fabric per poter creare istanze di quel tipo di servizio.</span><span class="sxs-lookup"><span data-stu-id="7e153-130">However, the application entry point is not the right place to create a WebHost in a Reliable Service, because the application entry point is only used to register a service type with the Service Fabric runtime, so that it may create instances of that service type.</span></span> <span data-ttu-id="7e153-131">Il WebHost deve essere creato in un servizio Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="7e153-131">The WebHost should be created in a Reliable Service itself.</span></span> <span data-ttu-id="7e153-132">Nel processo host del servizio, le istanze e/o le repliche del servizio possono attraversare più cicli di vita.</span><span class="sxs-lookup"><span data-stu-id="7e153-132">Within the service host process, service instances and/or replicas can go through multiple lifecycles.</span></span> 

<span data-ttu-id="7e153-133">Un'istanza di Reliable Services è rappresentata dalla classe del servizio derivante da `StatelessService` o `StatefulService`.</span><span class="sxs-lookup"><span data-stu-id="7e153-133">A Reliable Service instance is represented by your service class deriving from `StatelessService` or `StatefulService`.</span></span> <span data-ttu-id="7e153-134">Lo stack di comunicazione di un servizio è contenuto in un'implementazione `ICommunicationListener` nella classe del servizio.</span><span class="sxs-lookup"><span data-stu-id="7e153-134">The communication stack for a service is contained in an `ICommunicationListener` implementation in your service class.</span></span> <span data-ttu-id="7e153-135">I pacchetti NuGet `Microsoft.ServiceFabric.Services.AspNetCore.*` contengono implementazioni di `ICommunicationListener` che avviano e gestiscono WebHost ASP.NET Core per Kestrel o WebListener in un servizio Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="7e153-135">The `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages contain implementations of `ICommunicationListener` that start and manage the ASP.NET Core WebHost for either Kestrel or WebListener in a Reliable Service.</span></span>

![Hosting di ASP.NET Core in un servizio Reliable Services][1]

## <a name="aspnet-core-icommunicationlisteners"></a><span data-ttu-id="7e153-137">ICommunicationListeners ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="7e153-137">ASP.NET Core ICommunicationListeners</span></span>
<span data-ttu-id="7e153-138">Le implementazioni di `ICommunicationListener` per Kestrel e WebListener nei pacchetti NuGet `Microsoft.ServiceFabric.Services.AspNetCore.*` hanno modelli di uso simili, ma eseguono azioni leggermente specifiche per ogni server Web.</span><span class="sxs-lookup"><span data-stu-id="7e153-138">The `ICommunicationListener` implementations for Kestrel and WebListener in the  `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages have similar use patterns but perform slightly different actions specific to each web server.</span></span> 

<span data-ttu-id="7e153-139">Entrambi i listener di comunicazione forniscono un costruttore che accetta gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="7e153-139">Both communication listeners provide a constructor that takes the following arguments:</span></span>
 - <span data-ttu-id="7e153-140">**`ServiceContext serviceContext`**: oggetto `ServiceContext` che contiene informazioni sul servizio in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="7e153-140">**`ServiceContext serviceContext`**: The `ServiceContext` object that contains information about the running service.</span></span>
 - <span data-ttu-id="7e153-141">**`string endpointName`**: nome di una configurazione `Endpoint` in ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="7e153-141">**`string endpointName`**: the name of an `Endpoint` configuration in ServiceManifest.xml.</span></span> <span data-ttu-id="7e153-142">È principalmente qui che i due listener di comunicazione differiscono: WebListener **richiede** una configurazione `Endpoint` che non è invece necessaria per Kestrel.</span><span class="sxs-lookup"><span data-stu-id="7e153-142">This is primarily where the two communication listeners differ: WebListener **requires** an `Endpoint` configuration, while Kestrel does not.</span></span>
 - <span data-ttu-id="7e153-143">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: espressione lambda implementata in cui viene creato e restituito un elemento `IWebHost`.</span><span class="sxs-lookup"><span data-stu-id="7e153-143">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: a lambda that you implement in which you create and return an `IWebHost`.</span></span> <span data-ttu-id="7e153-144">È così possibile configurare `IWebHost` come si farebbe normalmente in un'applicazione ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="7e153-144">This allows you to configure `IWebHost` the way you normally would in an ASP.NET Core application.</span></span> <span data-ttu-id="7e153-145">L'espressione lambda fornisce un URL che viene generato automaticamente a seconda delle opzioni di integrazione di Service Fabric usate e della configurazione `Endpoint` specificata.</span><span class="sxs-lookup"><span data-stu-id="7e153-145">The lambda provides a URL which is generated for you depending on the Service Fabric integration options you use and the `Endpoint` configuration you provide.</span></span> <span data-ttu-id="7e153-146">L'URL può quindi essere modificato o usato così com'è per avviare il server Web.</span><span class="sxs-lookup"><span data-stu-id="7e153-146">That URL can then be modified or used as-is to start the web server.</span></span>

## <a name="service-fabric-integration-middleware"></a><span data-ttu-id="7e153-147">Middleware di integrazione di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7e153-147">Service Fabric integration middleware</span></span>
<span data-ttu-id="7e153-148">Il pacchetto NuGet `Microsoft.ServiceFabric.Services.AspNetCore` include il metodo di estensione `UseServiceFabricIntegration` in `IWebHostBuilder` che aggiunge middleware compatibile con Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7e153-148">The `Microsoft.ServiceFabric.Services.AspNetCore` NuGet package includes the `UseServiceFabricIntegration` extension method on `IWebHostBuilder` that adds Service Fabric-aware middleware.</span></span> <span data-ttu-id="7e153-149">Questo middleware configura l'elemento `ICommunicationListener` di Kestrel o WebListener per la registrazione di un URL di servizio univoco con Service Fabric Naming Service e quindi convalida le richieste dei client per assicurare che i client si connettano al servizio corretto.</span><span class="sxs-lookup"><span data-stu-id="7e153-149">This middleware configures the Kestrel or WebListener `ICommunicationListener` to register a unique service URL with the Service Fabric Naming Service and then validates client requests to ensure clients are connecting to the right service.</span></span> <span data-ttu-id="7e153-150">Ciò è necessario in un ambiente host condiviso, ad esempio Service Fabric, in cui più applicazioni Web possono essere eseguite nello stesso computer fisico o nella stessa macchina virtuale ma non usano nomi host univoci, per impedire ai client di connettersi erroneamente al servizio sbagliato.</span><span class="sxs-lookup"><span data-stu-id="7e153-150">This is necessary in a shared-host environment such as Service Fabric, where multiple web applications can run on the same physical or virtual machine but do not use unique host names, to prevent clients from mistakenly connecting to the wrong service.</span></span> <span data-ttu-id="7e153-151">Questo scenario è descritto più dettagliatamente nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="7e153-151">This scenario is described in more detail in the next section.</span></span>

### <a name="a-case-of-mistaken-identity"></a><span data-ttu-id="7e153-152">Un caso di identità errata</span><span class="sxs-lookup"><span data-stu-id="7e153-152">A case of mistaken identity</span></span>
<span data-ttu-id="7e153-153">Le repliche del servizio, indipendentemente dal protocollo, sono in ascolto in una combinazione IP:porta univoca.</span><span class="sxs-lookup"><span data-stu-id="7e153-153">Service replicas, regardless of protocol, listen on a unique IP:port combination.</span></span> <span data-ttu-id="7e153-154">Quando è in ascolto su un endpoint IP:porta, la replica del servizio segnala l'indirizzo dell'endpoint a Service Fabric Naming Service, dove può essere individuato dai client o da altri servizi.</span><span class="sxs-lookup"><span data-stu-id="7e153-154">Once a service replica has started listening on an IP:port endpoint, it reports that endpoint address to the Service Fabric Naming Service where it can be discovered by clients or other services.</span></span> <span data-ttu-id="7e153-155">Se i servizi usano porte delle applicazioni assegnate dinamicamente, una replica del servizio può usare per coincidenza lo stesso endpoint IP:porta di un altro servizio che si trovava precedentemente nello stesso computer fisico o nella stessa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7e153-155">If services use dynamically-assigned application ports, a service replica may coincidentally use the same IP:port endpoint of another service that was previously on the same physical or virtual machine.</span></span> <span data-ttu-id="7e153-156">In questo modo un client può connettersi per errore al servizio sbagliato.</span><span class="sxs-lookup"><span data-stu-id="7e153-156">This can cause a client to mistakely connect to the wrong service.</span></span> <span data-ttu-id="7e153-157">Questa situazione può verificarsi in presenza di questa sequenza di eventi:</span><span class="sxs-lookup"><span data-stu-id="7e153-157">This can happen if the following sequence of events occur:</span></span>

 1. <span data-ttu-id="7e153-158">Il servizio A è in ascolto in 10.0.0.1:30000 su HTTP.</span><span class="sxs-lookup"><span data-stu-id="7e153-158">Service A listens on 10.0.0.1:30000 over HTTP.</span></span> 
 2. <span data-ttu-id="7e153-159">Il client risolve il servizio A e ottiene l'indirizzo 10.0.0.1:30000</span><span class="sxs-lookup"><span data-stu-id="7e153-159">Client resolves Service A and gets address 10.0.0.1:30000</span></span>
 3. <span data-ttu-id="7e153-160">Il servizio A si sposta in un nodo diverso.</span><span class="sxs-lookup"><span data-stu-id="7e153-160">Service A moves to a different node.</span></span>
 4. <span data-ttu-id="7e153-161">Il servizio B si trova in 10.0.0.1 e usa per coincidenza la stessa porta 30000.</span><span class="sxs-lookup"><span data-stu-id="7e153-161">Service B is placed on 10.0.0.1 and coincidentally uses the same port 30000.</span></span>
 5. <span data-ttu-id="7e153-162">Il client prova a connettersi al servizio A con l'indirizzo 10.0.0.1:30000 memorizzato nella cache.</span><span class="sxs-lookup"><span data-stu-id="7e153-162">Client attempts to connect to service A with cached address 10.0.0.1:30000.</span></span>
 6. <span data-ttu-id="7e153-163">Il client è ora connesso al servizio B e non rileva di essersi connesso al servizio sbagliato.</span><span class="sxs-lookup"><span data-stu-id="7e153-163">Client is now successfully connected to service B not realizing it is connected to the wrong service.</span></span>

<span data-ttu-id="7e153-164">Ciò può causare bug in momenti casuali che possono essere difficili da diagnosticare.</span><span class="sxs-lookup"><span data-stu-id="7e153-164">This can cause bugs at random times that can be difficult to diagnose.</span></span> 

### <a name="using-unique-service-urls"></a><span data-ttu-id="7e153-165">Uso di URL di servizio univoci</span><span class="sxs-lookup"><span data-stu-id="7e153-165">Using unique service URLs</span></span>
<span data-ttu-id="7e153-166">Per evitare questo problema, i servizi possono inviare un endpoint al servizio Naming con un identificatore univoco e quindi convalidare tale identificatore univoco durante le richieste client.</span><span class="sxs-lookup"><span data-stu-id="7e153-166">To prevent this, services can post an endpoint to the Naming Service with a unique identifier, and then validate that unique identifier during client requests.</span></span> <span data-ttu-id="7e153-167">Si tratta di un'azione cooperativa tra servizi in un ambiente attendibile di tenant non ostili.</span><span class="sxs-lookup"><span data-stu-id="7e153-167">This is a cooperative action between services in a non-hostile-tenant trusted environment.</span></span> <span data-ttu-id="7e153-168">Non offre l'autenticazione sicura dei servizi in un ambiente di tenant ostili.</span><span class="sxs-lookup"><span data-stu-id="7e153-168">This does not provide secure service authentication in a hostile-tenant environment.</span></span>

<span data-ttu-id="7e153-169">In un ambiente attendibile, il middleware aggiunto dal metodo `UseServiceFabricIntegration` accoda automaticamente un identificatore univoco all'indirizzo inviato al servizio Naming e convalida l'identificatore a ogni richiesta.</span><span class="sxs-lookup"><span data-stu-id="7e153-169">In a trusted environment, the middleware that's added by the `UseServiceFabricIntegration` method automatically appends a unique identifier to the address that is posted to the Naming Service and validates that identifier on each request.</span></span> <span data-ttu-id="7e153-170">Se l'identificatore non corrisponde, il middleware restituisce immediatamente una risposta HTTP 410 - Non più disponibile.</span><span class="sxs-lookup"><span data-stu-id="7e153-170">If the identifier does not match, the middleware immediately returns an HTTP 410 Gone response.</span></span>

<span data-ttu-id="7e153-171">I servizi che usano una porta assegnata dinamicamente devono usare questo middleware.</span><span class="sxs-lookup"><span data-stu-id="7e153-171">Services that use a dynamically-assigned port should make use of this middleware.</span></span>

<span data-ttu-id="7e153-172">I servizi che usano una porta fissa univoca non hanno questo problema in un ambiente collaborativo.</span><span class="sxs-lookup"><span data-stu-id="7e153-172">Services that use a fixed unique port do not have this problem in a cooperative environment.</span></span> <span data-ttu-id="7e153-173">Una porta fissa univoca viene in genere usata per i servizi esterni che richiedono una porta nota per la connessione delle applicazioni client.</span><span class="sxs-lookup"><span data-stu-id="7e153-173">A fixed unique port is typically used for externally-facing services that need a well-known port for client applications to connect to.</span></span> <span data-ttu-id="7e153-174">La maggior parte delle applicazioni Web per Internet, ad esempio, usa la porta 80 o 443 per connessioni tramite Web browser.</span><span class="sxs-lookup"><span data-stu-id="7e153-174">For example, most Internet-facing web applications will use port 80 or 443 for web browser connections.</span></span> <span data-ttu-id="7e153-175">In questo caso, l'identificatore univoco non deve essere abilitato.</span><span class="sxs-lookup"><span data-stu-id="7e153-175">In this case, the unique identifier should not be enabled.</span></span>

<span data-ttu-id="7e153-176">Il diagramma seguente illustra il flusso della richiesta con il middleware abilitato:</span><span class="sxs-lookup"><span data-stu-id="7e153-176">The following diagram shows the request flow with the middleware enabled:</span></span>

![Integrazione ASP.NET Core di Service Fabric][2]

<span data-ttu-id="7e153-178">Le implementazioni di `ICommunicationListener` di Kestrel e WebListener usano questo meccanismo nello stesso identico modo.</span><span class="sxs-lookup"><span data-stu-id="7e153-178">Both Kestrel and WebListener `ICommunicationListener` implementations use this mechanism in exactly the same way.</span></span> <span data-ttu-id="7e153-179">Anche se WebListener può differenziare internamente le richieste in base a percorsi URL univoci usando la funzionalità di condivisione delle porte *http.sys* sottostante, questa funzionalità *non* viene usata dall'implementazione `ICommunicationListener` di WebListener perché provocherebbe i codici di stato di errore HTTP 503 e HTTP 404 nello scenario descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="7e153-179">Although WebListener can internally differentiate requests based on unique URL paths using the underlying *http.sys* port sharing feature, that functionality is *not* used by the WebListener `ICommunicationListener` implementation because that will result in HTTP 503 and HTTP 404 error status codes in the scenario described earlier.</span></span> <span data-ttu-id="7e153-180">Ciò rende a sua volta molto difficile per i client determinare la finalità dell'errore, perché i codici HTTP 503 e HTTP 404 sono già comunemente usati per indicare altri errori.</span><span class="sxs-lookup"><span data-stu-id="7e153-180">That in turn makes it very difficult for clients to determine the intent of the error, as HTTP 503 and HTTP 404 are already commonly used to indicate other errors.</span></span> <span data-ttu-id="7e153-181">Le implementazioni di `ICommunicationListener` di Kestrel e WebListener vengono quindi standardizzate con il middleware fornito dal metodo di estensione `UseServiceFabricIntegration`, in modo che i client debbano solo eseguire nuovamente la risoluzione dell'endpoint del servizio nelle risposte HTTP 410.</span><span class="sxs-lookup"><span data-stu-id="7e153-181">Thus, both Kestrel and WebListener `ICommunicationListener` implementations standardize on the middleware provided by the `UseServiceFabricIntegration` extension method so that clients only need to perform a service endpoint re-resolve action on HTTP 410 responses.</span></span>

## <a name="weblistener-in-reliable-services"></a><span data-ttu-id="7e153-182">WebListener in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="7e153-182">WebListener in Reliable Services</span></span>
<span data-ttu-id="7e153-183">WebListener può essere usato in un servizio Reliable Services importando il pacchetto NuGet **Microsoft.ServiceFabric.AspNetCore.WebListener**.</span><span class="sxs-lookup"><span data-stu-id="7e153-183">WebListener can be used in a Reliable Service by importing the **Microsoft.ServiceFabric.AspNetCore.WebListener** NuGet package.</span></span> <span data-ttu-id="7e153-184">Questo pacchetto contiene `WebListenerCommunicationListener`, un'implementazione di `ICommunicationListener`, che consente di creare un WebHost ASP.NET Core all'interno di un servizio Reliable Services usando WebListener come server Web.</span><span class="sxs-lookup"><span data-stu-id="7e153-184">This package contains `WebListenerCommunicationListener`, an implementation of `ICommunicationListener`, that allows you to create an ASP.NET Core WebHost inside a Reliable Service using WebListener as the web server.</span></span>

<span data-ttu-id="7e153-185">WebListener si basa sull'[API server HTTP di Windows](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx),</span><span class="sxs-lookup"><span data-stu-id="7e153-185">WebListener is built on the [Windows HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx).</span></span> <span data-ttu-id="7e153-186">che usa il driver del kernel *http.sys* usato da IIS per elaborare le richieste HTTP e indirizzarle ai processi che eseguono le applicazioni Web.</span><span class="sxs-lookup"><span data-stu-id="7e153-186">This uses the *http.sys* kernel driver used by IIS to process HTTP requests and route them to processes running web applications.</span></span> <span data-ttu-id="7e153-187">Ciò consente a più processi nello stesso computer fisico o nella stessa macchina virtuale di ospitare applicazioni Web sulla stessa porta, identificate senza ambiguità dal nome host o dal percorso URL univoco.</span><span class="sxs-lookup"><span data-stu-id="7e153-187">This allows multiple processes on the same physical or virtual machine to host web applications on the same port, disambiguated by either a unique URL path or hostname.</span></span> <span data-ttu-id="7e153-188">Queste funzionalità sono utili in Service Fabric per ospitare più siti Web nello stesso cluster.</span><span class="sxs-lookup"><span data-stu-id="7e153-188">These features are useful in Service Fabric for hosting multiple websites in the same cluster.</span></span>

<span data-ttu-id="7e153-189">Il diagramma seguente illustra il modo in cui WebListener usa il driver del kernel *http.sys* in Windows per la condivisione delle porte:</span><span class="sxs-lookup"><span data-stu-id="7e153-189">The following diagram illustrates how WebListener uses the *http.sys* kernel driver on Windows for port sharing:</span></span>

![http.sys][3]

### <a name="weblistener-in-a-stateless-service"></a><span data-ttu-id="7e153-191">WebListener in un servizio senza stato</span><span class="sxs-lookup"><span data-stu-id="7e153-191">WebListener in a stateless service</span></span>
<span data-ttu-id="7e153-192">Per usare `WebListener` in un servizio senza stato, eseguire l'override del metodo `CreateServiceInstanceListeners` e restituire un'istanza `WebListenerCommunicationListener`:</span><span class="sxs-lookup"><span data-stu-id="7e153-192">To use `WebListener` in a stateless service, override the `CreateServiceInstanceListeners` method and return a `WebListenerCommunicationListener` instance:</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseWebListener()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build()))
    };
}
```

### <a name="weblistener-in-a-stateful-service"></a><span data-ttu-id="7e153-193">WebListener in un servizio con stato</span><span class="sxs-lookup"><span data-stu-id="7e153-193">WebListener in a stateful service</span></span>

<span data-ttu-id="7e153-194">`WebListenerCommunicationListener` non è attualmente progettato per l'uso in servizi con stato, a causa di problemi con la funzionalità di condivisione delle porte *http.sys* sottostante.</span><span class="sxs-lookup"><span data-stu-id="7e153-194">`WebListenerCommunicationListener` is currently not designed for use in stateful services due to complications with the underlying *http.sys* port sharing feature.</span></span> <span data-ttu-id="7e153-195">Per altre informazioni, vedere la sezione seguente sull'allocazione dinamica delle porte con WebListener.</span><span class="sxs-lookup"><span data-stu-id="7e153-195">For more information, see the following section on dynamic port allocation with WebListener.</span></span> <span data-ttu-id="7e153-196">Per i servizi con stato, Kestrel è il server Web consigliato.</span><span class="sxs-lookup"><span data-stu-id="7e153-196">For stateful services, Kestrel is the recommended web server.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="7e153-197">Configurazione dell'endpoint</span><span class="sxs-lookup"><span data-stu-id="7e153-197">Endpoint configuration</span></span>

<span data-ttu-id="7e153-198">È necessaria una configurazione `Endpoint` per i server Web che usano l'API server HTTP di Windows, tra cui WebListener.</span><span class="sxs-lookup"><span data-stu-id="7e153-198">An `Endpoint` configuration is required for web servers that use the Windows HTTP Server API, including WebListener.</span></span> <span data-ttu-id="7e153-199">I server Web che usano l'API server HTTP di Windows devono prima riservare i rispettivi URL con *http.sys*. Questa operazione viene in genere eseguita con lo strumento [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="7e153-199">Web servers that use the Windows HTTP Server API must first reserve their URL with *http.sys* (this is normally accomplished with the [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) tool).</span></span> <span data-ttu-id="7e153-200">Questa azione richiede privilegi elevati che i servizi non hanno per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="7e153-200">This action requires elevated privileges that your services by default do not have.</span></span> <span data-ttu-id="7e153-201">Le opzioni "http" o "https" per la proprietà `Protocol` della configurazione `Endpoint` in *ServiceManifest.xml* vengono usate specificamente per indicare al runtime di Service Fabric di registrare un URL con *http.sys* per conto dell'utente con il prefisso URL [*con caratteri jolly complessi*](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="7e153-201">The "http" or "https" options for the `Protocol` property of the `Endpoint` configuration in *ServiceManifest.xml* are used specifically to instruct the Service Fabric runtime to register a URL with *http.sys* on your behalf using the [*strong wildcard*](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) URL prefix.</span></span>

<span data-ttu-id="7e153-202">Per riservare ad esempio `http://+:80` per un servizio, è necessario usare la configurazione seguente in ServiceManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="7e153-202">For example, to reserve `http://+:80` for a service, the following configuration should be used in ServiceManifest.xml:</span></span>

```xml
<ServiceManifest ... >
    ...
    <Resources>
        <Endpoints>
            <Endpoint Name="ServiceEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>

</ServiceManifest>
```

<span data-ttu-id="7e153-203">Il nome dell'endpoint deve essere passato al costruttore `WebListenerCommunicationListener`:</span><span class="sxs-lookup"><span data-stu-id="7e153-203">And the endpoint name must be passed to the `WebListenerCommunicationListener` constructor:</span></span>

```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     return new WebHostBuilder()
         .UseWebListener()
         .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
         .UseUrls(url)
         .Build();
 })
```

#### <a name="use-weblistener-with-a-static-port"></a><span data-ttu-id="7e153-204">Usare WebListener con una porta statica</span><span class="sxs-lookup"><span data-stu-id="7e153-204">Use WebListener with a static port</span></span>
<span data-ttu-id="7e153-205">Per usare una porta statica con WebListener, specificare il numero della porta nella configurazione `Endpoint`:</span><span class="sxs-lookup"><span data-stu-id="7e153-205">To use a static port with WebListener, provide the port number in the `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

#### <a name="use-weblistener-with-a-dynamic-port"></a><span data-ttu-id="7e153-206">Usare WebListener con una porta dinamica</span><span class="sxs-lookup"><span data-stu-id="7e153-206">Use WebListener with a dynamic port</span></span>
<span data-ttu-id="7e153-207">Per usare una porta assegnata dinamicamente con WebListener, omettere la proprietà `Port` nella configurazione `Endpoint`:</span><span class="sxs-lookup"><span data-stu-id="7e153-207">To use a dynamically assigned port with WebListener, omit the `Port` property in the `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="7e153-208">Si noti che una porta dinamica allocata da una configurazione `Endpoint` fornisce una sola porta *per ogni processo host*.</span><span class="sxs-lookup"><span data-stu-id="7e153-208">Note that a dynamic port allocated by an `Endpoint` configuration only provides one port *per host process*.</span></span> <span data-ttu-id="7e153-209">Il modello di hosting corrente di Service Fabric consente l'hosting di più istanze e/o repliche del servizio nello stesso processo, vale a dire che ognuna condivide la stessa porta, se allocata tramite la configurazione `Endpoint`.</span><span class="sxs-lookup"><span data-stu-id="7e153-209">The current Service Fabric hosting model allows multiple service instances and/or replicas to be hosted in the same process, meaning that each one will share the same port when allocated through the `Endpoint` configuration.</span></span> <span data-ttu-id="7e153-210">Più istanze di WebListener possono condividere una porta usando la funzionalità di condivisione delle porte *http.sys* sottostante, ma questa funzionalità non è supportata da `WebListenerCommunicationListener` a causa dei problemi che provoca per le richieste dei client.</span><span class="sxs-lookup"><span data-stu-id="7e153-210">Multiple WebListener instances can share a port using the underlying *http.sys* port sharing feature, but that is not supported by `WebListenerCommunicationListener` due to the complications it introduces for client requests.</span></span> <span data-ttu-id="7e153-211">Per l'uso delle porte dinamiche, Kestrel è il server Web consigliato.</span><span class="sxs-lookup"><span data-stu-id="7e153-211">For dynamic port usage, Kestrel is the recommended web server.</span></span>

## <a name="kestrel-in-reliable-services"></a><span data-ttu-id="7e153-212">Kestrel in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="7e153-212">Kestrel in Reliable Services</span></span>
<span data-ttu-id="7e153-213">Kestrel può essere usato in un servizio Reliable Services importando il pacchetto NuGet **Microsoft.ServiceFabric.AspNetCore.Kestrel**.</span><span class="sxs-lookup"><span data-stu-id="7e153-213">Kestrel can be used in a Reliable Service by importing the **Microsoft.ServiceFabric.AspNetCore.Kestrel** NuGet package.</span></span> <span data-ttu-id="7e153-214">Questo pacchetto contiene `KestrelCommunicationListener`, un'implementazione di `ICommunicationListener`, che consente di creare un WebHost ASP.NET Core all'interno di un servizio Reliable Services usando Kestrel come server Web.</span><span class="sxs-lookup"><span data-stu-id="7e153-214">This package contains `KestrelCommunicationListener`, an implementation of `ICommunicationListener`, that allows you to create an ASP.NET Core WebHost inside a Reliable Service using Kestrel as the web server.</span></span>

<span data-ttu-id="7e153-215">Kestrel è che un server Web multipiattaforma per ASP.NET Core basato su libuv, una libreria I/O asincrona multipiattaforma.</span><span class="sxs-lookup"><span data-stu-id="7e153-215">Kestrel is a cross-platform web server for ASP.NET Core based on libuv, a cross-platform asynchronous I/O library.</span></span> <span data-ttu-id="7e153-216">A differenza di WebListener, Kestrel non usa una gestione centralizzata dell'endpoint come *http.sys*.</span><span class="sxs-lookup"><span data-stu-id="7e153-216">Unlike WebListener, Kestrel does not use a centralized endpoint manager such as *http.sys*.</span></span> <span data-ttu-id="7e153-217">A differenza di WebListener, Kestrel non supporta la condivisione delle porte tra più processi.</span><span class="sxs-lookup"><span data-stu-id="7e153-217">And unlike WebListener, Kestrel does not support port sharing between multiple processes.</span></span> <span data-ttu-id="7e153-218">Ogni istanza di Kestrel deve usare una porta univoca.</span><span class="sxs-lookup"><span data-stu-id="7e153-218">Each instance of Kestrel must use a unique port.</span></span>

![kestrel][4]

### <a name="kestrel-in-a-stateless-service"></a><span data-ttu-id="7e153-220">Kestrel in un servizio senza stato</span><span class="sxs-lookup"><span data-stu-id="7e153-220">Kestrel in a stateless service</span></span>
<span data-ttu-id="7e153-221">Per usare `Kestrel` in un servizio senza stato, eseguire l'override del metodo `CreateServiceInstanceListeners` e restituire un'istanza `KestrelCommunicationListener`:</span><span class="sxs-lookup"><span data-stu-id="7e153-221">To use `Kestrel` in a stateless service, override the `CreateServiceInstanceListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

### <a name="kestrel-in-a-stateful-service"></a><span data-ttu-id="7e153-222">Kestrel in un servizio con stato</span><span class="sxs-lookup"><span data-stu-id="7e153-222">Kestrel in a stateful service</span></span>
<span data-ttu-id="7e153-223">Per usare `Kestrel` in un servizio con stato, eseguire l'override del metodo `CreateServiceReplicaListeners` e restituire un'istanza `KestrelCommunicationListener`:</span><span class="sxs-lookup"><span data-stu-id="7e153-223">To use `Kestrel` in a stateful service, override the `CreateServiceReplicaListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new ServiceReplicaListener[]
    {
        new ServiceReplicaListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                         services => services
                             .AddSingleton<StatefulServiceContext>(serviceContext)
                             .AddSingleton<IReliableStateManager>(this.StateManager))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

<span data-ttu-id="7e153-224">In questo esempio viene fornita un'istanza singleton di `IReliableStateManager` al contenitore di inserimento delle dipendenze WebHost.</span><span class="sxs-lookup"><span data-stu-id="7e153-224">In this example, a singleton instance of `IReliableStateManager` is provided to the WebHost dependency injection container.</span></span> <span data-ttu-id="7e153-225">Questa operazione non è strettamente necessaria, ma consente di usare `IReliableStateManager` e Reliable Collections nei metodi di azione del controller MVC.</span><span class="sxs-lookup"><span data-stu-id="7e153-225">This is not strictly necessary, but it allows you to use `IReliableStateManager` and Reliable Collections in your MVC controller action methods.</span></span>

<span data-ttu-id="7e153-226">Si noti che **non** viene fornito un nome di configurazione `Endpoint` a `KestrelCommunicationListener` in un servizio con stato,</span><span class="sxs-lookup"><span data-stu-id="7e153-226">Note that an `Endpoint` configuration name is **not** provided to `KestrelCommunicationListener` in a stateful service.</span></span> <span data-ttu-id="7e153-227">come spiegato più dettagliatamente nella sezione seguente.</span><span class="sxs-lookup"><span data-stu-id="7e153-227">This is explained in more detail in the following section.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="7e153-228">Configurazione dell'endpoint</span><span class="sxs-lookup"><span data-stu-id="7e153-228">Endpoint configuration</span></span>
<span data-ttu-id="7e153-229">Non è necessaria una configurazione `Endpoint` per usare Kestrel.</span><span class="sxs-lookup"><span data-stu-id="7e153-229">An `Endpoint` configuration is not required to use Kestrel.</span></span> 

<span data-ttu-id="7e153-230">Kestrel è un server Web autonomo semplice e a differenza di WebListener (o HttpListener) non necessita di una configurazione `Endpoint` in *ServiceManifest.xml* perché non richiede la registrazione dell'URL prima dell'avvio.</span><span class="sxs-lookup"><span data-stu-id="7e153-230">Kestrel is a simple stand-alone web server; unlike WebListener (or HttpListener), it does not need an `Endpoint` configuration in *ServiceManifest.xml* because it does not require URL registration prior to starting.</span></span> 

#### <a name="use-kestrel-with-a-static-port"></a><span data-ttu-id="7e153-231">Usare Kestrel con una porta statica</span><span class="sxs-lookup"><span data-stu-id="7e153-231">Use Kestrel with a static port</span></span>
<span data-ttu-id="7e153-232">È possibile definire una porta statica nella configurazione `Endpoint` di ServiceManifest.xml per l'uso con Kestrel.</span><span class="sxs-lookup"><span data-stu-id="7e153-232">A static port can be configured in the `Endpoint` configuration of ServiceManifest.xml for use with Kestrel.</span></span> <span data-ttu-id="7e153-233">Anche se non è strettamente necessaria, questa operazione offre due vantaggi potenziali:</span><span class="sxs-lookup"><span data-stu-id="7e153-233">Although this is not strictly necessary, it provides two potential benefits:</span></span>
 1. <span data-ttu-id="7e153-234">Se la porta non rientra nell'intervallo di porte dell'applicazione, verrà aperta da Service Fabric nel firewall del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="7e153-234">If the port does not fall in the application port range, it is opened through the OS firewall by Service Fabric.</span></span>
 2. <span data-ttu-id="7e153-235">L'URL fornito all'utente tramite `KestrelCommunicationListener` userà questa porta.</span><span class="sxs-lookup"><span data-stu-id="7e153-235">The URL provided to you through `KestrelCommunicationListener` will use this port.</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="7e153-236">Se è configurato un `Endpoint`, il nome deve essere passato al costruttore `KestrelCommunicationListener`:</span><span class="sxs-lookup"><span data-stu-id="7e153-236">If an `Endpoint` is configured, its name must be passed into the `KestrelCommunicationListener` constructor:</span></span> 

```csharp
new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) => ...
```

<span data-ttu-id="7e153-237">Se non viene usata una configurazione `Endpoint`, omettere il nome nel costruttore `KestrelCommunicationListener`.</span><span class="sxs-lookup"><span data-stu-id="7e153-237">If an `Endpoint` configuration is not used, omit the name in the `KestrelCommunicationListener` constructor.</span></span> <span data-ttu-id="7e153-238">In questo caso verrà usata una porta dinamica.</span><span class="sxs-lookup"><span data-stu-id="7e153-238">In this case, a dynamic port will be used.</span></span> <span data-ttu-id="7e153-239">Per altre informazioni, vedere la sezione seguente.</span><span class="sxs-lookup"><span data-stu-id="7e153-239">See the next section for more information.</span></span>

#### <a name="use-kestrel-with-a-dynamic-port"></a><span data-ttu-id="7e153-240">Usare Kestrel con una porta dinamica</span><span class="sxs-lookup"><span data-stu-id="7e153-240">Use Kestrel with a dynamic port</span></span>
<span data-ttu-id="7e153-241">Kestrel non può usare l'assegnazione automatica delle porte della configurazione `Endpoint` in ServiceManifest.xml, perché l'assegnazione automatica delle porte di una configurazione `Endpoint` assegna una porta univoca per ogni *processo host* e un singolo processo host può contenere più istanze di Kestrel.</span><span class="sxs-lookup"><span data-stu-id="7e153-241">Kestrel cannot use the automatic port assignment from the `Endpoint` configuration in ServiceManifest.xml, because automatic port assignment from an `Endpoint` configuration assigns a unique port per *host process*, and a single host process can contain multiple Kestrel instances.</span></span> <span data-ttu-id="7e153-242">Poiché Kestrel non supporta la condivisione delle porte, questa modalità di assegnazione non funziona perché ogni istanza di Kestrel deve essere aperta in una porta univoca.</span><span class="sxs-lookup"><span data-stu-id="7e153-242">Since Kestrel does not support port sharing, this does not work as each Kestrel instance must be opened on a unique port.</span></span>

<span data-ttu-id="7e153-243">Per usare l'assegnazione dinamica delle porte con Kestrel è sufficiente omettere del tutto la configurazione `Endpoint` in ServiceManifest.xml e non passare un nome endpoint al costruttore `KestrelCommunicationListener`:</span><span class="sxs-lookup"><span data-stu-id="7e153-243">To use dynamic port assignment with Kestrel, simply omit the `Endpoint` configuration in ServiceManifest.xml entirely, and do not pass an endpoint name to the `KestrelCommunicationListener` constructor:</span></span>

```csharp
new KestrelCommunicationListener(serviceContext, (url, listener) => ...
```

<span data-ttu-id="7e153-244">In questa configurazione, `KestrelCommunicationListener` selezionerà automaticamente una porta non usata dall'intervallo di porte dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7e153-244">In this configuration, `KestrelCommunicationListener` will automatically select an unused port from the application port range.</span></span>

## <a name="scenarios-and-configurations"></a><span data-ttu-id="7e153-245">Scenari e configurazioni</span><span class="sxs-lookup"><span data-stu-id="7e153-245">Scenarios and configurations</span></span>
<span data-ttu-id="7e153-246">Questa sezione descrive gli scenari seguenti e offre la combinazione consigliata di server Web, configurazione delle porte, opzioni di integrazione di Service Fabric e altre impostazioni per ottenere un servizio che funzioni correttamente:</span><span class="sxs-lookup"><span data-stu-id="7e153-246">This section describes the following scenarios and provides the recommended combination of web server, port configuration, Service Fabric integration options, and miscellaneous settings to achieve a properly functioning service:</span></span>
 - <span data-ttu-id="7e153-247">Servizio ASP.NET Core senza stato esposto all'esterno</span><span class="sxs-lookup"><span data-stu-id="7e153-247">Externally exposed ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="7e153-248">Servizio ASP.NET Core senza stato solo interno</span><span class="sxs-lookup"><span data-stu-id="7e153-248">Internal-only ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="7e153-249">Servizio ASP.NET Core con stato solo interno</span><span class="sxs-lookup"><span data-stu-id="7e153-249">Internal-only ASP.NET Core stateful service</span></span>

<span data-ttu-id="7e153-250">Un servizio **esposto all'esterno** è un servizio che espone un endpoint raggiungibile dall'esterno del cluster, in genere tramite un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="7e153-250">An **externally exposed** service is one that exposes an endpoint reachable from outside the cluster, usually through a load balancer.</span></span>

<span data-ttu-id="7e153-251">Un servizio **solo interno** è un servizio il cui endpoint è raggiungibile solo dall'interno del cluster.</span><span class="sxs-lookup"><span data-stu-id="7e153-251">An **internal-only** service is one whose endpoint is only reachable from within the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="7e153-252">Gli endpoint di servizio con stato non devono essere in genere esposti a Internet.</span><span class="sxs-lookup"><span data-stu-id="7e153-252">Stateful service endpoints generally should not be exposed to the Internet.</span></span> <span data-ttu-id="7e153-253">I cluster che si trovano dietro a servizi di bilanciamento del carico che non rilevano la risoluzione del servizio di Service Fabric, ad esempio Azure Load Balancer, non possono esporre i servizi con stato perché il servizio di bilanciamento del carico non può individuare e instradare il traffico alla replica del servizio con stato appropriata.</span><span class="sxs-lookup"><span data-stu-id="7e153-253">Clusters that are behind load balancers that are unaware of Service Fabric service resolution, such as the Azure Load Balancer, will be unable to expose stateful services because the load balancer will not be able to locate and route traffic to the appropriate stateful service replica.</span></span> 

### <a name="externally-exposed-aspnet-core-stateless-services"></a><span data-ttu-id="7e153-254">Servizi ASP.NET Core senza stato esposti all'esterno</span><span class="sxs-lookup"><span data-stu-id="7e153-254">Externally exposed ASP.NET Core stateless services</span></span>
<span data-ttu-id="7e153-255">WebListener è il server Web consigliato per i servizi front-end che espongono endpoint HTTP Internet esterni in Windows.</span><span class="sxs-lookup"><span data-stu-id="7e153-255">WebListener is the recommended web server for front-end services that expose external, Internet-facing HTTP endpoints on Windows.</span></span> <span data-ttu-id="7e153-256">Offre una migliore protezione dagli attacchi e supporta funzionalità non supportate da Kestrel, ad esempio l'autenticazione di Windows e la condivisione delle porte.</span><span class="sxs-lookup"><span data-stu-id="7e153-256">It provides better protection against attacks and supports features that Kestrel does not, such as Windows Authentication and port sharing.</span></span> 

<span data-ttu-id="7e153-257">Kestrel non è attualmente supportato come server perimetrale per Internet.</span><span class="sxs-lookup"><span data-stu-id="7e153-257">Kestrel is not supported as an edge (Internet-facing) server at this time.</span></span> <span data-ttu-id="7e153-258">È necessario usare un server proxy inverso, ad esempio IIS o Nginx, per gestire il traffico da Internet pubblico.</span><span class="sxs-lookup"><span data-stu-id="7e153-258">A reverse proxy server such as IIS or Nginx must be used to handle traffic from the public Internet.</span></span>
 
<span data-ttu-id="7e153-259">Quando è esposto a Internet, un servizio senza stato deve usare un endpoint noto e stabile raggiungibile tramite un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="7e153-259">When exposed to the Internet, a stateless service should use a well-known and stable endpoint that is reachable through a load balancer.</span></span> <span data-ttu-id="7e153-260">Si tratta dell'URL che verrà fornito agli utenti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7e153-260">This is the URL you will provide to users of your application.</span></span> <span data-ttu-id="7e153-261">È consigliabile la configurazione seguente:</span><span class="sxs-lookup"><span data-stu-id="7e153-261">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="7e153-262">**Note**</span><span class="sxs-lookup"><span data-stu-id="7e153-262">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7e153-263">Server Web</span><span class="sxs-lookup"><span data-stu-id="7e153-263">Web server</span></span> | <span data-ttu-id="7e153-264">WebListener</span><span class="sxs-lookup"><span data-stu-id="7e153-264">WebListener</span></span> | <span data-ttu-id="7e153-265">Se il servizio viene esposto solo a una rete attendibile, ad esempio una rete Intranet, è possibile usare Kestrel.</span><span class="sxs-lookup"><span data-stu-id="7e153-265">If the service is only exposed to a trusted network, such an intranet, Kestrel may be used.</span></span> <span data-ttu-id="7e153-266">In caso contrario, WebListener è l'opzione preferita.</span><span class="sxs-lookup"><span data-stu-id="7e153-266">Otherwise, WebListener is the preferred option.</span></span> |
| <span data-ttu-id="7e153-267">Configurazione delle porte</span><span class="sxs-lookup"><span data-stu-id="7e153-267">Port configuration</span></span> | <span data-ttu-id="7e153-268">Statica</span><span class="sxs-lookup"><span data-stu-id="7e153-268">static</span></span> | <span data-ttu-id="7e153-269">È necessario configurare una porta statica nota nella configurazione `Endpoints` di ServiceManifest.xml, ad esempio 80 per HTTP o 443 per HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7e153-269">A well-known static port should be configured in the `Endpoints` configuration of ServiceManifest.xml, such as 80 for HTTP or 443 for HTTPS.</span></span> |
| <span data-ttu-id="7e153-270">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="7e153-270">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="7e153-271">None</span><span class="sxs-lookup"><span data-stu-id="7e153-271">None</span></span> | <span data-ttu-id="7e153-272">È necessario usare l'opzione `ServiceFabricIntegrationOptions.None` quando si configura il middleware di integrazione di Service Fabric, in modo che il servizio non provi a convalidare le richieste in ingresso per un identificatore univoco.</span><span class="sxs-lookup"><span data-stu-id="7e153-272">The `ServiceFabricIntegrationOptions.None` option should be used when configuring Service Fabric integration middleware so that the service does not attempt to validate incoming requests for a unique identifier.</span></span> <span data-ttu-id="7e153-273">Gli utenti esterni dell'applicazione non saranno a conoscenza delle informazioni di identificazione univoche usate dal middleware.</span><span class="sxs-lookup"><span data-stu-id="7e153-273">External users of your application will not know the unique identifying information used by the middleware.</span></span> |
| <span data-ttu-id="7e153-274">Conteggio istanze</span><span class="sxs-lookup"><span data-stu-id="7e153-274">Instance Count</span></span> | <span data-ttu-id="7e153-275">-1</span><span class="sxs-lookup"><span data-stu-id="7e153-275">-1</span></span> | <span data-ttu-id="7e153-276">In casi d'uso tipici, l'impostazione del numero di istanze deve essere "-1" in modo che un'istanza sia disponibile in tutti i nodi che ricevono il traffico da un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="7e153-276">In typical use cases, the instance count setting should be set to "-1" so that an instance is available on all nodes that receive traffic from a load balancer.</span></span> |

<span data-ttu-id="7e153-277">Se più servizi esposti all'esterno condividono lo stesso set di nodi, usare un percorso URL univoco ma stabile,</span><span class="sxs-lookup"><span data-stu-id="7e153-277">If multiple externally exposed services share the same set of nodes, a unique but stable URL path should be used.</span></span> <span data-ttu-id="7e153-278">modificando l'URL specificato durante la configurazione di IWebHost.</span><span class="sxs-lookup"><span data-stu-id="7e153-278">This can be accomplished by modifying the URL provided when configuring IWebHost.</span></span> <span data-ttu-id="7e153-279">Si noti che questa operazione è applicabile solo a WebListener.</span><span class="sxs-lookup"><span data-stu-id="7e153-279">Note this applies to WebListener only.</span></span>

 ```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     url += "/MyUniqueServicePath";
 
     return new WebHostBuilder()
         .UseWebListener()
         ...
         .UseUrls(url)
         .Build();
 })
 ```

### <a name="internal-only-stateless-aspnet-core-service"></a><span data-ttu-id="7e153-280">Servizio ASP.NET Core senza stato solo interno</span><span class="sxs-lookup"><span data-stu-id="7e153-280">Internal-only stateless ASP.NET Core service</span></span>
<span data-ttu-id="7e153-281">I servizi senza stato che vengono chiamati solo dall'interno del cluster devono usare URL univoci e porte assegnate dinamicamente per assicurare la cooperazione tra più servizi.</span><span class="sxs-lookup"><span data-stu-id="7e153-281">Stateless services that are only called from within the cluster should use unique URLs and dynamically assigned ports to ensure cooperation between multiple services.</span></span> <span data-ttu-id="7e153-282">È consigliabile la configurazione seguente:</span><span class="sxs-lookup"><span data-stu-id="7e153-282">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="7e153-283">**Note**</span><span class="sxs-lookup"><span data-stu-id="7e153-283">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7e153-284">Server Web</span><span class="sxs-lookup"><span data-stu-id="7e153-284">Web server</span></span> | <span data-ttu-id="7e153-285">Kestrel</span><span class="sxs-lookup"><span data-stu-id="7e153-285">Kestrel</span></span> | <span data-ttu-id="7e153-286">Anche se è possibile usare WebListener per i servizi interni senza stato, Kestrel è il server consigliato per consentire la condivisione di un host da parte di più istanze del servizio.</span><span class="sxs-lookup"><span data-stu-id="7e153-286">Although WebListener may be used for internal stateless services, Kestrel is the recommended server to allow multiple service instances to share a host.</span></span>  |
| <span data-ttu-id="7e153-287">Configurazione delle porte</span><span class="sxs-lookup"><span data-stu-id="7e153-287">Port configuration</span></span> | <span data-ttu-id="7e153-288">assegnate in modo dinamico</span><span class="sxs-lookup"><span data-stu-id="7e153-288">dynamically assigned</span></span> | <span data-ttu-id="7e153-289">Più repliche di un servizio con stato possono condividere un processo host o un sistema operativo host e richiedono quindi porte univoche.</span><span class="sxs-lookup"><span data-stu-id="7e153-289">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="7e153-290">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="7e153-290">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="7e153-291">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="7e153-291">UseUniqueServiceUrl</span></span> | <span data-ttu-id="7e153-292">Con l'assegnazione dinamica delle porte, questa impostazione evita il problema di errata identificazione descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="7e153-292">With dynamic port assignment, this setting prevents the mistaken identity issue described earlier.</span></span> |
| <span data-ttu-id="7e153-293">InstanceCount</span><span class="sxs-lookup"><span data-stu-id="7e153-293">InstanceCount</span></span> | <span data-ttu-id="7e153-294">qualsiasi</span><span class="sxs-lookup"><span data-stu-id="7e153-294">any</span></span> | <span data-ttu-id="7e153-295">Il numero di istanze può essere impostato su qualsiasi valore necessario per il funzionamento del servizio.</span><span class="sxs-lookup"><span data-stu-id="7e153-295">The instance count setting can be set to any value necessary to operate the service.</span></span> |

### <a name="internal-only-stateful-aspnet-core-service"></a><span data-ttu-id="7e153-296">Servizio ASP.NET Core con stato solo interno</span><span class="sxs-lookup"><span data-stu-id="7e153-296">Internal-only stateful ASP.NET Core service</span></span>
<span data-ttu-id="7e153-297">I servizi con stato che vengono chiamati solo dall'interno del cluster devono usare porte assegnate dinamicamente per assicurare la cooperazione tra più servizi.</span><span class="sxs-lookup"><span data-stu-id="7e153-297">Stateful services that are only called from within the cluster should use dynamically assigned ports to ensure cooperation between multiple services.</span></span> <span data-ttu-id="7e153-298">È consigliabile la configurazione seguente:</span><span class="sxs-lookup"><span data-stu-id="7e153-298">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="7e153-299">**Note**</span><span class="sxs-lookup"><span data-stu-id="7e153-299">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7e153-300">Server Web</span><span class="sxs-lookup"><span data-stu-id="7e153-300">Web server</span></span> | <span data-ttu-id="7e153-301">Kestrel</span><span class="sxs-lookup"><span data-stu-id="7e153-301">Kestrel</span></span> | <span data-ttu-id="7e153-302">`WebListenerCommunicationListener` non può essere usato dai servizi con stato in cui le repliche condividono un processo host.</span><span class="sxs-lookup"><span data-stu-id="7e153-302">The `WebListenerCommunicationListener` is not designed for use by stateful services in which replicas share a host process.</span></span> |
| <span data-ttu-id="7e153-303">Configurazione delle porte</span><span class="sxs-lookup"><span data-stu-id="7e153-303">Port configuration</span></span> | <span data-ttu-id="7e153-304">assegnate in modo dinamico</span><span class="sxs-lookup"><span data-stu-id="7e153-304">dynamically assigned</span></span> | <span data-ttu-id="7e153-305">Più repliche di un servizio con stato possono condividere un processo host o un sistema operativo host e richiedono quindi porte univoche.</span><span class="sxs-lookup"><span data-stu-id="7e153-305">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="7e153-306">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="7e153-306">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="7e153-307">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="7e153-307">UseUniqueServiceUrl</span></span> | <span data-ttu-id="7e153-308">Con l'assegnazione dinamica delle porte, questa impostazione evita il problema di errata identificazione descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="7e153-308">With dynamic port assignment, this setting prevents the mistaken identity issue described earlier.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7e153-309">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7e153-309">Next steps</span></span>
[<span data-ttu-id="7e153-310">Debug dell'applicazione di Service Fabric mediante Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7e153-310">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

<!--Image references-->
[0]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-standalone.png
[1]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-servicefabric.png
[2]:./media/service-fabric-reliable-services-communication-aspnetcore/integration.png
[3]:./media/service-fabric-reliable-services-communication-aspnetcore/httpsys.png
[4]:./media/service-fabric-reliable-services-communication-aspnetcore/kestrel.png
