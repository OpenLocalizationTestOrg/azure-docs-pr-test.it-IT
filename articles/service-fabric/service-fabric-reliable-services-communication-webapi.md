---
title: Comunicazione dei servizi con l'API Web ASP.NET | Microsoft Docs
description: Informazioni dettagliate su come implementare la comunicazione dei servizi mediante l'API Web ASP.NET con self-hosting OWIN nell'API di Reliable Services.
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
ms.openlocfilehash: 73b7e1c0cb93ae7c54780a3aab837b0e5bcdb0a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-service-fabric-web-api-services-with-owin-self-hosting"></a><span data-ttu-id="48425-103">Introduzione ai servizi API Web di Service Fabric con self-hosting OWIN</span><span class="sxs-lookup"><span data-stu-id="48425-103">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>
<span data-ttu-id="48425-104">Azure Service Fabric consente di definire la modalità di comunicazione dei servizi con gli utenti e tra loro.</span><span class="sxs-lookup"><span data-stu-id="48425-104">Azure Service Fabric puts the power in your hands when you're deciding how you want your services to communicate with users and with each other.</span></span> <span data-ttu-id="48425-105">Questa esercitazione è incentrata sull'implementazione della comunicazione dei servizi mediante l'API Web ASP.NET con self-hosting OWIN (Open Web Interface for .NET) nell'API di Reliable Services di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="48425-105">This tutorial focuses on implementing service communication using ASP.NET Web API with Open Web Interface for .NET (OWIN) self-hosting in Service Fabric's Reliable Services API.</span></span> <span data-ttu-id="48425-106">Verrà illustrata approfonditamente l'API di comunicazione collegabile di Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="48425-106">We'll delve deeply into the Reliable Services pluggable communication API.</span></span> <span data-ttu-id="48425-107">Verrà anche fornito un esempio dettagliato con l'API Web per illustrare come configurare un listener di comunicazione personalizzato.</span><span class="sxs-lookup"><span data-stu-id="48425-107">We'll also use Web API in a step-by-step example to show you how to set up a custom communication listener.</span></span>

## <a name="introduction-to-web-api-in-service-fabric"></a><span data-ttu-id="48425-108">Introduzione alle API Web in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="48425-108">Introduction to Web API in Service Fabric</span></span>
<span data-ttu-id="48425-109">L'API Web ASP.NET è un diffuso e potente framework per la creazione di API HTTP in .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="48425-109">ASP.NET Web API is a popular and powerful framework for building HTTP APIs on top of the .NET Framework.</span></span> <span data-ttu-id="48425-110">Se non si ha già familiarità con il framework, per informazioni vedere l' [introduzione all'API Web 2 ASP.NET](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) .</span><span class="sxs-lookup"><span data-stu-id="48425-110">If you're not already familiar with the framework, see [Getting started with ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) to learn more.</span></span>

<span data-ttu-id="48425-111">L'API Web in Service Fabric è la stessa API Web ASP.NET già nota e apprezzata dagli utenti.</span><span class="sxs-lookup"><span data-stu-id="48425-111">Web API in Service Fabric is the same ASP.NET Web API you know and love.</span></span> <span data-ttu-id="48425-112">La differenza consiste nella modalità di *hosting* di un'applicazione API Web.</span><span class="sxs-lookup"><span data-stu-id="48425-112">The difference is in how you *host* a Web API application.</span></span> <span data-ttu-id="48425-113">Non si userà Microsoft Internet Information Services (IIS).</span><span class="sxs-lookup"><span data-stu-id="48425-113">You won't be using Microsoft Internet Information Services (IIS).</span></span> <span data-ttu-id="48425-114">Per comprendere meglio la differenza, l'argomento verrà suddiviso in due parti:</span><span class="sxs-lookup"><span data-stu-id="48425-114">To better understand the difference, let's break it into two parts:</span></span>

1. <span data-ttu-id="48425-115">L'applicazione API Web (inclusi i controller e i modelli)</span><span class="sxs-lookup"><span data-stu-id="48425-115">The Web API application (including controllers and models)</span></span>
2. <span data-ttu-id="48425-116">L'host (il server Web, in genere IIS)</span><span class="sxs-lookup"><span data-stu-id="48425-116">The host (the web server, usually IIS)</span></span>

<span data-ttu-id="48425-117">L'applicazione API Web non cambia.</span><span class="sxs-lookup"><span data-stu-id="48425-117">A Web API application itself doesn't change.</span></span> <span data-ttu-id="48425-118">Non è diversa dalle applicazioni API Web scritte in precedenza, pertanto dovrebbe essere possibile spostare semplicemente la maggior parte del codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="48425-118">It's no different from Web API applications you may have written in the past, and you should be able to simply move over most of your application code.</span></span> <span data-ttu-id="48425-119">Se si è abituati all'hosting in IIS, l'hosting dell'applicazione potrebbe tuttavia risultare leggermente diverso.</span><span class="sxs-lookup"><span data-stu-id="48425-119">But if you've been hosting on IIS, where you host the application may be a little different from what you're used to.</span></span> <span data-ttu-id="48425-120">Prima di passare all'hosting, verrà illustrata la parte più familiare: l'applicazione API Web.</span><span class="sxs-lookup"><span data-stu-id="48425-120">Before we get to the hosting part, let's start with something more familiar: the Web API application.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="48425-121">Creazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="48425-121">Create the application</span></span>
<span data-ttu-id="48425-122">Iniziare creando una nuova applicazione Service Fabric con un singolo servizio senza stato in Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="48425-122">Start by creating a new Service Fabric application with a single stateless service in Visual Studio 2015.</span></span>

<span data-ttu-id="48425-123">È disponibile un modello di Visual Studio per un servizio senza stato tramite l'API Web.</span><span class="sxs-lookup"><span data-stu-id="48425-123">A Visual Studio template for a stateless service using Web API is available to you.</span></span> <span data-ttu-id="48425-124">In questa esercitazione verrà compilato da zero un progetto API Web che genera un risultato simile a ciò che si otterrebbe selezionando tale modello.</span><span class="sxs-lookup"><span data-stu-id="48425-124">In this tutorial, we'll build a Web API project from scratch that results in what you'd get if you selected this template.</span></span>

<span data-ttu-id="48425-125">È possibile selezionare un progetto Servizio senza stato vuoto per imparare a compilare da zero un progetto API Web oppure partire da un modello API Web di servizio senza stato e seguire semplicemente la procedura.</span><span class="sxs-lookup"><span data-stu-id="48425-125">Select a blank Stateless Service project to learn how to build a Web API project from scratch, or you can start with the stateless service Web API template and simply follow along.</span></span>  

<span data-ttu-id="48425-126">Il primo passaggio consiste nell'eseguire il pull di alcuni pacchetti NuGet per l'API Web.</span><span class="sxs-lookup"><span data-stu-id="48425-126">The first step is to pull in some NuGet packages for Web API.</span></span> <span data-ttu-id="48425-127">Il pacchetto da usare è Microsoft.AspNet.WebApi.OwinSelfHost.</span><span class="sxs-lookup"><span data-stu-id="48425-127">The package we want to use is Microsoft.AspNet.WebApi.OwinSelfHost.</span></span> <span data-ttu-id="48425-128">Questo pacchetto include tutti i pacchetti di API Web necessari e i pacchetti *host*,</span><span class="sxs-lookup"><span data-stu-id="48425-128">This package includes all the necessary Web API packages and the *host* packages.</span></span> <span data-ttu-id="48425-129">che saranno importanti in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="48425-129">This will be important later.</span></span>

<span data-ttu-id="48425-130">Dopo aver installato i pacchetti, iniziare a compilare la struttura di base del progetto API Web.</span><span class="sxs-lookup"><span data-stu-id="48425-130">After the packages have been installed, you can begin building out the basic Web API project structure.</span></span> <span data-ttu-id="48425-131">Se è già stata usata un'API Web, la struttura del progetto dovrebbe avere un aspetto familiare.</span><span class="sxs-lookup"><span data-stu-id="48425-131">If you've used Web API, the project structure should look very familiar.</span></span> <span data-ttu-id="48425-132">Iniziare aggiungendo una directory `Controllers` e un semplice controller di valori:</span><span class="sxs-lookup"><span data-stu-id="48425-132">Start by adding a `Controllers` directory and a simple values controller:</span></span>

<span data-ttu-id="48425-133">**ValuesController.cs**</span><span class="sxs-lookup"><span data-stu-id="48425-133">**ValuesController.cs**</span></span>

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

<span data-ttu-id="48425-134">Aggiungere quindi una classe Startup alla radice del progetto per registrare il routing, i formattatori e le altre impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="48425-134">Next, add a Startup class at the project root to register the routing, formatters, and any other configuration setup.</span></span> <span data-ttu-id="48425-135">Si tratta inoltre della classe in cui l'API Web si collega all' *host*, come verrà illustrato più avanti.</span><span class="sxs-lookup"><span data-stu-id="48425-135">This is also where Web API plugs in to the *host*, which will be revisited again later.</span></span> 

<span data-ttu-id="48425-136">**Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="48425-136">**Startup.cs**</span></span>

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

<span data-ttu-id="48425-137">La parte relativa all'applicazione è terminata.</span><span class="sxs-lookup"><span data-stu-id="48425-137">That's it for the application part.</span></span> <span data-ttu-id="48425-138">È stato quindi impostato il layout del progetto API Web di base.</span><span class="sxs-lookup"><span data-stu-id="48425-138">At this point, we've set up just the basic Web API project layout.</span></span> <span data-ttu-id="48425-139">Questo progetto sarà simile ai progetti API Web scritti in precedenza o al modello API Web di base.</span><span class="sxs-lookup"><span data-stu-id="48425-139">So far, it shouldn't look much different from Web API projects you may have written in the past or from the basic Web API template.</span></span> <span data-ttu-id="48425-140">Come al solito, la logica di business si basa sui controller e sui modelli.</span><span class="sxs-lookup"><span data-stu-id="48425-140">Your business logic goes in the controllers and models as usual.</span></span>

<span data-ttu-id="48425-141">Verrà ora illustrato come configurare l'hosting per eseguire il servizio.</span><span class="sxs-lookup"><span data-stu-id="48425-141">Now what do we do about hosting so that we can actually run it?</span></span>

## <a name="service-hosting"></a><span data-ttu-id="48425-142">Hosting del servizio</span><span class="sxs-lookup"><span data-stu-id="48425-142">Service hosting</span></span>
<span data-ttu-id="48425-143">In Service Fabric il servizio viene eseguito in un *processo host del servizio*, un file eseguibile che esegue il codice del servizio.</span><span class="sxs-lookup"><span data-stu-id="48425-143">In Service Fabric, your service runs in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="48425-144">Quando si scrive un servizio usando l'API di Reliable Services, il progetto di servizio viene compilato solo in un file eseguibile che registra il tipo di servizio ed esegue il codice.</span><span class="sxs-lookup"><span data-stu-id="48425-144">When you write a service by using the Reliable Services API, your service project just compiles to an executable file that registers your service type and runs your code.</span></span> <span data-ttu-id="48425-145">Questo vale nella maggior parte dei casi in cui si scrive un servizio in Service Fabric in .NET.</span><span class="sxs-lookup"><span data-stu-id="48425-145">This is true in most cases when you write a service on Service Fabric in .NET.</span></span> <span data-ttu-id="48425-146">Se si apre Program.cs nel progetto di servizio senza stato, verrà visualizzato quanto segue:</span><span class="sxs-lookup"><span data-stu-id="48425-146">When you open Program.cs in the stateless service project, you should see:</span></span>

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

<span data-ttu-id="48425-147">L'aspetto potrebbe apparire simile al punto di ingresso a un'applicazione console:</span><span class="sxs-lookup"><span data-stu-id="48425-147">If that looks suspiciously like the entry point to a console application, that's because it is.</span></span>

<span data-ttu-id="48425-148">I dettagli relativi al processo host del servizio e alla registrazione del servizio non rientrano nell'ambito di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="48425-148">Further details about the service host process and service registration are beyond the scope of this article.</span></span> <span data-ttu-id="48425-149">È comunque importante sapere che *il codice del servizio è in esecuzione nel relativo processo*.</span><span class="sxs-lookup"><span data-stu-id="48425-149">But it's important to know for now that *your service code is running in its own process*.</span></span>

## <a name="self-host-web-api-with-an-owin-host"></a><span data-ttu-id="48425-150">Ospitare in modo autonomo l'API Web con self-hosting OWIN</span><span class="sxs-lookup"><span data-stu-id="48425-150">Self-host Web API with an OWIN host</span></span>
<span data-ttu-id="48425-151">Il codice dell'applicazione API Web è ospitato nel relativo processo. Verrà ora illustrato come associarlo a un server Web.</span><span class="sxs-lookup"><span data-stu-id="48425-151">Given that your Web API application code is hosted in its own process, how do you hook it up to a web server?</span></span> <span data-ttu-id="48425-152">Immettere [OWIN](http://owin.org/).</span><span class="sxs-lookup"><span data-stu-id="48425-152">Enter [OWIN](http://owin.org/).</span></span> <span data-ttu-id="48425-153">OWIN è semplicemente un contratto tra le applicazioni Web .NET e i server Web.</span><span class="sxs-lookup"><span data-stu-id="48425-153">OWIN is simply a contract between .NET web applications and web servers.</span></span> <span data-ttu-id="48425-154">Quando viene usato ASP.NET, fino a MVC 5, l'applicazione Web in genere è strettamente associata a IIS tramite System.Web.</span><span class="sxs-lookup"><span data-stu-id="48425-154">Traditionally when ASP.NET (up to MVC 5) is used, the web application is tightly coupled to IIS through System.Web.</span></span> <span data-ttu-id="48425-155">L'API Web implementa tuttavia OWIN, che consente di scrivere un'applicazione Web separata dal server Web che la ospita.</span><span class="sxs-lookup"><span data-stu-id="48425-155">However, Web API implements OWIN, so you can write a web application that is decoupled from the web server that hosts it.</span></span> <span data-ttu-id="48425-156">Per questo motivo è possibile usare un server Web OWIN *con self-hosting* e avviarlo nel processo.</span><span class="sxs-lookup"><span data-stu-id="48425-156">Because of this, you can use a *self-hosted* OWIN web server that you can start in your own process.</span></span> <span data-ttu-id="48425-157">Questo server si adatta perfettamente al modello di hosting di Service Fabric descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="48425-157">This fits perfectly with the Service Fabric hosting model we just described.</span></span>

<span data-ttu-id="48425-158">In questo articolo verrà usato Katana come host OWIN per l'applicazione API Web.</span><span class="sxs-lookup"><span data-stu-id="48425-158">In this article, we'll use Katana as the OWIN host for the Web API application.</span></span> <span data-ttu-id="48425-159">Katana è un'implementazione host OWIN open source basata su [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) e sull'[API server HTTP](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx) di Windows.</span><span class="sxs-lookup"><span data-stu-id="48425-159">Katana is an open-source OWIN host implementation built on [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) and the Windows [HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="48425-160">Per altre informazioni su Katana, visitare il [sito Katana](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span><span class="sxs-lookup"><span data-stu-id="48425-160">To learn more about Katana, go to the [Katana site](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span></span> <span data-ttu-id="48425-161">Per una rapida panoramica di come usare Katana per il self-hosting dell'API Web, vedere [Use OWIN to Self-Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api)(Uso di OWIN per il self-hosting dell'API Web ASP.NET 2).</span><span class="sxs-lookup"><span data-stu-id="48425-161">For a quick overview of how to use Katana to self-host Web API, see [Use OWIN to Self-Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).</span></span>
> 
> 

## <a name="set-up-the-web-server"></a><span data-ttu-id="48425-162">Configurare il server Web</span><span class="sxs-lookup"><span data-stu-id="48425-162">Set up the web server</span></span>
<span data-ttu-id="48425-163">L'API di Reliable Services offre un punto di ingresso di comunicazione in cui è possibile collegare gli stack di comunicazione che consentono agli utenti e ai client di connettersi al servizio:</span><span class="sxs-lookup"><span data-stu-id="48425-163">The Reliable Services API provides a communication entry point where you can plug in communication stacks that allow users and clients to connect to the service:</span></span>

```csharp

protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}

```

<span data-ttu-id="48425-164">Il server Web e gli eventuali stack di comunicazione da usare in futuro, ad esempio WebSocket, devono usare l'interfaccia ICommunicationListener per la corretta integrazione con il sistema.</span><span class="sxs-lookup"><span data-stu-id="48425-164">The web server (and any other communication stack you use in the future, such as WebSockets) should use the ICommunicationListener interface to integrate correctly with the system.</span></span> <span data-ttu-id="48425-165">I motivi verranno illustrati nei passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="48425-165">The reasons for this will become more apparent in the following steps.</span></span>

<span data-ttu-id="48425-166">Creare innanzitutto una classe denominata OwinCommunicationListener che implementa l'interfaccia ICommunicationListener:</span><span class="sxs-lookup"><span data-stu-id="48425-166">First, create a class called OwinCommunicationListener that implements ICommunicationListener:</span></span>

<span data-ttu-id="48425-167">**OwinCommunicationListener.cs**</span><span class="sxs-lookup"><span data-stu-id="48425-167">**OwinCommunicationListener.cs**</span></span>

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

<span data-ttu-id="48425-168">L'interfaccia ICommunicationListener fornisce tre metodi per gestire un listener di comunicazione per il servizio:</span><span class="sxs-lookup"><span data-stu-id="48425-168">The ICommunicationListener interface provides three methods to manage a communication listener for your service:</span></span>

* <span data-ttu-id="48425-169">*OpenAsync*.</span><span class="sxs-lookup"><span data-stu-id="48425-169">*OpenAsync*.</span></span> <span data-ttu-id="48425-170">Avviare l'ascolto delle richieste.</span><span class="sxs-lookup"><span data-stu-id="48425-170">Start listening for requests.</span></span>
* <span data-ttu-id="48425-171">*CloseAsync*.</span><span class="sxs-lookup"><span data-stu-id="48425-171">*CloseAsync*.</span></span> <span data-ttu-id="48425-172">Interrompere l'ascolto delle richieste, completare tutte le richieste in elaborazione ed eseguire l'arresto normalmente.</span><span class="sxs-lookup"><span data-stu-id="48425-172">Stop listening for requests, finish any in-flight requests, and shut down gracefully.</span></span>
* <span data-ttu-id="48425-173">*Abort*.</span><span class="sxs-lookup"><span data-stu-id="48425-173">*Abort*.</span></span> <span data-ttu-id="48425-174">Cancellare tutto ed eseguire l'arresto immediatamente.</span><span class="sxs-lookup"><span data-stu-id="48425-174">Cancel everything and stop immediately.</span></span>

<span data-ttu-id="48425-175">Per iniziare, aggiungere membri di classe privata per gli elementi per cui il listener dovrà funzionare.</span><span class="sxs-lookup"><span data-stu-id="48425-175">To get started, add private class members for things the listener will need to function.</span></span> <span data-ttu-id="48425-176">Questi elementi verranno inizializzati tramite il costruttore e verranno usati in seguito durante la configurazione dell'URL di ascolto.</span><span class="sxs-lookup"><span data-stu-id="48425-176">These will be initialized through the constructor and used later when you set up the listening URL.</span></span>

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

## <a name="implement-openasync"></a><span data-ttu-id="48425-177">Implementare OpenAsync</span><span class="sxs-lookup"><span data-stu-id="48425-177">Implement OpenAsync</span></span>
<span data-ttu-id="48425-178">Per configurare il server Web, sono necessarie due informazioni:</span><span class="sxs-lookup"><span data-stu-id="48425-178">To set up the web server, you need two pieces of information:</span></span>

* <span data-ttu-id="48425-179">*Un prefisso del percorso URL*.</span><span class="sxs-lookup"><span data-stu-id="48425-179">*A URL path prefix*.</span></span> <span data-ttu-id="48425-180">Sebbene sia facoltativo, è consigliabile configurarlo ora per poter ospitare in modo sicuro più servizi Web nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="48425-180">Although this is optional, it's good for you to set this up now so that you can safely host multiple web services in your application.</span></span>
* <span data-ttu-id="48425-181">*Una porta*.</span><span class="sxs-lookup"><span data-stu-id="48425-181">*A port*.</span></span>

<span data-ttu-id="48425-182">Prima di ottenere una porta per il server Web, è importante comprendere che Service Fabric offre un livello di applicazione che funge da buffer tra l'applicazione e il sistema operativo sottostante in cui è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="48425-182">Before you get a port for the web server, it's important that you understand that Service Fabric provides an application layer that acts as a buffer between your application and the underlying operating system that it runs on.</span></span> <span data-ttu-id="48425-183">Service Fabric consente pertanto di configurare *endpoint* per i servizi.</span><span class="sxs-lookup"><span data-stu-id="48425-183">As such, Service Fabric provides a way to configure *endpoints* for your services.</span></span> <span data-ttu-id="48425-184">Service Fabric assicura che gli endpoint siano disponibili per l'uso da parte del servizio.</span><span class="sxs-lookup"><span data-stu-id="48425-184">Service Fabric ensures that endpoints are available for your service to use.</span></span> <span data-ttu-id="48425-185">In questo modo non è necessario configurarli manualmente nell'ambiente del sistema operativo sottostante.</span><span class="sxs-lookup"><span data-stu-id="48425-185">This way, you don't have to configure them yourself in the underlying OS environment.</span></span> <span data-ttu-id="48425-186">È possibile ospitare facilmente l'applicazione di Service Fabric in ambienti diversi senza dover apportare modifiche all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="48425-186">You can easily host your Service Fabric application in different environments without having to make any changes to your application.</span></span> <span data-ttu-id="48425-187">È possibile ad esempio ospitare la stessa applicazione in Azure o nel proprio data center.</span><span class="sxs-lookup"><span data-stu-id="48425-187">(For example, you can host the same application in Azure or in your own datacenter.)</span></span>

<span data-ttu-id="48425-188">Configurare un endpoint HTTP in PackageRoot\ServiceManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="48425-188">Configure an HTTP endpoint in PackageRoot\ServiceManifest.xml:</span></span>

```xml
<Resources>
    <Endpoints>
        <Endpoint Name="ServiceEndpoint" Type="Input" Protocol="http" Port="8281" />
    </Endpoints>
</Resources>

```

<span data-ttu-id="48425-189">Questo passaggio è importante perché il processo host del servizio viene eseguito con credenziali con restrizioni (servizio di rete in Windows).</span><span class="sxs-lookup"><span data-stu-id="48425-189">This step is important because the service host process runs under restricted credentials (Network Service on Windows).</span></span> <span data-ttu-id="48425-190">Il servizio non avrà quindi l'autorizzazione necessaria per configurare un endpoint HTTP in modo autonomo.</span><span class="sxs-lookup"><span data-stu-id="48425-190">This means that your service won't have access to set up an HTTP endpoint on its own.</span></span> <span data-ttu-id="48425-191">Usando la configurazione dell'endpoint, Service Fabric imposta l'elenco di controllo di accesso (ACL) appropriato per l'URL su cui il servizio rimarrà in ascolto.</span><span class="sxs-lookup"><span data-stu-id="48425-191">By using the endpoint configuration, Service Fabric knows to set up the proper access control list (ACL) for the URL that the service will listen on.</span></span> <span data-ttu-id="48425-192">Service Fabric offre anche una posizione standard per la configurazione degli endpoint.</span><span class="sxs-lookup"><span data-stu-id="48425-192">Service Fabric also provides a standard place to configure endpoints.</span></span>

<span data-ttu-id="48425-193">Una volta tornati in OwinCommunicationListener.cs, iniziare a implementare OpenAsync.</span><span class="sxs-lookup"><span data-stu-id="48425-193">Back in OwinCommunicationListener.cs, you can start implementing OpenAsync.</span></span> <span data-ttu-id="48425-194">Da qui si avvia il server Web.</span><span class="sxs-lookup"><span data-stu-id="48425-194">This is where you start the web server.</span></span> <span data-ttu-id="48425-195">Innanzitutto, ottenere le informazioni sull'endpoint e creare l'URL su cui il servizio rimarrà in ascolto.</span><span class="sxs-lookup"><span data-stu-id="48425-195">First, get the endpoint information and create the URL that the service will listen on.</span></span> <span data-ttu-id="48425-196">L'URL sarà diverso a seconda che il listener venga usato in un servizio senza stato o in un servizio con stato.</span><span class="sxs-lookup"><span data-stu-id="48425-196">The URL will be different depending on whether the listener is used in a stateless service or a stateful service.</span></span> <span data-ttu-id="48425-197">Per un servizio con stato, il listener deve creare un indirizzo univoco per ogni replica del servizio con stato di cui è in ascolto.</span><span class="sxs-lookup"><span data-stu-id="48425-197">For a stateful service, the listener needs to create a unique address for every stateful service replica it listens on.</span></span> <span data-ttu-id="48425-198">Per un servizio senza stato, l'indirizzo può essere molto più semplice.</span><span class="sxs-lookup"><span data-stu-id="48425-198">For stateless services, the address can be much simpler.</span></span> 

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

<span data-ttu-id="48425-199">Si noti che viene usato "http://+"</span><span class="sxs-lookup"><span data-stu-id="48425-199">Note that "http://+" is used here.</span></span> <span data-ttu-id="48425-200">per assicurarsi che il server Web sia in ascolto su tutti gli indirizzi disponibili, tra cui il localhost, il nome di dominio completo e l'IP del computer.</span><span class="sxs-lookup"><span data-stu-id="48425-200">This is to make sure that the web server is listening on all available addresses, including localhost, FQDN, and the machine IP.</span></span>

<span data-ttu-id="48425-201">L'implementazione di OpenAsync è uno dei principali motivi per cui il server Web (o qualsiasi stack di comunicazione) viene implementato come interfaccia ICommunicationListener anziché essere aperto direttamente da `RunAsync()` nel servizio.</span><span class="sxs-lookup"><span data-stu-id="48425-201">The OpenAsync implementation is one of the most important reasons why the web server (or any communication stack) is implemented as an ICommunicationListener, rather than just having it open directly from `RunAsync()` in the service.</span></span> <span data-ttu-id="48425-202">Il valore restituito da OpenAsync è l'indirizzo su cui è in ascolto il server Web.</span><span class="sxs-lookup"><span data-stu-id="48425-202">The return value from OpenAsync is the address that the web server is listening on.</span></span> <span data-ttu-id="48425-203">Quando questo indirizzo viene restituito al sistema, registra l'indirizzo con il servizio.</span><span class="sxs-lookup"><span data-stu-id="48425-203">When this address is returned to the system, it registers the address with the service.</span></span> <span data-ttu-id="48425-204">L'API di Service Fabric consente ai client e ad altri servizi di richiedere questo indirizzo in base al nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="48425-204">Service Fabric provides an API that allows clients and other services to then ask for this address by service name.</span></span> <span data-ttu-id="48425-205">Questo aspetto è importante perché l'indirizzo del servizio non è statico.</span><span class="sxs-lookup"><span data-stu-id="48425-205">This is important because the service address is not static.</span></span> <span data-ttu-id="48425-206">I servizi vengono spostati nel cluster ai fini del bilanciamento del carico e della disponibilità delle risorse.</span><span class="sxs-lookup"><span data-stu-id="48425-206">Services are moved around in the cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="48425-207">Questo meccanismo consente ai client di risolvere l'indirizzo di ascolto per un servizio.</span><span class="sxs-lookup"><span data-stu-id="48425-207">This is the mechanism that allows clients to resolve the listening address for a service.</span></span>

<span data-ttu-id="48425-208">Tenendo presente questo aspetto, OpenAsync avvia il server Web e restituisce l'indirizzo su cui è in ascolto.</span><span class="sxs-lookup"><span data-stu-id="48425-208">With that in mind, OpenAsync starts the web server and returns the address that it's listening on.</span></span> <span data-ttu-id="48425-209">Si noti che è in ascolto su "http://+", ma prima che OpenAsync restituisca l'indirizzo, il "+" viene sostituito con l'IP o con il nome di dominio completo del nodo corrente.</span><span class="sxs-lookup"><span data-stu-id="48425-209">Note that it listens on "http://+", but before OpenAsync returns the address, the "+" is replaced with the IP or FQDN of the node it is currently on.</span></span> <span data-ttu-id="48425-210">L'indirizzo restituito da questo metodo è quello registrato con il sistema.</span><span class="sxs-lookup"><span data-stu-id="48425-210">The address that is returned by this method is what's registered with the system.</span></span> <span data-ttu-id="48425-211">È anche l'indirizzo visualizzato dai client e dagli altri servizi quando richiedono l'indirizzo di un servizio.</span><span class="sxs-lookup"><span data-stu-id="48425-211">It's also what clients and other services see when they ask for a service's address.</span></span> <span data-ttu-id="48425-212">Per una corretta connessione dei client, è necessario un IP o un nome di dominio completo effettivo nell'indirizzo.</span><span class="sxs-lookup"><span data-stu-id="48425-212">For clients to correctly connect to it, they need an actual IP or FQDN in the address.</span></span>

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
        this.eventSource.Message("Web server failed to open endpoint {0}. {1}", this.endpointName, ex.ToString());

        this.StopWebServer();

        throw;
    }
}

```

<span data-ttu-id="48425-213">Si noti che fa riferimento alla classe Startup passata all'oggetto OwinCommunicationListener nel costruttore.</span><span class="sxs-lookup"><span data-stu-id="48425-213">Note that this references the Startup class that was passed in to the OwinCommunicationListener in the constructor.</span></span> <span data-ttu-id="48425-214">Questa istanza di Startup viene usata dal server Web per avviare l'applicazione API Web.</span><span class="sxs-lookup"><span data-stu-id="48425-214">This startup instance is used by the web server to bootstrap the Web API application.</span></span>

<span data-ttu-id="48425-215">Durante l'esecuzione dell'applicazione verrà visualizzata la riga `ServiceEventSource.Current.Message()` nella finestra degli eventi di diagnostica per confermare che il server Web è stato avviato correttamente.</span><span class="sxs-lookup"><span data-stu-id="48425-215">The `ServiceEventSource.Current.Message()` line will appear in the Diagnostic Events window later, when you run the application to confirm that the web server has started successfully.</span></span>

## <a name="implement-closeasync-and-abort"></a><span data-ttu-id="48425-216">Implementare CloseAsync e Abort</span><span class="sxs-lookup"><span data-stu-id="48425-216">Implement CloseAsync and Abort</span></span>
<span data-ttu-id="48425-217">Implementare infine CloseAsync e Abort per arrestare il server Web.</span><span class="sxs-lookup"><span data-stu-id="48425-217">Finally, implement both CloseAsync and Abort to stop the web server.</span></span> <span data-ttu-id="48425-218">Il server Web può essere arrestato eliminando l'handle del server creato durante OpenAsync.</span><span class="sxs-lookup"><span data-stu-id="48425-218">The web server can be stopped by disposing the server handle that was created during OpenAsync.</span></span>

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

<span data-ttu-id="48425-219">In questa implementazione di esempio CloseAsync e Abort consentono di arrestare semplicemente il server Web.</span><span class="sxs-lookup"><span data-stu-id="48425-219">In this implementation example, both CloseAsync and Abort simply stop the web server.</span></span> <span data-ttu-id="48425-220">È possibile scegliere di eseguire normalmente un arresto coordinato del server Web in CloseAsync.</span><span class="sxs-lookup"><span data-stu-id="48425-220">You may opt to perform a more gracefully coordinated shutdown of the web server in CloseAsync.</span></span> <span data-ttu-id="48425-221">L'arresto potrebbe ad esempio attendere il completamento delle richieste in elaborazione prima di restituire il valore.</span><span class="sxs-lookup"><span data-stu-id="48425-221">For example, the shutdown could wait for in-flight requests to be completed before the return.</span></span>

## <a name="start-the-web-server"></a><span data-ttu-id="48425-222">Avviare il server Web</span><span class="sxs-lookup"><span data-stu-id="48425-222">Start the web server</span></span>
<span data-ttu-id="48425-223">È ora possibile creare e restituire un'istanza di OwinCommunicationListener per avviare il server Web.</span><span class="sxs-lookup"><span data-stu-id="48425-223">You're now ready to create and return an instance of OwinCommunicationListener to start the web server.</span></span> <span data-ttu-id="48425-224">Nella classe del servizio WebService.cs eseguire l'override del metodo `CreateServiceInstanceListeners()`:</span><span class="sxs-lookup"><span data-stu-id="48425-224">Back in the Service class (WebService.cs), override the `CreateServiceInstanceListeners()` method:</span></span>

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

<span data-ttu-id="48425-225">Qui si riuniscono, infine, l'*applicazione* API Web e l'*host* OWIN.</span><span class="sxs-lookup"><span data-stu-id="48425-225">This is where the Web API *application* and the OWIN *host* finally meet.</span></span> <span data-ttu-id="48425-226">All'host OwinCommunicationListener viene assegnata un'istanza dell' *applicazione* , ovvero l'API Web tramite la classe Startup.</span><span class="sxs-lookup"><span data-stu-id="48425-226">The host (OwinCommunicationListener) is given an instance of the *application* (Web API) via the Startup class.</span></span> <span data-ttu-id="48425-227">Service Fabric ne gestisce quindi il ciclo di vita.</span><span class="sxs-lookup"><span data-stu-id="48425-227">Service Fabric then manages its lifecycle.</span></span> <span data-ttu-id="48425-228">Questo modello può essere seguito con qualsiasi stack di comunicazione.</span><span class="sxs-lookup"><span data-stu-id="48425-228">This same pattern can typically be followed with any communication stack.</span></span>

## <a name="put-it-all-together"></a><span data-ttu-id="48425-229">Combinare tutti gli elementi</span><span class="sxs-lookup"><span data-stu-id="48425-229">Put it all together</span></span>
<span data-ttu-id="48425-230">In questo esempio non è necessario eseguire alcuna operazione nel metodo `RunAsync()` , quindi l'override può essere semplicemente rimosso.</span><span class="sxs-lookup"><span data-stu-id="48425-230">In this example, you don't need to do anything in the `RunAsync()` method, so that override can simply be removed.</span></span>

<span data-ttu-id="48425-231">L'implementazione del servizio finale sarà molto semplice.</span><span class="sxs-lookup"><span data-stu-id="48425-231">The final service implementation should be very simple.</span></span> <span data-ttu-id="48425-232">È necessario solo creare il listener di comunicazione:</span><span class="sxs-lookup"><span data-stu-id="48425-232">It only needs to create the communication listener:</span></span>

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

<span data-ttu-id="48425-233">La classe `OwinCommunicationListener` completa:</span><span class="sxs-lookup"><span data-stu-id="48425-233">The complete `OwinCommunicationListener` class:</span></span>

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
                this.eventSource.Message("Web server failed to open endpoint {0}. {1}", this.endpointName, ex.ToString());

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

<span data-ttu-id="48425-234">Dopo che tutti gli elementi necessari sono pronti, il progetto sarà simile a una tipica applicazione API Web con i punti di ingresso dell'API di Reliable Services e un host OWIN.</span><span class="sxs-lookup"><span data-stu-id="48425-234">Now that you have put all the pieces in place, your project should look like a typical Web API application with Reliable Services API entry points and an OWIN host.</span></span>

## <a name="run-and-connect-through-a-web-browser"></a><span data-ttu-id="48425-235">Esecuzione e connessione tramite un Web browser</span><span class="sxs-lookup"><span data-stu-id="48425-235">Run and connect through a web browser</span></span>
<span data-ttu-id="48425-236">Se non lo si è già fatto, [configurare l'ambiente di sviluppo](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="48425-236">If you haven't done so, [set up your development environment](service-fabric-get-started.md).</span></span>

<span data-ttu-id="48425-237">È ora possibile compilare e distribuire il servizio.</span><span class="sxs-lookup"><span data-stu-id="48425-237">You can now build and deploy your service.</span></span> <span data-ttu-id="48425-238">Premere **F5** in Visual Studio per compilare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="48425-238">Press **F5** in Visual Studio to build and deploy the application.</span></span> <span data-ttu-id="48425-239">Nella finestra degli eventi di diagnostica si dovrebbe visualizzare un messaggio nel quale viene indicato che il server Web è aperto in http://localhost:8281/.</span><span class="sxs-lookup"><span data-stu-id="48425-239">In the Diagnostic Events window, you should see a message that indicates that the web server opened on http://localhost:8281/.</span></span>

> [!NOTE]
> <span data-ttu-id="48425-240">Se la porta è già stata aperta da un altro processo nel computer, è possibile che venga visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="48425-240">If the port has already been opened by another process on your machine, you may see an error here.</span></span> <span data-ttu-id="48425-241">Questo messaggio di errore indica che il listener non può essere aperto.</span><span class="sxs-lookup"><span data-stu-id="48425-241">This indicates that the listener couldn't be opened.</span></span> <span data-ttu-id="48425-242">In questo caso provare a usare una porta diversa nella configurazione dell'endpoint in ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="48425-242">If that's the case, try using a different port for the endpoint configuration in ServiceManifest.xml.</span></span>
> 
> 

<span data-ttu-id="48425-243">Quando il servizio è in esecuzione, aprire un browser e passare a [http://localhost:8281/api/values](http://localhost:8281/api/values) per testarlo.</span><span class="sxs-lookup"><span data-stu-id="48425-243">Once the service is running, open a browser and navigate to [http://localhost:8281/api/values](http://localhost:8281/api/values) to test it.</span></span>

## <a name="scale-it-out"></a><span data-ttu-id="48425-244">Scalabilità orizzontale</span><span class="sxs-lookup"><span data-stu-id="48425-244">Scale it out</span></span>
<span data-ttu-id="48425-245">Scalare orizzontalmente app Web senza stato in genere significa aggiungere più macchine e attivare in esse le applicazioni Web.</span><span class="sxs-lookup"><span data-stu-id="48425-245">Scaling out stateless web apps typically means adding more machines and spinning up the web apps on them.</span></span> <span data-ttu-id="48425-246">Il motore di orchestrazione di Service Fabric è in grado di farlo automaticamente ogni volta che vengono aggiunti nuovi nodi a un cluster.</span><span class="sxs-lookup"><span data-stu-id="48425-246">Service Fabric's orchestration engine can do this for you whenever new nodes are added to a cluster.</span></span> <span data-ttu-id="48425-247">Durante la creazione di istanze di un servizio senza stato, specificare il numero di istanze che si vuole creare.</span><span class="sxs-lookup"><span data-stu-id="48425-247">When you create instances of a stateless service, you can specify the number of instances you want to create.</span></span> <span data-ttu-id="48425-248">Service Fabric inserisce il numero di istanze specificato nei nodi del cluster</span><span class="sxs-lookup"><span data-stu-id="48425-248">Service Fabric places that number of instances on nodes in the cluster.</span></span> <span data-ttu-id="48425-249">e si assicura che non venga creata più di un'istanza in ciascun nodo.</span><span class="sxs-lookup"><span data-stu-id="48425-249">And it makes sure not to create more than one instance on any one node.</span></span> <span data-ttu-id="48425-250">È anche possibile impostare Service Fabric in modo che crei un'istanza in ogni nodo specificando **-1** per il numero di istanze.</span><span class="sxs-lookup"><span data-stu-id="48425-250">You can also instruct Service Fabric to always create an instance on every node by specifying **-1** for the instance count.</span></span> <span data-ttu-id="48425-251">In questo modo si garantisce che ogni volta che si aggiungono nodi per scalare orizzontalmente il cluster, nei nuovi nodi verrà creata un'istanza del servizio senza stato.</span><span class="sxs-lookup"><span data-stu-id="48425-251">This guarantees that whenever you add nodes to scale out your cluster, an instance of your stateless service will be created on the new nodes.</span></span> <span data-ttu-id="48425-252">Questo valore è una proprietà dell'istanza del servizio, pertanto viene impostato quando si crea un'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="48425-252">This value is a property of the service instance, so it is set when you create a service instance.</span></span> <span data-ttu-id="48425-253">Per farlo, è possibile usare PowerShell:</span><span class="sxs-lookup"><span data-stu-id="48425-253">You can do this through PowerShell:</span></span>

```powershell

New-ServiceFabricService -ApplicationName "fabric:/WebServiceApplication" -ServiceName "fabric:/WebServiceApplication/WebService" -ServiceTypeName "WebServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1

```

<span data-ttu-id="48425-254">Questa operazione può essere effettuata anche quando si definisce un servizio predefinito in un progetto di servizio senza stato di Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="48425-254">You can also do this when you define a default service in a Visual Studio stateless service project:</span></span>

```xml

<DefaultServices>
  <Service Name="WebService">
    <StatelessService ServiceTypeName="WebServiceType" InstanceCount="-1">
      <SingletonPartition />
    </StatelessService>
  </Service>
</DefaultServices>

```

<span data-ttu-id="48425-255">Per altre informazioni sulla creazione di istanze di applicazioni e di servizi, vedere [Distribuire un'applicazione](service-fabric-deploy-remove-applications.md).</span><span class="sxs-lookup"><span data-stu-id="48425-255">For more information on how to create application and service instances, see [Deploy an application](service-fabric-deploy-remove-applications.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="48425-256">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="48425-256">Next steps</span></span>
[<span data-ttu-id="48425-257">Debug dell'applicazione di Service Fabric mediante Visual Studio</span><span class="sxs-lookup"><span data-stu-id="48425-257">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

