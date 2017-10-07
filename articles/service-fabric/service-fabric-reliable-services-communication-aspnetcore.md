---
title: la comunicazione con ASP.NET Core hello aaaService | Documenti Microsoft
description: Informazioni su come toouse ASP.NET Core in servizi affidabili e senza stato.
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
ms.openlocfilehash: 6e6a83ab04390150292f63de5d9b51d290284e50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-core-in-service-fabric-reliable-services"></a>ASP.NET Core in Reliable Services di Service Fabric

ASP.NET Core è un nuovo framework open source e multipiattaforma per la compilazione di applicazioni Internet moderne basate sul cloud, ad esempio app Web, app per IoT e back-end per dispositivi mobili. 

Questo articolo è toohosting una guida approfondita di servizi di ASP.NET Core in Service Fabric servizi affidabili utilizzando hello **Microsoft.ServiceFabric.AspNetCore.** * set di pacchetti NuGet.

Per un'esercitazione introduttiva su ASP.NET Core in Service Fabric e istruzioni per la configurazione dell'ambiente di sviluppo, vedere [Compilare un front-end di servizio Web per l'applicazione tramite ASP.NET Core](service-fabric-add-a-web-frontend.md).

rest Hello di questo articolo presuppone una certa familiarità con ASP.NET Core. Se non è consigliabile esaminare hello [nozioni fondamentali su ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/index).

## <a name="aspnet-core-in-hello-service-fabric-environment"></a>ASP.NET Core nell'ambiente di Service Fabric hello

Mentre le applicazioni ASP.NET Core può essere eseguito su .NET Core o su hello su che completa di .NET Framework, servizi di Service Fabric attualmente può essere eseguito solo hello completa di .NET Framework. Ciò significa che quando si compila un servizio di Service Fabric di ASP.NET Core, è comunque necessario assegnare hello completa di .NET Framework.

ASP.NET Core può essere usato in due modi diversi in Service Fabric:
 - **Ospitato come eseguibile guest**. Si tratta principalmente usato toorun ASP.NET Core applicazioni esistenti in Service Fabric senza apportare modifiche al codice.
 - **Eseguito in un servizio Reliable Services**. Ciò consente una migliore integrazione con il runtime di Service Fabric hello e consente ai servizi con stato ASP.NET Core.

rest Hello di questo articolo viene illustrato come toouse ASP.NET Core all'interno di un servizio affidabile usando hello componenti di integrazione ASP.NET Core forniti con hello Service Fabric SDK. 

## <a name="service-fabric-service-hosting"></a>Hosting di servizi di Service Fabric

In Service Fabric, una o più istanze e/o repliche del servizio vengono eseguite in un *processo host del servizio*, un file eseguibile che esegue il codice del servizio. Come l'autore di un servizio, il proprietario processo host del servizio di hello e Service Fabric attiva e si esegue il monitoraggio per l'utente.

ASP.NET tradizionale (backup tooMVC 5) è fortemente accoppiata tooIIS tramite System.Web.dll. ASP.NET Core fornisce una separazione tra server web hello e l'applicazione web. In questo modo portabile tra i server web diverso toobe di applicazioni web e si consente inoltre di web server toobe *self-hosted*, ovvero è possibile avviare un server web in un processo personalizzato, come processo anziché tooa appartenente a web dedicato software server, come IIS. 

In ordine toocombine un servizio di Service Fabric e ASP.NET, come un eseguibile guest o in un servizio affidabile, è necessario essere in grado di toostart ASP.NET all'interno del processo host del servizio. ASP.NET Core self-hosting consente toodo questo.

## <a name="hosting-aspnet-core-in-a-reliable-service"></a>Hosting di ASP.NET Core in un servizio Reliable Services
In genere, le applicazioni ASP.NET Core indipendenti creano un WebHost nel punto di ingresso di un'applicazione, ad esempio hello `static void Main()` metodo `Program.cs`. In questo caso, hello ciclo di vita di hello WebHost è associato toohello ciclo di vita del processo di hello.

![Hosting di ASP.NET Core in un processo][0]

Tuttavia, il punto di ingresso applicazione hello non hello posto giusto toocreate un WebHost in un servizio affidabile, poiché viene utilizzato solo il punto di ingresso applicazione hello tooregister un servizio di tipo con il runtime di Service Fabric hello, in modo che è possibile creare istanze del servizio tipo. Hello WebHost deve essere creato in un servizio affidabile se stesso. Nel processo host del servizio di hello, le istanze del servizio e/o repliche possono essere eseguita per più cicli di vita. 

Un'istanza di Reliable Services è rappresentata dalla classe del servizio derivante da `StatelessService` o `StatefulService`. stack di comunicazione Hello per un servizio è contenuto in un `ICommunicationListener` implementazione nella classe del servizio. Hello `Microsoft.ServiceFabric.Services.AspNetCore.*` pacchetti NuGet contengono le implementazioni di `ICommunicationListener` che avvia e gestire hello ASP.NET Core WebHost per Kestrel o WebListener in un servizio affidabile.

![Hosting di ASP.NET Core in un servizio Reliable Services][1]

## <a name="aspnet-core-icommunicationlisteners"></a>ICommunicationListeners ASP.NET Core
Hello `ICommunicationListener` implementazioni per Kestrel e WebListener in hello `Microsoft.ServiceFabric.Services.AspNetCore.*` pacchetti NuGet sono modelli di utilizzo simili ma eseguire i server web tooeach specifico di azioni leggermente diverse. 

Entrambi i listener di comunicazione forniscono un costruttore che accetta hello gli argomenti seguenti:
 - **`ServiceContext serviceContext`**: hello `ServiceContext` oggetto contenente informazioni sul servizio hello.
 - **`string endpointName`**: nome hello un `Endpoint` configurazione in ServiceManifest.xml. Si tratta principalmente in cui il listener di comunicazione hello due diversi: WebListener **richiede** un `Endpoint` configurazione, mentre non Kestrel.
 - **`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: espressione lambda implementata in cui viene creato e restituito un elemento `IWebHost`. In questo modo è tooconfigure `IWebHost` hello normalmente i in un'applicazione ASP.NET Core. lambda Hello fornisce un URL che viene generato per in base a integrazione di Service Fabric hello opzioni di utilizzo e hello `Endpoint` permette di configurazione. Che URL può quindi essere modificato o se è stato utilizzato come-toostart hello web server.

## <a name="service-fabric-integration-middleware"></a>Middleware di integrazione di Service Fabric
Hello `Microsoft.ServiceFabric.Services.AspNetCore` pacchetto NuGet include hello `UseServiceFabricIntegration` metodo di estensione su `IWebHostBuilder` che aggiunge middleware che supporta Service Fabric. Consente di configurare questo middleware hello Kestrel o WebListener `ICommunicationListener` tooregister hello Service Fabric Naming Service e quindi la convalida di un URL di servizio univoco con servizio corretto toohello connessione dei client di tooensure di richieste client. Ciò è necessario in un ambiente host condiviso, ad esempio Service Fabric, in cui è possono eseguire su hello stesso fisico o macchina virtuale ma non utilizzano nomi host univoco, ai client di tooprevent erroneamente connessione servizio errato toohello più applicazioni web. Questo scenario viene descritto più dettagliatamente nella sezione successiva hello.

### <a name="a-case-of-mistaken-identity"></a>Un caso di identità errata
Le repliche del servizio, indipendentemente dal protocollo, sono in ascolto in una combinazione IP:porta univoca. Una volta avviata una replica del servizio in ascolto su un endpoint creato, viene segnalato che toohello indirizzo endpoint servizio Naming Service Fabric in cui può essere individuata dai client o da altri servizi. Se i servizi di porte assegnate dinamicamente applicazione, una replica del servizio possono utilizzare coincidenza hello stesso endpoint IP: Port di un altro servizio che è stato in precedenza in hello stesso fisico o macchina virtuale. Ciò può provocare un client toomistakely connettersi toohello di servizio non valido. Questa situazione può verificarsi se si verifica hello seguente sequenza di eventi:

 1. Il servizio A è in ascolto in 10.0.0.1:30000 su HTTP. 
 2. Il client risolve il servizio A e ottiene l'indirizzo 10.0.0.1:30000
 3. Un nodo diverso di spostamenti tooa del servizio.
 4. Servizio B viene applicato al 10.0.0.1 e coincidenza utilizza hello stessa porta 30000.
 5. Client tenta tooconnect tooservice A con 10.0.0.1:30000 indirizzi memorizzati nella cache.
 6. Client è ora sia connesso correttamente connesso tooservice B possa toohello di servizio non valido.

Ciò può causare errori in momenti casuali che possono essere difficile toodiagnose. 

### <a name="using-unique-service-urls"></a>Uso di URL di servizio univoci
tooprevent, servizi può registrare un toohello endpoint servizio di denominazione con un identificatore univoco e quindi convalidare tale identificatore univoco durante le richieste client. Si tratta di un'azione cooperativa tra servizi in un ambiente attendibile di tenant non ostili. Non offre l'autenticazione sicura dei servizi in un ambiente di tenant ostili.

In un ambiente attendibile, hello middleware che viene aggiunto per hello `UseServiceFabricIntegration` metodo aggiunge automaticamente un indirizzo di toohello identificatore univoco che viene registrato toohello servizio di denominazione e tale identificatore per ogni richiesta di convalida. Se non corrisponde a identificatore hello, hello middleware restituisce immediatamente una risposta HTTP 410 Gone.

I servizi che usano una porta assegnata dinamicamente devono usare questo middleware.

I servizi che usano una porta fissa univoca non hanno questo problema in un ambiente collaborativo. Una porta fissa univoca viene in genere utilizzata per i servizi esterno che è necessaria una porta ben nota per tooconnect applicazioni client per. La maggior parte delle applicazioni Web per Internet, ad esempio, usa la porta 80 o 443 per connessioni tramite Web browser. Identificatore univoco di hello in questo caso, non deve essere abilitata.

Hello diagramma seguente mostra il flusso di richiesta hello con middleware hello abilitato:

![Integrazione ASP.NET Core di Service Fabric][2]

Kestrel sia WebListener `ICommunicationListener` implementazioni usano questo meccanismo in hello esattamente allo stesso modo. Sebbene WebListener internamente in grado di distinguere le richieste in base ai percorsi di URL univoci utilizzando hello sottostante *http.sys* funzionalità, la funzionalità di condivisione delle porte *non* utilizzato da hello WebListener `ICommunicationListener` implementazione perché che causano codici di stato errore HTTP 503 e HTTP 404 nello scenario di hello descritto in precedenza. Che a sua volta rende molto difficile per finalità di hello client toodetermine di errore hello, come HTTP 503 e HTTP 404 sono già utilizzati tooindicate altri errori. Di conseguenza, Kestrel e WebListener `ICommunicationListener` implementazioni standardizzare middleware hello fornito da hello `UseServiceFabricIntegration` metodo di estensione in modo che i client devono solo un endpoint del servizio tooperform risolvere azione su risposte HTTP 410.

## <a name="weblistener-in-reliable-services"></a>WebListener in Reliable Services
WebListener può essere utilizzato in un servizio affidabile importando hello **Microsoft.ServiceFabric.AspNetCore.WebListener** pacchetto NuGet. Questo pacchetto contiene `WebListenerCommunicationListener`, un'implementazione di `ICommunicationListener`, che consente un WebHost Core ASP.NET all'interno di un servizio affidabile toocreate utilizzando WebListener come server web hello.

WebListener si basa su hello [API Server HTTP di Windows](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx). Questo metodo utilizza hello *http.sys* driver kernel utilizzato da IIS tooprocess HTTP richieste e loro tooprocesses eseguire applicazioni web di route. Ciò consente a più processi in hello stessa macchina virtuale o fisica toohost applicazioni web su hello stessa porta, identificata dal nome host o percorso URL univoco. Tali caratteristiche risultano utili in Service Fabric per ospitare più siti Web in hello dello stesso cluster.

Hello diagramma seguente illustra come WebListener utilizza hello *http.sys* driver kernel di Windows per la condivisione delle porte:

![http.sys][3]

### <a name="weblistener-in-a-stateless-service"></a>WebListener in un servizio senza stato
toouse `WebListener` in un servizio senza stato, eseguire l'override hello `CreateServiceInstanceListeners` metodo e restituire un `WebListenerCommunicationListener` istanza:

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

### <a name="weblistener-in-a-stateful-service"></a>WebListener in un servizio con stato

`WebListenerCommunicationListener`non è attualmente progettato per l'utilizzo nei servizi con stati scadenza toocomplications con hello sottostante *http.sys* funzionalità di condivisione delle porte. Per ulteriori informazioni, vedere l'argomento seguente sezione sull'allocazione delle porte dinamiche con WebListener hello. Per i servizi con stati, Kestrel è hello consigliato di server web.

### <a name="endpoint-configuration"></a>Configurazione dell'endpoint

Un `Endpoint` configurazione è necessaria per server web che utilizzano API Server HTTP di Windows, tra cui WebListener hello. Server Web che utilizzano API Server HTTP di Windows hello prima di tutto necessario riservare l'URL con *http.sys* (questa operazione viene in genere eseguita con hello [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) strumento). Questa azione richiede privilegi elevati che i servizi non hanno per impostazione predefinita. Hello "http" o "https" Opzioni di hello `Protocol` proprietà di hello `Endpoint` configurazione *ServiceManifest.xml* vengono utilizzati in particolare tooinstruct hello Service Fabric runtime tooregister un URL con *http.sys* per conto dell'utente utilizzando hello [ *carattere jolly complesso* ](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) prefisso dell'URL.

Ad esempio, tooreserve `http://+:80` per un servizio, hello configurazione seguente deve essere utilizzata in ServiceManifest.xml:

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

E il nome dell'endpoint hello deve essere passato toohello `WebListenerCommunicationListener` costruttore:

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

#### <a name="use-weblistener-with-a-static-port"></a>Usare WebListener con una porta statica
toouse una porta statica con WebListener, specificare il numero di porta hello in hello `Endpoint` configurazione:

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

#### <a name="use-weblistener-with-a-dynamic-port"></a>Usare WebListener con una porta dinamica
una porta assegnata dinamicamente con WebListener, toouse omettere hello `Port` proprietà hello `Endpoint` configurazione:

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" />
    </Endpoints>
  </Resources>
```

Si noti che una porta dinamica allocata da una configurazione `Endpoint` fornisce una sola porta *per ogni processo host*. Hello corrente Service Fabric, modello di hosting consente più servizio istanze e/o repliche toobe ospitati in hello stessa procedura adottata, vale a dire che ciascuna di esse condivideranno la stessa porta quando allocata tramite hello hello `Endpoint` configurazione. Più istanze di WebListener possono condividere una porta utilizzando hello sottostante *http.sys* funzionalità, ma che la condivisione delle porte non sono supportata da `WebListenerCommunicationListener` a causa di problemi toohello introduce per le richieste client. Per informazioni sull'utilizzo di porte dinamiche, Kestrel è hello consigliato di server web.

## <a name="kestrel-in-reliable-services"></a>Kestrel in Reliable Services
Kestrel può essere utilizzato in un servizio affidabile importando hello **Microsoft.ServiceFabric.AspNetCore.Kestrel** pacchetto NuGet. Questo pacchetto contiene `KestrelCommunicationListener`, un'implementazione di `ICommunicationListener`, che consente un WebHost Core ASP.NET all'interno di un servizio affidabile toocreate utilizzando Kestrel come server web hello.

Kestrel è che un server Web multipiattaforma per ASP.NET Core basato su libuv, una libreria I/O asincrona multipiattaforma. A differenza di WebListener, Kestrel non usa una gestione centralizzata dell'endpoint come *http.sys*. A differenza di WebListener, Kestrel non supporta la condivisione delle porte tra più processi. Ogni istanza di Kestrel deve usare una porta univoca.

![kestrel][4]

### <a name="kestrel-in-a-stateless-service"></a>Kestrel in un servizio senza stato
toouse `Kestrel` in un servizio senza stato, eseguire l'override hello `CreateServiceInstanceListeners` metodo e restituire un `KestrelCommunicationListener` istanza:

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

### <a name="kestrel-in-a-stateful-service"></a>Kestrel in un servizio con stato
toouse `Kestrel` in un servizio con stato, eseguire l'override hello `CreateServiceReplicaListeners` metodo e restituire un `KestrelCommunicationListener` istanza:

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

In questo esempio, un'istanza singleton del `IReliableStateManager` toohello WebHost contenitore dell'inserimento di dipendenza è disponibile. Questo non è strettamente necessario, ma consente toouse `IReliableStateManager` e affidabile raccolte nei metodi di azione di controller MVC.

Si noti che un `Endpoint` nome di configurazione **non** fornito troppo`KestrelCommunicationListener` in un servizio con stato. Ciò è illustrato più dettagliatamente nella seguente sezione hello.

### <a name="endpoint-configuration"></a>Configurazione dell'endpoint
Un `Endpoint` configurazione non è necessario toouse Kestrel. 

Kestrel è un server web autonoma semplice. a differenza di WebListener (o HttpListener), non è necessario un `Endpoint` configurazione *ServiceManifest.xml* perché non è necessario toostarting prima registrazione di URL. 

#### <a name="use-kestrel-with-a-static-port"></a>Usare Kestrel con una porta statica
È possibile configurare una porta statica in hello `Endpoint` ServiceManifest.xml la configurazione per l'utilizzo con Kestrel. Anche se non è strettamente necessaria, questa operazione offre due vantaggi potenziali:
 1. Se la porta hello non è compreso nell'intervallo di porte applicazione hello, viene aperta tramite firewall del sistema operativo hello dall'infrastruttura del servizio.
 2. Hello tooyou URL fornito tramite `KestrelCommunicationListener` utilizzerà questa porta.

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

Se un `Endpoint` è configurato, il nome deve essere passato in hello `KestrelCommunicationListener` costruttore: 

```csharp
new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) => ...
```

Se un `Endpoint` configurazione non viene utilizzata, omettere il nome di hello in hello `KestrelCommunicationListener` costruttore. In questo caso verrà usata una porta dinamica. Vedere hello sezione successiva per ulteriori informazioni.

#### <a name="use-kestrel-with-a-dynamic-port"></a>Usare Kestrel con una porta dinamica
Kestrel non è possibile utilizzare l'assegnazione automatica porta hello da hello `Endpoint` configurazione in ServiceManifest.xml, perché l'assegnazione automatica porta da un `Endpoint` configurazione assegna una porta univoca per ogni *processo host* , e un singolo processo host può contenere più istanze di Kestrel. Poiché Kestrel non supporta la condivisione delle porte, questa modalità di assegnazione non funziona perché ogni istanza di Kestrel deve essere aperta in una porta univoca.

assegnazione di porte dinamiche toouse con Kestrel, omettere hello `Endpoint` configurazione in ServiceManifest.xml interamente e che non superano un toohello nome endpoint `KestrelCommunicationListener` costruttore:

```csharp
new KestrelCommunicationListener(serviceContext, (url, listener) => ...
```

In questa configurazione, `KestrelCommunicationListener` selezionerà automaticamente una porta inutilizzata dall'intervallo di porte applicazione hello.

## <a name="scenarios-and-configurations"></a>Scenari e configurazioni
Questa sezione descrive i seguenti scenari hello e fornisce hello consiglia combinazione di server web, la configurazione della porta, le opzioni di integrazione di Service Fabric e tooachieve varie impostazioni di un servizio che funzionano correttamente:
 - Servizio ASP.NET Core senza stato esposto all'esterno
 - Servizio ASP.NET Core senza stato solo interno
 - Servizio ASP.NET Core con stato solo interno

Un **esposta esternamente** è un servizio che espone un endpoint raggiungibile all'esterno del cluster di hello, generalmente tramite un servizio di bilanciamento del carico.

Un **solo interno** del servizio è uno cui endpoint sia raggiungibile all'interno di cluster hello solo.

> [!NOTE]
> Servizio con stato endpoint non devono in genere essere esposto toohello Internet. Cluster protetti da servizi di bilanciamento del carico che non siano informati di risoluzione del servizio Service Fabric, ad esempio hello bilanciamento del carico di Azure, sarà servizi con stato non è possibile tooexpose perché bilanciamento del carico hello non essere in grado di toolocate e indirizzare il traffico toohello replica del servizio con stato appropriato. 

### <a name="externally-exposed-aspnet-core-stateless-services"></a>Servizi ASP.NET Core senza stato esposti all'esterno
WebListener viene consigliato di server web per i servizi front-end che espone gli endpoint HTTP esterni e con connessione Internet in Windows hello. Offre una migliore protezione dagli attacchi e supporta funzionalità non supportate da Kestrel, ad esempio l'autenticazione di Windows e la condivisione delle porte. 

Kestrel non è attualmente supportato come server perimetrale per Internet. È necessario utilizzare un server proxy inverso, ad esempio IIS o Nginx toohandle traffico da hello rete Internet pubblica.
 
Quando toohello esposto Internet, un servizio senza stato deve utilizzare un endpoint noto e stabile che sia raggiungibile tramite un servizio di bilanciamento del carico. Si tratta hello URL si fornirà toousers dell'applicazione. è consigliabile Hello seguente configurazione:

|  |  | **Note** |
| --- | --- | --- |
| Server Web | WebListener | Se il servizio di hello è solo tooa esposto rete attendibile, una rete intranet, è possibile utilizzare Kestrel. In caso contrario, WebListener è hello preferito. |
| Configurazione delle porte | Statica | Una porta statica nota deve essere configurata in hello `Endpoints` configurazione di ServiceManifest.xml, ad esempio 80 per HTTP o 443 per HTTPS. |
| ServiceFabricIntegrationOptions | Nessuno | Hello `ServiceFabricIntegrationOptions.None` opzione deve essere utilizzata quando si configura il middleware di integrazione dell'infrastruttura di servizio in modo che il servizio di hello non toovalidate le richieste in ingresso per un identificatore univoco. Gli utenti esterni di applicazione non riconoscerà hello informazioni di identificazione univoche utilizzate dal middleware hello. |
| Conteggio istanze | -1 | In casi di utilizzo tipico, il numero di istanze hello impostazione deve essere impostato troppo "-1" in modo che un'istanza è disponibile in tutti i nodi che ricevono il traffico dal bilanciamento del carico. |

Se più servizi esposti esternamente condividono hello stesso set di nodi, utilizzare un percorso URL univoco ma stabile. Questo può essere eseguito modificando hello URL fornito quando si configura IWebHost. Si noti come che si applica solo a tooWebListener.

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

### <a name="internal-only-stateless-aspnet-core-service"></a>Servizio ASP.NET Core senza stato solo interno
I servizi senza stati che vengono chiamati solo da all'interno di cluster hello devono utilizzare URL univoci e le porte assegnate dinamicamente tooensure cooperazione tra più servizi. è consigliabile Hello seguente configurazione:

|  |  | **Note** |
| --- | --- | --- |
| Server Web | Kestrel | Sebbene WebListener possono essere utilizzati per i servizi senza stati interni, Kestrel è hello consigliato tooallow server tooshare istanze di servizio più un host.  |
| Configurazione delle porte | assegnate in modo dinamico | Più repliche di un servizio con stato possono condividere un processo host o un sistema operativo host e richiedono quindi porte univoche. |
| ServiceFabricIntegrationOptions | UseUniqueServiceUrl | Assegnazione di porte dinamiche, questa impostazione impedisce problema identità hello erroneamente descritto in precedenza. |
| InstanceCount | qualsiasi | numero di istanze di Hello impostazione può essere impostato del servizio di hello tooany valore toooperate necessarie. |

### <a name="internal-only-stateful-aspnet-core-service"></a>Servizio ASP.NET Core con stato solo interno
I servizi con stati che vengono chiamati solo da all'interno di cluster hello devono utilizzare porte assegnate dinamicamente tooensure cooperazione tra più servizi. è consigliabile Hello seguente configurazione:

|  |  | **Note** |
| --- | --- | --- |
| Server Web | Kestrel | Hello `WebListenerCommunicationListener` non deve essere utilizzato dai servizi con stati in cui le repliche condividono un processo host. |
| Configurazione delle porte | assegnate in modo dinamico | Più repliche di un servizio con stato possono condividere un processo host o un sistema operativo host e richiedono quindi porte univoche. |
| ServiceFabricIntegrationOptions | UseUniqueServiceUrl | Assegnazione di porte dinamiche, questa impostazione impedisce problema identità hello erroneamente descritto in precedenza. |

## <a name="next-steps"></a>Passaggi successivi
[Debug dell'applicazione di Service Fabric mediante Visual Studio](service-fabric-debugging-your-application.md)

<!--Image references-->
[0]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-standalone.png
[1]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-servicefabric.png
[2]:./media/service-fabric-reliable-services-communication-aspnetcore/integration.png
[3]:./media/service-fabric-reliable-services-communication-aspnetcore/httpsys.png
[4]:./media/service-fabric-reliable-services-communication-aspnetcore/kestrel.png
