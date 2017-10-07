---
title: la comunicazione con ASP.NET Web API hello aaaService | Documenti Microsoft
description: Informazioni su come la comunicazione dei servizi tooimplement dettagliata tramite hello ASP.NET Web API con OWIN self-hosting in hello affidabile API dei servizi.
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
ms.date: 02/10/2017
ms.author: vturecek
redirect_url: /azure/service-fabric/service-fabric-reliable-services-communication-aspnetcore
ms.openlocfilehash: 3fb18fcb141ada0d79a0acda3dccbc7fb044346d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-service-fabric-web-api-services-with-owin-self-hosting"></a><span data-ttu-id="18cc5-103">Introduzione ai servizi API Web di Service Fabric con self-hosting OWIN</span><span class="sxs-lookup"><span data-stu-id="18cc5-103">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>
<span data-ttu-id="18cc5-104">Azure Service Fabric pone power hello in pratiche per decidere come si desidera toocommunicate i servizi con utenti e tra loro.</span><span class="sxs-lookup"><span data-stu-id="18cc5-104">Azure Service Fabric puts hello power in your hands when you're deciding how you want your services toocommunicate with users and with each other.</span></span> <span data-ttu-id="18cc5-105">Questa esercitazione è incentrata sull'implementazione della comunicazione dei servizi mediante l'API Web ASP.NET con self-hosting OWIN (Open Web Interface for .NET) nell'API di Reliable Services di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="18cc5-105">This tutorial focuses on implementing service communication using ASP.NET Web API with Open Web Interface for .NET (OWIN) self-hosting in Service Fabric's Reliable Services API.</span></span> <span data-ttu-id="18cc5-106">Approfondiremo eccessivamente hello comunicazione modulare di servizi affidabili API.</span><span class="sxs-lookup"><span data-stu-id="18cc5-106">We'll delve deeply into hello Reliable Services pluggable communication API.</span></span> <span data-ttu-id="18cc5-107">Si userà API Web in un esempio dettagliato di tooshow è come tooset di un listener personalizzate di comunicazione.</span><span class="sxs-lookup"><span data-stu-id="18cc5-107">We'll also use Web API in a step-by-step example tooshow you how tooset up a custom communication listener.</span></span>

## <a name="introduction-tooweb-api-in-service-fabric"></a><span data-ttu-id="18cc5-108">Introduzione tooWeb API in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="18cc5-108">Introduction tooWeb API in Service Fabric</span></span>
<span data-ttu-id="18cc5-109">API Web ASP.NET è un framework comune e potente per la compilazione di APIs HTTP su hello .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="18cc5-109">ASP.NET Web API is a popular and powerful framework for building HTTP APIs on top of hello .NET Framework.</span></span> <span data-ttu-id="18cc5-110">Se non si ha già familiarità con framework hello, vedere [Introduzione a ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) toolearn altre.</span><span class="sxs-lookup"><span data-stu-id="18cc5-110">If you're not already familiar with hello framework, see [Getting started with ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) toolearn more.</span></span>

<span data-ttu-id="18cc5-111">API Web Service Fabric è hello stessa noto e apprezzato di API Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="18cc5-111">Web API in Service Fabric is hello same ASP.NET Web API you know and love.</span></span> <span data-ttu-id="18cc5-112">Hello differenza consiste nella procedura si *host* un'applicazione Web API.</span><span class="sxs-lookup"><span data-stu-id="18cc5-112">hello difference is in how you *host* a Web API application.</span></span> <span data-ttu-id="18cc5-113">Non si userà Microsoft Internet Information Services (IIS).</span><span class="sxs-lookup"><span data-stu-id="18cc5-113">You won't be using Microsoft Internet Information Services (IIS).</span></span> <span data-ttu-id="18cc5-114">toobetter comprendere la differenza hello, è possibile suddividerla in due parti:</span><span class="sxs-lookup"><span data-stu-id="18cc5-114">toobetter understand hello difference, let's break it into two parts:</span></span>

1. <span data-ttu-id="18cc5-115">applicazione Web API Hello (inclusi i controller e i modelli)</span><span class="sxs-lookup"><span data-stu-id="18cc5-115">hello Web API application (including controllers and models)</span></span>
2. <span data-ttu-id="18cc5-116">host Hello (hello web server IIS in genere)</span><span class="sxs-lookup"><span data-stu-id="18cc5-116">hello host (hello web server, usually IIS)</span></span>

<span data-ttu-id="18cc5-117">L'applicazione API Web non cambia.</span><span class="sxs-lookup"><span data-stu-id="18cc5-117">A Web API application itself doesn't change.</span></span> <span data-ttu-id="18cc5-118">Non diverse dalle applicazioni Web API che scritto in hello precedente e dovrebbe essere in grado di toosimply sposta sulla maggior parte del codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="18cc5-118">It's no different from Web API applications you may have written in hello past, and you should be able toosimply move over most of your application code.</span></span> <span data-ttu-id="18cc5-119">Ma se è stata hosting in IIS, in cui ospitare un'applicazione hello potrebbe essere leggermente diverso da quello che si sta per.</span><span class="sxs-lookup"><span data-stu-id="18cc5-119">But if you've been hosting on IIS, where you host hello application may be a little different from what you're used to.</span></span> <span data-ttu-id="18cc5-120">Prima di passare toohello hosting parte, iniziamo con qualcosa di più familiari: hello applicazione API Web.</span><span class="sxs-lookup"><span data-stu-id="18cc5-120">Before we get toohello hosting part, let's start with something more familiar: hello Web API application.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="18cc5-121">Creare un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="18cc5-121">Create hello application</span></span>
<span data-ttu-id="18cc5-122">Iniziare creando una nuova applicazione Service Fabric con un singolo servizio senza stato in Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="18cc5-122">Start by creating a new Service Fabric application with a single stateless service in Visual Studio 2015.</span></span>

<span data-ttu-id="18cc5-123">Un modello di Visual Studio per un servizio senza stato mediante API Web è tooyou disponibili.</span><span class="sxs-lookup"><span data-stu-id="18cc5-123">A Visual Studio template for a stateless service using Web API is available tooyou.</span></span> <span data-ttu-id="18cc5-124">In questa esercitazione verrà compilato da zero un progetto API Web che genera un risultato simile a ciò che si otterrebbe selezionando tale modello.</span><span class="sxs-lookup"><span data-stu-id="18cc5-124">In this tutorial, we'll build a Web API project from scratch that results in what you'd get if you selected this template.</span></span>

<span data-ttu-id="18cc5-125">Selezionare un progetto di servizio senza stato vuoto toolearn come toobuild un progetto di API Web da zero, oppure è possibile iniziare con il servizio senza stato hello modello API Web e semplicemente seguire la procedura.</span><span class="sxs-lookup"><span data-stu-id="18cc5-125">Select a blank Stateless Service project toolearn how toobuild a Web API project from scratch, or you can start with hello stateless service Web API template and simply follow along.</span></span>  

<span data-ttu-id="18cc5-126">primo passaggio Hello è toopull in alcuni pacchetti NuGet per l'API Web.</span><span class="sxs-lookup"><span data-stu-id="18cc5-126">hello first step is toopull in some NuGet packages for Web API.</span></span> <span data-ttu-id="18cc5-127">pacchetto di Hello desideriamo toouse è Microsoft.AspNet.WebApi.OwinSelfHost.</span><span class="sxs-lookup"><span data-stu-id="18cc5-127">hello package we want toouse is Microsoft.AspNet.WebApi.OwinSelfHost.</span></span> <span data-ttu-id="18cc5-128">Questo pacchetto include tutti i pacchetti hello necessari API Web e hello *host* pacchetti.</span><span class="sxs-lookup"><span data-stu-id="18cc5-128">This package includes all hello necessary Web API packages and hello *host* packages.</span></span> <span data-ttu-id="18cc5-129">che saranno importanti in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="18cc5-129">This will be important later.</span></span>

<span data-ttu-id="18cc5-130">Dopo l'installazione di pacchetti hello, è possibile iniziare a costruire la struttura del progetto API Web basic hello.</span><span class="sxs-lookup"><span data-stu-id="18cc5-130">After hello packages have been installed, you can begin building out hello basic Web API project structure.</span></span> <span data-ttu-id="18cc5-131">Se è stata usata l'API Web, struttura del progetto hello dovrebbe essere molto familiare.</span><span class="sxs-lookup"><span data-stu-id="18cc5-131">If you've used Web API, hello project structure should look very familiar.</span></span> <span data-ttu-id="18cc5-132">Iniziare aggiungendo una directory `Controllers` e un semplice controller di valori:</span><span class="sxs-lookup"><span data-stu-id="18cc5-132">Start by adding a `Controllers` directory and a simple values controller:</span></span>

<span data-ttu-id="18cc5-133">**ValuesController.cs**</span><span class="sxs-lookup"><span data-stu-id="18cc5-133">**ValuesController.cs**</span></span>

```csharp
using System.Collections.Generic;
using System.Web.Http;

namespace WebService.Controllers
{
    public class ValuesController : ApiController
    {
        // GET api/values 
        public IEnumerable<string> Get()
        {
            return new string[] { "value1", "value2" };
        }

        // GET api/values/5 
        public string Get(int id)
        {
            return "value";
        }

        // POST api/values 
        public void Post([FromBody]string value)
        {
        }

        // PUT api/values/5 
        public void Put(int id, [FromBody]string value)
        {
        }

        // DELETE api/values/5 
        public void Delete(int id)
        {
        }
    }
}

```

<span data-ttu-id="18cc5-134">Successivamente, aggiungere una classe di avvio in hello progetto radice tooregister hello routing formattatori e altre impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="18cc5-134">Next, add a Startup class at hello project root tooregister hello routing, formatters, and any other configuration setup.</span></span> <span data-ttu-id="18cc5-135">Si tratta di API Web in cui inserisce toohello *host*, che sarà possibile accedere più tardi.</span><span class="sxs-lookup"><span data-stu-id="18cc5-135">This is also where Web API plugs in toohello *host*, which will be revisited again later.</span></span> 

<span data-ttu-id="18cc5-136">**Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="18cc5-136">**Startup.cs**</span></span>

```csharp
using System.Web.Http;
using Owin;

namespace WebService
{
    public static class Startup
    {
        public static void ConfigureApp(IAppBuilder appBuilder)
        {
            // Configure Web API for self-host. 
            HttpConfiguration config = new HttpConfiguration();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            appBuilder.UseWebApi(config);
        }
    }
}
```

<span data-ttu-id="18cc5-137">Per la parte dell'applicazione hello è tutto.</span><span class="sxs-lookup"><span data-stu-id="18cc5-137">That's it for hello application part.</span></span> <span data-ttu-id="18cc5-138">A questo punto, è stato configurato solo hello API Web progetto layout di base.</span><span class="sxs-lookup"><span data-stu-id="18cc5-138">At this point, we've set up just hello basic Web API project layout.</span></span> <span data-ttu-id="18cc5-139">Finora, non devono esaminare molto diverso dai progetti API Web che scritto in hello precedente o dal modello API Web di base hello.</span><span class="sxs-lookup"><span data-stu-id="18cc5-139">So far, it shouldn't look much different from Web API projects you may have written in hello past or from hello basic Web API template.</span></span> <span data-ttu-id="18cc5-140">La logica di business passa in modelli e i controller di hello come di consueto.</span><span class="sxs-lookup"><span data-stu-id="18cc5-140">Your business logic goes in hello controllers and models as usual.</span></span>

<span data-ttu-id="18cc5-141">Verrà ora illustrato come configurare l'hosting per eseguire il servizio.</span><span class="sxs-lookup"><span data-stu-id="18cc5-141">Now what do we do about hosting so that we can actually run it?</span></span>

## <a name="service-hosting"></a><span data-ttu-id="18cc5-142">Hosting del servizio</span><span class="sxs-lookup"><span data-stu-id="18cc5-142">Service hosting</span></span>
<span data-ttu-id="18cc5-143">In Service Fabric il servizio viene eseguito in un *processo host del servizio*, un file eseguibile che esegue il codice del servizio.</span><span class="sxs-lookup"><span data-stu-id="18cc5-143">In Service Fabric, your service runs in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="18cc5-144">Quando si scrive un servizio utilizzando hello affidabile API dei servizi, il progetto di servizio compila solo file eseguibile di tooan che registra il tipo di servizio e viene eseguito il codice.</span><span class="sxs-lookup"><span data-stu-id="18cc5-144">When you write a service by using hello Reliable Services API, your service project just compiles tooan executable file that registers your service type and runs your code.</span></span> <span data-ttu-id="18cc5-145">Questo vale nella maggior parte dei casi in cui si scrive un servizio in Service Fabric in .NET.</span><span class="sxs-lookup"><span data-stu-id="18cc5-145">This is true in most cases when you write a service on Service Fabric in .NET.</span></span> <span data-ttu-id="18cc5-146">Quando si apre Program.cs nel progetto di servizio senza stato hello, verrà visualizzato:</span><span class="sxs-lookup"><span data-stu-id="18cc5-146">When you open Program.cs in hello stateless service project, you should see:</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric.Services.Runtime;

internal static class Program
{
    private static void Main()
    {
        try
        {
            ServiceRuntime.RegisterServiceAsync("WebServiceType",
                context => new WebService(context)).GetAwaiter().GetResult();

            ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(WebService).Name);

            // Prevents this host process from terminating so services keeps running. 
            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

<span data-ttu-id="18cc5-147">Se che appare insolitamente come applicazione console tooa punto di ingresso hello, infatti è.</span><span class="sxs-lookup"><span data-stu-id="18cc5-147">If that looks suspiciously like hello entry point tooa console application, that's because it is.</span></span>

<span data-ttu-id="18cc5-148">Per ulteriori informazioni sugli hello processo host del servizio e la registrazione del servizio esulano dall'ambito di hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="18cc5-148">Further details about hello service host process and service registration are beyond hello scope of this article.</span></span> <span data-ttu-id="18cc5-149">Ma è importante tooknow per ora che *il codice del servizio è in esecuzione nel proprio processo*.</span><span class="sxs-lookup"><span data-stu-id="18cc5-149">But it's important tooknow for now that *your service code is running in its own process*.</span></span>

## <a name="self-host-web-api-with-an-owin-host"></a><span data-ttu-id="18cc5-150">Ospitare in modo autonomo l'API Web con self-hosting OWIN</span><span class="sxs-lookup"><span data-stu-id="18cc5-150">Self-host Web API with an OWIN host</span></span>
<span data-ttu-id="18cc5-151">Dato che il codice dell'applicazione API Web è ospitato in un processo, come associarlo di server web tooa?</span><span class="sxs-lookup"><span data-stu-id="18cc5-151">Given that your Web API application code is hosted in its own process, how do you hook it up tooa web server?</span></span> <span data-ttu-id="18cc5-152">Immettere [OWIN](http://owin.org/).</span><span class="sxs-lookup"><span data-stu-id="18cc5-152">Enter [OWIN](http://owin.org/).</span></span> <span data-ttu-id="18cc5-153">OWIN è semplicemente un contratto tra le applicazioni Web .NET e i server Web.</span><span class="sxs-lookup"><span data-stu-id="18cc5-153">OWIN is simply a contract between .NET web applications and web servers.</span></span> <span data-ttu-id="18cc5-154">In genere quando si utilizza ASP.NET (backup tooMVC 5), un'applicazione web hello è fortemente accoppiata tooIIS tramite System. Web.</span><span class="sxs-lookup"><span data-stu-id="18cc5-154">Traditionally when ASP.NET (up tooMVC 5) is used, hello web application is tightly coupled tooIIS through System.Web.</span></span> <span data-ttu-id="18cc5-155">Tuttavia, API Web implementa OWIN, pertanto è possibile scrivere un'applicazione web che viene separata dal server web hello che lo ospita.</span><span class="sxs-lookup"><span data-stu-id="18cc5-155">However, Web API implements OWIN, so you can write a web application that is decoupled from hello web server that hosts it.</span></span> <span data-ttu-id="18cc5-156">Per questo motivo è possibile usare un server Web OWIN *con self-hosting* e avviarlo nel processo.</span><span class="sxs-lookup"><span data-stu-id="18cc5-156">Because of this, you can use a *self-hosted* OWIN web server that you can start in your own process.</span></span> <span data-ttu-id="18cc5-157">Questo si adatta perfettamente con modello di hosting Service Fabric hello che appena descritti.</span><span class="sxs-lookup"><span data-stu-id="18cc5-157">This fits perfectly with hello Service Fabric hosting model we just described.</span></span>

<span data-ttu-id="18cc5-158">In questo articolo, si userà Katana come host di hello OWIN per l'applicazione Web API hello.</span><span class="sxs-lookup"><span data-stu-id="18cc5-158">In this article, we'll use Katana as hello OWIN host for hello Web API application.</span></span> <span data-ttu-id="18cc5-159">Katana è un'implementazione di host OWIN open source basata su [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) e Windows hello [API Server HTTP](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span><span class="sxs-lookup"><span data-stu-id="18cc5-159">Katana is an open-source OWIN host implementation built on [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) and hello Windows [HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="18cc5-160">ulteriori informazioni sulla Katana, andare toohello toolearn [Katana sito](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span><span class="sxs-lookup"><span data-stu-id="18cc5-160">toolearn more about Katana, go toohello [Katana site](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span></span> <span data-ttu-id="18cc5-161">Per una rapida panoramica di come toouse Katana tooself host Web API, vedere [OWIN utilizzare tooSelf Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).</span><span class="sxs-lookup"><span data-stu-id="18cc5-161">For a quick overview of how toouse Katana tooself-host Web API, see [Use OWIN tooSelf-Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).</span></span>
> 
> 

## <a name="set-up-hello-web-server"></a><span data-ttu-id="18cc5-162">Impostare i server web hello</span><span class="sxs-lookup"><span data-stu-id="18cc5-162">Set up hello web server</span></span>
<span data-ttu-id="18cc5-163">Hello affidabile API dei servizi fornisce un punto di ingresso di comunicazione in cui è possibile collegare gli stack di comunicazione che consentono agli utenti e servizio di toohello tooconnect client:</span><span class="sxs-lookup"><span data-stu-id="18cc5-163">hello Reliable Services API provides a communication entry point where you can plug in communication stacks that allow users and clients tooconnect toohello service:</span></span>

```csharp

protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}

```

<span data-ttu-id="18cc5-164">server web Hello (e qualsiasi altro stack di comunicazione che è utilizzare in futuro, ad esempio WebSocket hello) deve utilizzare hello ICommunicationListener interfaccia toointegrate correttamente con il sistema hello.</span><span class="sxs-lookup"><span data-stu-id="18cc5-164">hello web server (and any other communication stack you use in hello future, such as WebSockets) should use hello ICommunicationListener interface toointegrate correctly with hello system.</span></span> <span data-ttu-id="18cc5-165">Per motivi di Hello verranno diventano più evidenti in hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="18cc5-165">hello reasons for this will become more apparent in hello following steps.</span></span>

<span data-ttu-id="18cc5-166">Creare innanzitutto una classe denominata OwinCommunicationListener che implementa l'interfaccia ICommunicationListener:</span><span class="sxs-lookup"><span data-stu-id="18cc5-166">First, create a class called OwinCommunicationListener that implements ICommunicationListener:</span></span>

<span data-ttu-id="18cc5-167">**OwinCommunicationListener.cs**</span><span class="sxs-lookup"><span data-stu-id="18cc5-167">**OwinCommunicationListener.cs**</span></span>

```csharp
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;
using System;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        public void Abort()
        {
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
        }
    }
}
```

<span data-ttu-id="18cc5-168">interfaccia ICommunicationListener Hello fornisce tre metodi toomanage un listener di comunicazione per il servizio:</span><span class="sxs-lookup"><span data-stu-id="18cc5-168">hello ICommunicationListener interface provides three methods toomanage a communication listener for your service:</span></span>

* <span data-ttu-id="18cc5-169">*OpenAsync*.</span><span class="sxs-lookup"><span data-stu-id="18cc5-169">*OpenAsync*.</span></span> <span data-ttu-id="18cc5-170">Avviare l'ascolto delle richieste.</span><span class="sxs-lookup"><span data-stu-id="18cc5-170">Start listening for requests.</span></span>
* <span data-ttu-id="18cc5-171">*CloseAsync*.</span><span class="sxs-lookup"><span data-stu-id="18cc5-171">*CloseAsync*.</span></span> <span data-ttu-id="18cc5-172">Interrompere l'ascolto delle richieste, completare tutte le richieste in elaborazione ed eseguire l'arresto normalmente.</span><span class="sxs-lookup"><span data-stu-id="18cc5-172">Stop listening for requests, finish any in-flight requests, and shut down gracefully.</span></span>
* <span data-ttu-id="18cc5-173">*Abort*.</span><span class="sxs-lookup"><span data-stu-id="18cc5-173">*Abort*.</span></span> <span data-ttu-id="18cc5-174">Cancellare tutto ed eseguire l'arresto immediatamente.</span><span class="sxs-lookup"><span data-stu-id="18cc5-174">Cancel everything and stop immediately.</span></span>

<span data-ttu-id="18cc5-175">tooget avviato, aggiungere i membri di classe privata per il listener hello operazioni necessario toofunction.</span><span class="sxs-lookup"><span data-stu-id="18cc5-175">tooget started, add private class members for things hello listener will need toofunction.</span></span> <span data-ttu-id="18cc5-176">Questi verranno inizializzati tramite il costruttore hello e utilizzati in un secondo momento quando si configura hello URL in ascolto.</span><span class="sxs-lookup"><span data-stu-id="18cc5-176">These will be initialized through hello constructor and used later when you set up hello listening URL.</span></span>

```csharp
internal class OwinCommunicationListener : ICommunicationListener
{
    private readonly ServiceEventSource eventSource;
    private readonly Action<IAppBuilder> startup;
    private readonly ServiceContext serviceContext;
    private readonly string endpointName;
    private readonly string appRoot;

    private IDisposable webApp;
    private string publishAddress;
    private string listeningAddress;

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
        : this(startup, serviceContext, eventSource, endpointName, null)
    {
    }

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
    {
        if (startup == null)
        {
            throw new ArgumentNullException(nameof(startup));
        }

        if (serviceContext == null)
        {
            throw new ArgumentNullException(nameof(serviceContext));
        }

        if (endpointName == null)
        {
            throw new ArgumentNullException(nameof(endpointName));
        }

        if (eventSource == null)
        {
            throw new ArgumentNullException(nameof(eventSource));
        }

        this.startup = startup;
        this.serviceContext = serviceContext;
        this.endpointName = endpointName;
        this.eventSource = eventSource;
        this.appRoot = appRoot;
    }


    ...

```

## <a name="implement-openasync"></a><span data-ttu-id="18cc5-177">Implementare OpenAsync</span><span class="sxs-lookup"><span data-stu-id="18cc5-177">Implement OpenAsync</span></span>
<span data-ttu-id="18cc5-178">tooset di server web hello, è necessario due tipi di informazioni:</span><span class="sxs-lookup"><span data-stu-id="18cc5-178">tooset up hello web server, you need two pieces of information:</span></span>

* <span data-ttu-id="18cc5-179">*Un prefisso del percorso URL*.</span><span class="sxs-lookup"><span data-stu-id="18cc5-179">*A URL path prefix*.</span></span> <span data-ttu-id="18cc5-180">Anche se questo è facoltativo, è utile per si tooset questo fino a questo punto, in modo che in modo sicuro, è possibile ospitare più servizi web nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="18cc5-180">Although this is optional, it's good for you tooset this up now so that you can safely host multiple web services in your application.</span></span>
* <span data-ttu-id="18cc5-181">*Una porta*.</span><span class="sxs-lookup"><span data-stu-id="18cc5-181">*A port*.</span></span>

<span data-ttu-id="18cc5-182">Prima di ottenere una porta per il server web hello, è importante comprendere che Service Fabric fornisce un livello di applicazione che funge da buffer tra l'applicazione e il sistema operativo sottostante hello cui è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="18cc5-182">Before you get a port for hello web server, it's important that you understand that Service Fabric provides an application layer that acts as a buffer between your application and hello underlying operating system that it runs on.</span></span> <span data-ttu-id="18cc5-183">Di conseguenza, Service Fabric fornisce un modo tooconfigure *endpoint* per i servizi.</span><span class="sxs-lookup"><span data-stu-id="18cc5-183">As such, Service Fabric provides a way tooconfigure *endpoints* for your services.</span></span> <span data-ttu-id="18cc5-184">Service Fabric assicura che siano disponibili per il servizio toouse endpoint.</span><span class="sxs-lookup"><span data-stu-id="18cc5-184">Service Fabric ensures that endpoints are available for your service toouse.</span></span> <span data-ttu-id="18cc5-185">In questo modo, non è tooconfigure li manualmente in hello ambiente del sistema operativo sottostante.</span><span class="sxs-lookup"><span data-stu-id="18cc5-185">This way, you don't have tooconfigure them yourself in hello underlying OS environment.</span></span> <span data-ttu-id="18cc5-186">È facilmente possibile ospitare l'applicazione di Service Fabric in diversi ambienti senza la necessità di qualsiasi applicazione di modifiche tooyour toomake.</span><span class="sxs-lookup"><span data-stu-id="18cc5-186">You can easily host your Service Fabric application in different environments without having toomake any changes tooyour application.</span></span> <span data-ttu-id="18cc5-187">(Ad esempio, è possibile ospitare hello stessa applicazione in Azure o nel proprio Data Center.)</span><span class="sxs-lookup"><span data-stu-id="18cc5-187">(For example, you can host hello same application in Azure or in your own datacenter.)</span></span>

<span data-ttu-id="18cc5-188">Configurare un endpoint HTTP in PackageRoot\ServiceManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="18cc5-188">Configure an HTTP endpoint in PackageRoot\ServiceManifest.xml:</span></span>

```xml
<Resources>
    <Endpoints>
        <Endpoint Name="ServiceEndpoint" Type="Input" Protocol="http" Port="8281" />
    </Endpoints>
</Resources>

```

<span data-ttu-id="18cc5-189">Questo passaggio è importante perché il processo host del servizio di hello viene eseguito con credenziali limitate (servizio di rete in Windows).</span><span class="sxs-lookup"><span data-stu-id="18cc5-189">This step is important because hello service host process runs under restricted credentials (Network Service on Windows).</span></span> <span data-ttu-id="18cc5-190">Ciò significa che il servizio non disporrà di accesso tooset un endpoint HTTP autonomamente.</span><span class="sxs-lookup"><span data-stu-id="18cc5-190">This means that your service won't have access tooset up an HTTP endpoint on its own.</span></span> <span data-ttu-id="18cc5-191">Tramite la configurazione dell'endpoint hello, Service Fabric SA tooset elenco di controllo di accesso appropriato hello (ACL) per hello URL hello servizio sarà in ascolto.</span><span class="sxs-lookup"><span data-stu-id="18cc5-191">By using hello endpoint configuration, Service Fabric knows tooset up hello proper access control list (ACL) for hello URL that hello service will listen on.</span></span> <span data-ttu-id="18cc5-192">Service Fabric fornisce anche una posizione standard tooconfigure endpoint.</span><span class="sxs-lookup"><span data-stu-id="18cc5-192">Service Fabric also provides a standard place tooconfigure endpoints.</span></span>

<span data-ttu-id="18cc5-193">Una volta tornati in OwinCommunicationListener.cs, iniziare a implementare OpenAsync.</span><span class="sxs-lookup"><span data-stu-id="18cc5-193">Back in OwinCommunicationListener.cs, you can start implementing OpenAsync.</span></span> <span data-ttu-id="18cc5-194">Si tratta in cui si avvia il server di web hello.</span><span class="sxs-lookup"><span data-stu-id="18cc5-194">This is where you start hello web server.</span></span> <span data-ttu-id="18cc5-195">Innanzitutto, ottenere informazioni sull'endpoint hello e creare URL hello che resterà in ascolto il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="18cc5-195">First, get hello endpoint information and create hello URL that hello service will listen on.</span></span> <span data-ttu-id="18cc5-196">Hello URL sarà diverso a seconda se il listener hello viene utilizzato in un servizio senza stato o un servizio con stato.</span><span class="sxs-lookup"><span data-stu-id="18cc5-196">hello URL will be different depending on whether hello listener is used in a stateless service or a stateful service.</span></span> <span data-ttu-id="18cc5-197">Per un servizio con stato, il listener hello deve toocreate univoco risolverlo per ogni replica del servizio con stato resta in attesa su.</span><span class="sxs-lookup"><span data-stu-id="18cc5-197">For a stateful service, hello listener needs toocreate a unique address for every stateful service replica it listens on.</span></span> <span data-ttu-id="18cc5-198">Per i servizi senza stati, indirizzo hello può essere molto più semplice.</span><span class="sxs-lookup"><span data-stu-id="18cc5-198">For stateless services, hello address can be much simpler.</span></span> 

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
    var protocol = serviceEndpoint.Protocol;
    int port = serviceEndpoint.Port;

    if (this.serviceContext is StatefulServiceContext)
    {
        StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}{3}/{4}/{5}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/',
            statefulServiceContext.PartitionId,
            statefulServiceContext.ReplicaId,
            Guid.NewGuid());
    }
    else if (this.serviceContext is StatelessServiceContext)
    {
        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/');
    }
    else
    {
        throw new InvalidOperationException();
    }

    ...

```

<span data-ttu-id="18cc5-199">Si noti che viene usato "http://+"</span><span class="sxs-lookup"><span data-stu-id="18cc5-199">Note that "http://+" is used here.</span></span> <span data-ttu-id="18cc5-200">Si tratta di toomake assicurarsi che il server web hello è in ascolto su tutti gli indirizzi disponibili, inclusi localhost, FQDN e hello macchina IP.</span><span class="sxs-lookup"><span data-stu-id="18cc5-200">This is toomake sure that hello web server is listening on all available addresses, including localhost, FQDN, and hello machine IP.</span></span>

<span data-ttu-id="18cc5-201">Hello OpenAsync implementazione è uno dei motivi più importanti di hello motivo per cui server web hello (o qualsiasi stack di comunicazione) viene implementato come un ICommunicationListener, anziché la sola apre direttamente da `RunAsync()` nel servizio hello.</span><span class="sxs-lookup"><span data-stu-id="18cc5-201">hello OpenAsync implementation is one of hello most important reasons why hello web server (or any communication stack) is implemented as an ICommunicationListener, rather than just having it open directly from `RunAsync()` in hello service.</span></span> <span data-ttu-id="18cc5-202">valore restituito di Hello da OpenAsync è l'indirizzo hello hello server web è in ascolto.</span><span class="sxs-lookup"><span data-stu-id="18cc5-202">hello return value from OpenAsync is hello address that hello web server is listening on.</span></span> <span data-ttu-id="18cc5-203">Quando questo indirizzo viene restituito il sistema toohello, Registra indirizzo hello con servizio hello.</span><span class="sxs-lookup"><span data-stu-id="18cc5-203">When this address is returned toohello system, it registers hello address with hello service.</span></span> <span data-ttu-id="18cc5-204">Service Fabric fornisce un'API che consente ai client e altri servizi toothen chiedere per questo indirizzo dal nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="18cc5-204">Service Fabric provides an API that allows clients and other services toothen ask for this address by service name.</span></span> <span data-ttu-id="18cc5-205">Questo è importante perché l'indirizzo del servizio hello non è statico.</span><span class="sxs-lookup"><span data-stu-id="18cc5-205">This is important because hello service address is not static.</span></span> <span data-ttu-id="18cc5-206">Servizi vengono spostati nel cluster hello per scopi di bilanciamento del carico e disponibilità delle risorse.</span><span class="sxs-lookup"><span data-stu-id="18cc5-206">Services are moved around in hello cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="18cc5-207">Questo è il meccanismo hello che consente ai client hello tooresolve indirizzo per un servizio in ascolto.</span><span class="sxs-lookup"><span data-stu-id="18cc5-207">This is hello mechanism that allows clients tooresolve hello listening address for a service.</span></span>

<span data-ttu-id="18cc5-208">Tenendo in considerazione, OpenAsync avvia hello web server e restituisce indirizzo hello che è in ascolto.</span><span class="sxs-lookup"><span data-stu-id="18cc5-208">With that in mind, OpenAsync starts hello web server and returns hello address that it's listening on.</span></span> <span data-ttu-id="18cc5-209">Si noti che è in ascolto "http://+", ma prima di OpenAsync restituisce indirizzo hello, salve "+" viene sostituito con hello IP o nome di dominio completo del nodo hello che corrente.</span><span class="sxs-lookup"><span data-stu-id="18cc5-209">Note that it listens on "http://+", but before OpenAsync returns hello address, hello "+" is replaced with hello IP or FQDN of hello node it is currently on.</span></span> <span data-ttu-id="18cc5-210">indirizzo Hello restituito da questo metodo è ciò che è registrato con il sistema hello.</span><span class="sxs-lookup"><span data-stu-id="18cc5-210">hello address that is returned by this method is what's registered with hello system.</span></span> <span data-ttu-id="18cc5-211">È anche l'indirizzo visualizzato dai client e dagli altri servizi quando richiedono l'indirizzo di un servizio.</span><span class="sxs-lookup"><span data-stu-id="18cc5-211">It's also what clients and other services see when they ask for a service's address.</span></span> <span data-ttu-id="18cc5-212">Per i client toocorrectly connettersi tooit, devono disporre di un indirizzo IP o FQDN di effettivo indirizzo hello.</span><span class="sxs-lookup"><span data-stu-id="18cc5-212">For clients toocorrectly connect tooit, they need an actual IP or FQDN in hello address.</span></span>

```csharp
    ...

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    try
    {
        this.eventSource.Message("Starting web server on " + this.listeningAddress);

        this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

        this.eventSource.Message("Listening on " + this.publishAddress);

        return Task.FromResult(this.publishAddress);
    }
    catch (Exception ex)
    {
        this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

        this.StopWebServer();

        throw;
    }
}

```

<span data-ttu-id="18cc5-213">Si noti che questo riferimento di classe di avvio hello passato toohello OwinCommunicationListener nel costruttore hello.</span><span class="sxs-lookup"><span data-stu-id="18cc5-213">Note that this references hello Startup class that was passed in toohello OwinCommunicationListener in hello constructor.</span></span> <span data-ttu-id="18cc5-214">L'istanza di avvio viene usata da prova web server toobootstrap prova applicazione Web API.</span><span class="sxs-lookup"><span data-stu-id="18cc5-214">This startup instance is used by hello web server toobootstrap hello Web API application.</span></span>

<span data-ttu-id="18cc5-215">Hello `ServiceEventSource.Current.Message()` riga verrà visualizzate nella finestra di eventi di diagnostica di hello in un secondo momento, quando si esegue tooconfirm applicazione hello che il server web hello è stato avviato correttamente.</span><span class="sxs-lookup"><span data-stu-id="18cc5-215">hello `ServiceEventSource.Current.Message()` line will appear in hello Diagnostic Events window later, when you run hello application tooconfirm that hello web server has started successfully.</span></span>

## <a name="implement-closeasync-and-abort"></a><span data-ttu-id="18cc5-216">Implementare CloseAsync e Abort</span><span class="sxs-lookup"><span data-stu-id="18cc5-216">Implement CloseAsync and Abort</span></span>
<span data-ttu-id="18cc5-217">Infine, implementano sia CloseAsync e interruzione del server web di toostop hello.</span><span class="sxs-lookup"><span data-stu-id="18cc5-217">Finally, implement both CloseAsync and Abort toostop hello web server.</span></span> <span data-ttu-id="18cc5-218">server web Hello può essere arrestato eliminando l'handle del server hello durante OpenAsync è stato creato.</span><span class="sxs-lookup"><span data-stu-id="18cc5-218">hello web server can be stopped by disposing hello server handle that was created during OpenAsync.</span></span>

```csharp
public Task CloseAsync(CancellationToken cancellationToken)
{
    this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

    this.StopWebServer();

    return Task.FromResult(true);
}

public void Abort()
{
    this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

    this.StopWebServer();
}

private void StopWebServer()
{
    if (this.webApp != null)
    {
        try
        {
            this.webApp.Dispose();
        }
        catch (ObjectDisposedException)
        {
            // no-op
        }
    }
}
```

<span data-ttu-id="18cc5-219">In questo esempio di implementazione, CloseAsync sia interruzione semplicemente Arresta server web di hello.</span><span class="sxs-lookup"><span data-stu-id="18cc5-219">In this implementation example, both CloseAsync and Abort simply stop hello web server.</span></span> <span data-ttu-id="18cc5-220">È possibile scegliere tooperform un arresto del server web hello in CloseAsync più normalmente coordinato.</span><span class="sxs-lookup"><span data-stu-id="18cc5-220">You may opt tooperform a more gracefully coordinated shutdown of hello web server in CloseAsync.</span></span> <span data-ttu-id="18cc5-221">Ad esempio, arresto hello potrebbe attendere le richieste in transito toobe completato prima di restituire hello.</span><span class="sxs-lookup"><span data-stu-id="18cc5-221">For example, hello shutdown could wait for in-flight requests toobe completed before hello return.</span></span>

## <a name="start-hello-web-server"></a><span data-ttu-id="18cc5-222">Avviare il server web hello</span><span class="sxs-lookup"><span data-stu-id="18cc5-222">Start hello web server</span></span>
<span data-ttu-id="18cc5-223">È ora pronto toocreate e restituire un'istanza del server web di OwinCommunicationListener toostart hello.</span><span class="sxs-lookup"><span data-stu-id="18cc5-223">You're now ready toocreate and return an instance of OwinCommunicationListener toostart hello web server.</span></span> <span data-ttu-id="18cc5-224">Nella classe del servizio (WebService.cs) hello, eseguire l'override hello `CreateServiceInstanceListeners()` metodo:</span><span class="sxs-lookup"><span data-stu-id="18cc5-224">Back in hello Service class (WebService.cs), override hello `CreateServiceInstanceListeners()` method:</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                           .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                           .Select(endpoint => endpoint.Name);

    return endpoints.Select(endpoint => new ServiceInstanceListener(
        serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
}
```

<span data-ttu-id="18cc5-225">Questo è hello in Web API *applicazione* e hello OWIN *host* infine soddisfare.</span><span class="sxs-lookup"><span data-stu-id="18cc5-225">This is where hello Web API *application* and hello OWIN *host* finally meet.</span></span> <span data-ttu-id="18cc5-226">host Hello (OwinCommunicationListener) viene assegnato a un'istanza di hello *applicazione* (API Web) tramite hello classe di avvio.</span><span class="sxs-lookup"><span data-stu-id="18cc5-226">hello host (OwinCommunicationListener) is given an instance of hello *application* (Web API) via hello Startup class.</span></span> <span data-ttu-id="18cc5-227">Service Fabric ne gestisce quindi il ciclo di vita.</span><span class="sxs-lookup"><span data-stu-id="18cc5-227">Service Fabric then manages its lifecycle.</span></span> <span data-ttu-id="18cc5-228">Questo modello può essere seguito con qualsiasi stack di comunicazione.</span><span class="sxs-lookup"><span data-stu-id="18cc5-228">This same pattern can typically be followed with any communication stack.</span></span>

## <a name="put-it-all-together"></a><span data-ttu-id="18cc5-229">Combinare tutti gli elementi</span><span class="sxs-lookup"><span data-stu-id="18cc5-229">Put it all together</span></span>
<span data-ttu-id="18cc5-230">In questo esempio, non è necessario toodo qualsiasi elemento presente in hello `RunAsync()` (metodo), in modo che eseguono l'override può essere semplicemente rimossi.</span><span class="sxs-lookup"><span data-stu-id="18cc5-230">In this example, you don't need toodo anything in hello `RunAsync()` method, so that override can simply be removed.</span></span>

<span data-ttu-id="18cc5-231">implementazione del servizio finale Hello dovrebbe essere molto semplici.</span><span class="sxs-lookup"><span data-stu-id="18cc5-231">hello final service implementation should be very simple.</span></span> <span data-ttu-id="18cc5-232">È necessario solo listener di comunicazione toocreate hello:</span><span class="sxs-lookup"><span data-stu-id="18cc5-232">It only needs toocreate hello communication listener:</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Fabric;
using System.Fabric.Description;
using System.Linq;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace WebService
{
    internal sealed class WebService : StatelessService
    {
        public WebService(StatelessServiceContext context)
            : base(context)
        { }

        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
            var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                                   .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                                   .Select(endpoint => endpoint.Name);

            return endpoints.Select(endpoint => new ServiceInstanceListener(
                serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
        }
    }
}
```

<span data-ttu-id="18cc5-233">Hello completo `OwinCommunicationListener` classe:</span><span class="sxs-lookup"><span data-stu-id="18cc5-233">hello complete `OwinCommunicationListener` class:</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        private readonly ServiceEventSource eventSource;
        private readonly Action<IAppBuilder> startup;
        private readonly ServiceContext serviceContext;
        private readonly string endpointName;
        private readonly string appRoot;

        private IDisposable webApp;
        private string publishAddress;
        private string listeningAddress;

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
            : this(startup, serviceContext, eventSource, endpointName, null)
        {
        }

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
        {
            if (startup == null)
            {
                throw new ArgumentNullException(nameof(startup));
            }

            if (serviceContext == null)
            {
                throw new ArgumentNullException(nameof(serviceContext));
            }

            if (endpointName == null)
            {
                throw new ArgumentNullException(nameof(endpointName));
            }

            if (eventSource == null)
            {
                throw new ArgumentNullException(nameof(eventSource));
            }

            this.startup = startup;
            this.serviceContext = serviceContext;
            this.endpointName = endpointName;
            this.eventSource = eventSource;
            this.appRoot = appRoot;
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
            var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
            var protocol = serviceEndpoint.Protocol;
            int port = serviceEndpoint.Port;

            if (this.serviceContext is StatefulServiceContext)
            {
                StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}{3}/{4}/{5}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/',
                    statefulServiceContext.PartitionId,
                    statefulServiceContext.ReplicaId,
                    Guid.NewGuid());
            }
            else if (this.serviceContext is StatelessServiceContext)
            {
                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/');
            }
            else
            {
                throw new InvalidOperationException();
            }

            this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

            try
            {
                this.eventSource.Message("Starting web server on " + this.listeningAddress);

                this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

                this.eventSource.Message("Listening on " + this.publishAddress);

                return Task.FromResult(this.publishAddress);
            }
            catch (Exception ex)
            {
                this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

                this.StopWebServer();

                throw;
            }
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
            this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

            this.StopWebServer();

            return Task.FromResult(true);
        }

        public void Abort()
        {
            this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

            this.StopWebServer();
        }

        private void StopWebServer()
        {
            if (this.webApp != null)
            {
                try
                {
                    this.webApp.Dispose();
                }
                catch (ObjectDisposedException)
                {
                    // no-op
                }
            }
        }
    }
}
```

<span data-ttu-id="18cc5-234">Ora che è stato inserito tutte le parti di hello sul posto, il progetto dovrebbe essere simile una tipica applicazione Web API con punti di ingresso di API per servizi affidabili e un host OWIN.</span><span class="sxs-lookup"><span data-stu-id="18cc5-234">Now that you have put all hello pieces in place, your project should look like a typical Web API application with Reliable Services API entry points and an OWIN host.</span></span>

## <a name="run-and-connect-through-a-web-browser"></a><span data-ttu-id="18cc5-235">Esecuzione e connessione tramite un Web browser</span><span class="sxs-lookup"><span data-stu-id="18cc5-235">Run and connect through a web browser</span></span>
<span data-ttu-id="18cc5-236">Se non lo si è già fatto, [configurare l'ambiente di sviluppo](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="18cc5-236">If you haven't done so, [set up your development environment](service-fabric-get-started.md).</span></span>

<span data-ttu-id="18cc5-237">È ora possibile compilare e distribuire il servizio.</span><span class="sxs-lookup"><span data-stu-id="18cc5-237">You can now build and deploy your service.</span></span> <span data-ttu-id="18cc5-238">Premere **F5** in Visual Studio toobuild e distribuire un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="18cc5-238">Press **F5** in Visual Studio toobuild and deploy hello application.</span></span> <span data-ttu-id="18cc5-239">Nella finestra di eventi di diagnostica hello, si verrà visualizzato un messaggio che indica che il server web hello aperto su http://localhost:8281 /.</span><span class="sxs-lookup"><span data-stu-id="18cc5-239">In hello Diagnostic Events window, you should see a message that indicates that hello web server opened on http://localhost:8281/.</span></span>

> [!NOTE]
> <span data-ttu-id="18cc5-240">Se la porta hello è già stata aperta da un altro processo nel computer in uso, si venga visualizzato un errore di seguito.</span><span class="sxs-lookup"><span data-stu-id="18cc5-240">If hello port has already been opened by another process on your machine, you may see an error here.</span></span> <span data-ttu-id="18cc5-241">Ciò indica che non è possibile aprire il listener hello.</span><span class="sxs-lookup"><span data-stu-id="18cc5-241">This indicates that hello listener couldn't be opened.</span></span> <span data-ttu-id="18cc5-242">Se è questo caso di hello, provare a utilizzare una porta diversa per la configurazione di endpoint hello in ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="18cc5-242">If that's hello case, try using a different port for hello endpoint configuration in ServiceManifest.xml.</span></span>
> 
> 

<span data-ttu-id="18cc5-243">Quando è in esecuzione il servizio di hello, aprire un browser e andare troppo[http://localhost:8281, api e valori](http://localhost:8281/api/values) tootest è.</span><span class="sxs-lookup"><span data-stu-id="18cc5-243">Once hello service is running, open a browser and navigate too[http://localhost:8281/api/values](http://localhost:8281/api/values) tootest it.</span></span>

## <a name="scale-it-out"></a><span data-ttu-id="18cc5-244">Scalabilità orizzontale</span><span class="sxs-lookup"><span data-stu-id="18cc5-244">Scale it out</span></span>
<span data-ttu-id="18cc5-245">Scalabilità orizzontale di applicazioni web senza stato in genere significa aggiungere più computer e spin-up App web hello su di essi.</span><span class="sxs-lookup"><span data-stu-id="18cc5-245">Scaling out stateless web apps typically means adding more machines and spinning up hello web apps on them.</span></span> <span data-ttu-id="18cc5-246">Il motore di orchestrazione dell'infrastruttura servizio per questo scopo è ogni volta che vengono aggiunti il cluster tooa nuovi nodi.</span><span class="sxs-lookup"><span data-stu-id="18cc5-246">Service Fabric's orchestration engine can do this for you whenever new nodes are added tooa cluster.</span></span> <span data-ttu-id="18cc5-247">Quando si creano istanze di un servizio senza stato, è possibile specificare il numero di hello di istanze desiderato toocreate.</span><span class="sxs-lookup"><span data-stu-id="18cc5-247">When you create instances of a stateless service, you can specify hello number of instances you want toocreate.</span></span> <span data-ttu-id="18cc5-248">Service Fabric inserisce tale numero di istanze nei nodi cluster hello.</span><span class="sxs-lookup"><span data-stu-id="18cc5-248">Service Fabric places that number of instances on nodes in hello cluster.</span></span> <span data-ttu-id="18cc5-249">E garantisce toocreate non più di una istanza in un qualsiasi nodo.</span><span class="sxs-lookup"><span data-stu-id="18cc5-249">And it makes sure not toocreate more than one instance on any one node.</span></span> <span data-ttu-id="18cc5-250">È anche possibile indicare tooalways Service Fabric crea un'istanza in ogni nodo specificando **-1** hello conteggio delle istanze.</span><span class="sxs-lookup"><span data-stu-id="18cc5-250">You can also instruct Service Fabric tooalways create an instance on every node by specifying **-1** for hello instance count.</span></span> <span data-ttu-id="18cc5-251">In questo modo si garantisce che ogni volta che si aggiunta tooscale i nodi del cluster, un'istanza del servizio senza stato verrà creata in nuovi nodi di hello.</span><span class="sxs-lookup"><span data-stu-id="18cc5-251">This guarantees that whenever you add nodes tooscale out your cluster, an instance of your stateless service will be created on hello new nodes.</span></span> <span data-ttu-id="18cc5-252">Questo valore è una proprietà dell'istanza di servizio hello, in modo che viene impostata quando si crea un'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="18cc5-252">This value is a property of hello service instance, so it is set when you create a service instance.</span></span> <span data-ttu-id="18cc5-253">Per farlo, è possibile usare PowerShell:</span><span class="sxs-lookup"><span data-stu-id="18cc5-253">You can do this through PowerShell:</span></span>

```powershell

New-ServiceFabricService -ApplicationName "fabric:/WebServiceApplication" -ServiceName "fabric:/WebServiceApplication/WebService" -ServiceTypeName "WebServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1

```

<span data-ttu-id="18cc5-254">Questa operazione può essere effettuata anche quando si definisce un servizio predefinito in un progetto di servizio senza stato di Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="18cc5-254">You can also do this when you define a default service in a Visual Studio stateless service project:</span></span>

```xml

<DefaultServices>
  <Service Name="WebService">
    <StatelessService ServiceTypeName="WebServiceType" InstanceCount="-1">
      <SingletonPartition />
    </StatelessService>
  </Service>
</DefaultServices>

```

<span data-ttu-id="18cc5-255">Per ulteriori informazioni sull'applicazione toocreate e istanze del servizio, vedere [distribuire un'applicazione](service-fabric-deploy-remove-applications.md).</span><span class="sxs-lookup"><span data-stu-id="18cc5-255">For more information on how toocreate application and service instances, see [Deploy an application](service-fabric-deploy-remove-applications.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="18cc5-256">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="18cc5-256">Next steps</span></span>
[<span data-ttu-id="18cc5-257">Debug dell'applicazione di Service Fabric mediante Visual Studio</span><span class="sxs-lookup"><span data-stu-id="18cc5-257">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

