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
# <a name="get-started-service-fabric-web-api-services-with-owin-self-hosting"></a>Introduzione ai servizi API Web di Service Fabric con self-hosting OWIN
Azure Service Fabric pone power hello in pratiche per decidere come si desidera toocommunicate i servizi con utenti e tra loro. Questa esercitazione è incentrata sull'implementazione della comunicazione dei servizi mediante l'API Web ASP.NET con self-hosting OWIN (Open Web Interface for .NET) nell'API di Reliable Services di Service Fabric. Approfondiremo eccessivamente hello comunicazione modulare di servizi affidabili API. Si userà API Web in un esempio dettagliato di tooshow è come tooset di un listener personalizzate di comunicazione.

## <a name="introduction-tooweb-api-in-service-fabric"></a>Introduzione tooWeb API in Service Fabric
API Web ASP.NET è un framework comune e potente per la compilazione di APIs HTTP su hello .NET Framework. Se non si ha già familiarità con framework hello, vedere [Introduzione a ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) toolearn altre.

API Web Service Fabric è hello stessa noto e apprezzato di API Web ASP.NET. Hello differenza consiste nella procedura si *host* un'applicazione Web API. Non si userà Microsoft Internet Information Services (IIS). toobetter comprendere la differenza hello, è possibile suddividerla in due parti:

1. applicazione Web API Hello (inclusi i controller e i modelli)
2. host Hello (hello web server IIS in genere)

L'applicazione API Web non cambia. Non diverse dalle applicazioni Web API che scritto in hello precedente e dovrebbe essere in grado di toosimply sposta sulla maggior parte del codice dell'applicazione. Ma se è stata hosting in IIS, in cui ospitare un'applicazione hello potrebbe essere leggermente diverso da quello che si sta per. Prima di passare toohello hosting parte, iniziamo con qualcosa di più familiari: hello applicazione API Web.

## <a name="create-hello-application"></a>Creare un'applicazione hello
Iniziare creando una nuova applicazione Service Fabric con un singolo servizio senza stato in Visual Studio 2015.

Un modello di Visual Studio per un servizio senza stato mediante API Web è tooyou disponibili. In questa esercitazione verrà compilato da zero un progetto API Web che genera un risultato simile a ciò che si otterrebbe selezionando tale modello.

Selezionare un progetto di servizio senza stato vuoto toolearn come toobuild un progetto di API Web da zero, oppure è possibile iniziare con il servizio senza stato hello modello API Web e semplicemente seguire la procedura.  

primo passaggio Hello è toopull in alcuni pacchetti NuGet per l'API Web. pacchetto di Hello desideriamo toouse è Microsoft.AspNet.WebApi.OwinSelfHost. Questo pacchetto include tutti i pacchetti hello necessari API Web e hello *host* pacchetti. che saranno importanti in un secondo momento.

Dopo l'installazione di pacchetti hello, è possibile iniziare a costruire la struttura del progetto API Web basic hello. Se è stata usata l'API Web, struttura del progetto hello dovrebbe essere molto familiare. Iniziare aggiungendo una directory `Controllers` e un semplice controller di valori:

**ValuesController.cs**

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

Successivamente, aggiungere una classe di avvio in hello progetto radice tooregister hello routing formattatori e altre impostazioni di configurazione. Si tratta di API Web in cui inserisce toohello *host*, che sarà possibile accedere più tardi. 

**Startup.cs**

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

Per la parte dell'applicazione hello è tutto. A questo punto, è stato configurato solo hello API Web progetto layout di base. Finora, non devono esaminare molto diverso dai progetti API Web che scritto in hello precedente o dal modello API Web di base hello. La logica di business passa in modelli e i controller di hello come di consueto.

Verrà ora illustrato come configurare l'hosting per eseguire il servizio.

## <a name="service-hosting"></a>Hosting del servizio
In Service Fabric il servizio viene eseguito in un *processo host del servizio*, un file eseguibile che esegue il codice del servizio. Quando si scrive un servizio utilizzando hello affidabile API dei servizi, il progetto di servizio compila solo file eseguibile di tooan che registra il tipo di servizio e viene eseguito il codice. Questo vale nella maggior parte dei casi in cui si scrive un servizio in Service Fabric in .NET. Quando si apre Program.cs nel progetto di servizio senza stato hello, verrà visualizzato:

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

Se che appare insolitamente come applicazione console tooa punto di ingresso hello, infatti è.

Per ulteriori informazioni sugli hello processo host del servizio e la registrazione del servizio esulano dall'ambito di hello di questo articolo. Ma è importante tooknow per ora che *il codice del servizio è in esecuzione nel proprio processo*.

## <a name="self-host-web-api-with-an-owin-host"></a>Ospitare in modo autonomo l'API Web con self-hosting OWIN
Dato che il codice dell'applicazione API Web è ospitato in un processo, come associarlo di server web tooa? Immettere [OWIN](http://owin.org/). OWIN è semplicemente un contratto tra le applicazioni Web .NET e i server Web. In genere quando si utilizza ASP.NET (backup tooMVC 5), un'applicazione web hello è fortemente accoppiata tooIIS tramite System. Web. Tuttavia, API Web implementa OWIN, pertanto è possibile scrivere un'applicazione web che viene separata dal server web hello che lo ospita. Per questo motivo è possibile usare un server Web OWIN *con self-hosting* e avviarlo nel processo. Questo si adatta perfettamente con modello di hosting Service Fabric hello che appena descritti.

In questo articolo, si userà Katana come host di hello OWIN per l'applicazione Web API hello. Katana è un'implementazione di host OWIN open source basata su [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) e Windows hello [API Server HTTP](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).

> [!NOTE]
> ulteriori informazioni sulla Katana, andare toohello toolearn [Katana sito](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana). Per una rapida panoramica di come toouse Katana tooself host Web API, vedere [OWIN utilizzare tooSelf Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).
> 
> 

## <a name="set-up-hello-web-server"></a>Impostare i server web hello
Hello affidabile API dei servizi fornisce un punto di ingresso di comunicazione in cui è possibile collegare gli stack di comunicazione che consentono agli utenti e servizio di toohello tooconnect client:

```csharp

protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}

```

server web Hello (e qualsiasi altro stack di comunicazione che è utilizzare in futuro, ad esempio WebSocket hello) deve utilizzare hello ICommunicationListener interfaccia toointegrate correttamente con il sistema hello. Per motivi di Hello verranno diventano più evidenti in hello alla procedura seguente.

Creare innanzitutto una classe denominata OwinCommunicationListener che implementa l'interfaccia ICommunicationListener:

**OwinCommunicationListener.cs**

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

interfaccia ICommunicationListener Hello fornisce tre metodi toomanage un listener di comunicazione per il servizio:

* *OpenAsync*. Avviare l'ascolto delle richieste.
* *CloseAsync*. Interrompere l'ascolto delle richieste, completare tutte le richieste in elaborazione ed eseguire l'arresto normalmente.
* *Abort*. Cancellare tutto ed eseguire l'arresto immediatamente.

tooget avviato, aggiungere i membri di classe privata per il listener hello operazioni necessario toofunction. Questi verranno inizializzati tramite il costruttore hello e utilizzati in un secondo momento quando si configura hello URL in ascolto.

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

## <a name="implement-openasync"></a>Implementare OpenAsync
tooset di server web hello, è necessario due tipi di informazioni:

* *Un prefisso del percorso URL*. Anche se questo è facoltativo, è utile per si tooset questo fino a questo punto, in modo che in modo sicuro, è possibile ospitare più servizi web nell'applicazione.
* *Una porta*.

Prima di ottenere una porta per il server web hello, è importante comprendere che Service Fabric fornisce un livello di applicazione che funge da buffer tra l'applicazione e il sistema operativo sottostante hello cui è in esecuzione. Di conseguenza, Service Fabric fornisce un modo tooconfigure *endpoint* per i servizi. Service Fabric assicura che siano disponibili per il servizio toouse endpoint. In questo modo, non è tooconfigure li manualmente in hello ambiente del sistema operativo sottostante. È facilmente possibile ospitare l'applicazione di Service Fabric in diversi ambienti senza la necessità di qualsiasi applicazione di modifiche tooyour toomake. (Ad esempio, è possibile ospitare hello stessa applicazione in Azure o nel proprio Data Center.)

Configurare un endpoint HTTP in PackageRoot\ServiceManifest.xml:

```xml
<Resources>
    <Endpoints>
        <Endpoint Name="ServiceEndpoint" Type="Input" Protocol="http" Port="8281" />
    </Endpoints>
</Resources>

```

Questo passaggio è importante perché il processo host del servizio di hello viene eseguito con credenziali limitate (servizio di rete in Windows). Ciò significa che il servizio non disporrà di accesso tooset un endpoint HTTP autonomamente. Tramite la configurazione dell'endpoint hello, Service Fabric SA tooset elenco di controllo di accesso appropriato hello (ACL) per hello URL hello servizio sarà in ascolto. Service Fabric fornisce anche una posizione standard tooconfigure endpoint.

Una volta tornati in OwinCommunicationListener.cs, iniziare a implementare OpenAsync. Si tratta in cui si avvia il server di web hello. Innanzitutto, ottenere informazioni sull'endpoint hello e creare URL hello che resterà in ascolto il servizio di hello. Hello URL sarà diverso a seconda se il listener hello viene utilizzato in un servizio senza stato o un servizio con stato. Per un servizio con stato, il listener hello deve toocreate univoco risolverlo per ogni replica del servizio con stato resta in attesa su. Per i servizi senza stati, indirizzo hello può essere molto più semplice. 

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

Si noti che viene usato "http://+" Si tratta di toomake assicurarsi che il server web hello è in ascolto su tutti gli indirizzi disponibili, inclusi localhost, FQDN e hello macchina IP.

Hello OpenAsync implementazione è uno dei motivi più importanti di hello motivo per cui server web hello (o qualsiasi stack di comunicazione) viene implementato come un ICommunicationListener, anziché la sola apre direttamente da `RunAsync()` nel servizio hello. valore restituito di Hello da OpenAsync è l'indirizzo hello hello server web è in ascolto. Quando questo indirizzo viene restituito il sistema toohello, Registra indirizzo hello con servizio hello. Service Fabric fornisce un'API che consente ai client e altri servizi toothen chiedere per questo indirizzo dal nome del servizio. Questo è importante perché l'indirizzo del servizio hello non è statico. Servizi vengono spostati nel cluster hello per scopi di bilanciamento del carico e disponibilità delle risorse. Questo è il meccanismo hello che consente ai client hello tooresolve indirizzo per un servizio in ascolto.

Tenendo in considerazione, OpenAsync avvia hello web server e restituisce indirizzo hello che è in ascolto. Si noti che è in ascolto "http://+", ma prima di OpenAsync restituisce indirizzo hello, salve "+" viene sostituito con hello IP o nome di dominio completo del nodo hello che corrente. indirizzo Hello restituito da questo metodo è ciò che è registrato con il sistema hello. È anche l'indirizzo visualizzato dai client e dagli altri servizi quando richiedono l'indirizzo di un servizio. Per i client toocorrectly connettersi tooit, devono disporre di un indirizzo IP o FQDN di effettivo indirizzo hello.

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

Si noti che questo riferimento di classe di avvio hello passato toohello OwinCommunicationListener nel costruttore hello. L'istanza di avvio viene usata da prova web server toobootstrap prova applicazione Web API.

Hello `ServiceEventSource.Current.Message()` riga verrà visualizzate nella finestra di eventi di diagnostica di hello in un secondo momento, quando si esegue tooconfirm applicazione hello che il server web hello è stato avviato correttamente.

## <a name="implement-closeasync-and-abort"></a>Implementare CloseAsync e Abort
Infine, implementano sia CloseAsync e interruzione del server web di toostop hello. server web Hello può essere arrestato eliminando l'handle del server hello durante OpenAsync è stato creato.

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

In questo esempio di implementazione, CloseAsync sia interruzione semplicemente Arresta server web di hello. È possibile scegliere tooperform un arresto del server web hello in CloseAsync più normalmente coordinato. Ad esempio, arresto hello potrebbe attendere le richieste in transito toobe completato prima di restituire hello.

## <a name="start-hello-web-server"></a>Avviare il server web hello
È ora pronto toocreate e restituire un'istanza del server web di OwinCommunicationListener toostart hello. Nella classe del servizio (WebService.cs) hello, eseguire l'override hello `CreateServiceInstanceListeners()` metodo:

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

Questo è hello in Web API *applicazione* e hello OWIN *host* infine soddisfare. host Hello (OwinCommunicationListener) viene assegnato a un'istanza di hello *applicazione* (API Web) tramite hello classe di avvio. Service Fabric ne gestisce quindi il ciclo di vita. Questo modello può essere seguito con qualsiasi stack di comunicazione.

## <a name="put-it-all-together"></a>Combinare tutti gli elementi
In questo esempio, non è necessario toodo qualsiasi elemento presente in hello `RunAsync()` (metodo), in modo che eseguono l'override può essere semplicemente rimossi.

implementazione del servizio finale Hello dovrebbe essere molto semplici. È necessario solo listener di comunicazione toocreate hello:

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

Hello completo `OwinCommunicationListener` classe:

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

Ora che è stato inserito tutte le parti di hello sul posto, il progetto dovrebbe essere simile una tipica applicazione Web API con punti di ingresso di API per servizi affidabili e un host OWIN.

## <a name="run-and-connect-through-a-web-browser"></a>Esecuzione e connessione tramite un Web browser
Se non lo si è già fatto, [configurare l'ambiente di sviluppo](service-fabric-get-started.md).

È ora possibile compilare e distribuire il servizio. Premere **F5** in Visual Studio toobuild e distribuire un'applicazione hello. Nella finestra di eventi di diagnostica hello, si verrà visualizzato un messaggio che indica che il server web hello aperto su http://localhost:8281 /.

> [!NOTE]
> Se la porta hello è già stata aperta da un altro processo nel computer in uso, si venga visualizzato un errore di seguito. Ciò indica che non è possibile aprire il listener hello. Se è questo caso di hello, provare a utilizzare una porta diversa per la configurazione di endpoint hello in ServiceManifest.xml.
> 
> 

Quando è in esecuzione il servizio di hello, aprire un browser e andare troppo[http://localhost:8281, api e valori](http://localhost:8281/api/values) tootest è.

## <a name="scale-it-out"></a>Scalabilità orizzontale
Scalabilità orizzontale di applicazioni web senza stato in genere significa aggiungere più computer e spin-up App web hello su di essi. Il motore di orchestrazione dell'infrastruttura servizio per questo scopo è ogni volta che vengono aggiunti il cluster tooa nuovi nodi. Quando si creano istanze di un servizio senza stato, è possibile specificare il numero di hello di istanze desiderato toocreate. Service Fabric inserisce tale numero di istanze nei nodi cluster hello. E garantisce toocreate non più di una istanza in un qualsiasi nodo. È anche possibile indicare tooalways Service Fabric crea un'istanza in ogni nodo specificando **-1** hello conteggio delle istanze. In questo modo si garantisce che ogni volta che si aggiunta tooscale i nodi del cluster, un'istanza del servizio senza stato verrà creata in nuovi nodi di hello. Questo valore è una proprietà dell'istanza di servizio hello, in modo che viene impostata quando si crea un'istanza del servizio. Per farlo, è possibile usare PowerShell:

```powershell

New-ServiceFabricService -ApplicationName "fabric:/WebServiceApplication" -ServiceName "fabric:/WebServiceApplication/WebService" -ServiceTypeName "WebServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1

```

Questa operazione può essere effettuata anche quando si definisce un servizio predefinito in un progetto di servizio senza stato di Visual Studio:

```xml

<DefaultServices>
  <Service Name="WebService">
    <StatelessService ServiceTypeName="WebServiceType" InstanceCount="-1">
      <SingletonPartition />
    </StatelessService>
  </Service>
</DefaultServices>

```

Per ulteriori informazioni sull'applicazione toocreate e istanze del servizio, vedere [distribuire un'applicazione](service-fabric-deploy-remove-applications.md).

## <a name="next-steps"></a>Passaggi successivi
[Debug dell'applicazione di Service Fabric mediante Visual Studio](service-fabric-debugging-your-application.md)

