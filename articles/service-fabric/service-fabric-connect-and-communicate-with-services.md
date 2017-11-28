---
title: aaaConnect e comunicare con servizi di Azure Service Fabric | Documenti Microsoft
description: Informazioni su come tooresolve, connettersi e comunicare con servizi di Service Fabric.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: msfussell
ms.assetid: 7d1052ec-2c9f-443d-8b99-b75c97266e6c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/9/2017
ms.author: vturecek
ms.openlocfilehash: b8b374a71d4c5d21f48a560a3a8c81b357fe418d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-and-communicate-with-services-in-service-fabric"></a><span data-ttu-id="5b0a5-103">Connettersi e comunicare con i servizi in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5b0a5-103">Connect and communicate with services in Service Fabric</span></span>
<span data-ttu-id="5b0a5-104">In Service Fabric un servizio viene eseguito in una posizione nel cluster di Service Fabric, in genere distribuito su più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-104">In Service Fabric, a service runs somewhere in a Service Fabric cluster, typically distributed across multiple VMs.</span></span> <span data-ttu-id="5b0a5-105">Può essere spostato da un'unica posizione tooanother, dal proprietario del servizio hello o automaticamente dall'infrastruttura del servizio.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-105">It can be moved from one place tooanother, either by hello service owner, or automatically by Service Fabric.</span></span> <span data-ttu-id="5b0a5-106">Servizi non sono collegati in modo statico tooa specifico computer o l'indirizzo.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-106">Services are not statically tied tooa particular machine or address.</span></span>

<span data-ttu-id="5b0a5-107">Un'applicazione di Service Fabric è in genere costituita da molti servizi diversi, ognuno dei quali esegue un'attività specializzata.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-107">A Service Fabric application is generally composed of many different services, where each service performs a specialized task.</span></span> <span data-ttu-id="5b0a5-108">Questi servizi possono comunicare tra loro tooform una funzione completa, ad esempio parti diverse di rendering di un'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-108">These services may communicate with each other tooform a complete function, such as rendering different parts of a web application.</span></span> <span data-ttu-id="5b0a5-109">Sono disponibili anche le applicazioni che si connettono tooand comunicano con i servizi client.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-109">There are also client applications that connect tooand communicate with services.</span></span> <span data-ttu-id="5b0a5-110">Questo documento vengono illustrate come tooset delle comunicazioni con e tra i servizi di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-110">This document discusses how tooset up communication with and between your services in Service Fabric.</span></span>

<span data-ttu-id="5b0a5-111">Questo video di Microsoft Virtual Academy illustra anche la comunicazione tra servizi: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965"></span><span class="sxs-lookup"><span data-stu-id="5b0a5-111">This Microsoft Virtual Academy video also discusses service communication: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965"></span></span>  
<img src="./media/service-fabric-connect-and-communicate-with-services/CommunicationVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="bring-your-own-protocol"></a><span data-ttu-id="5b0a5-112">Usare un protocollo personalizzato</span><span class="sxs-lookup"><span data-stu-id="5b0a5-112">Bring your own protocol</span></span>
<span data-ttu-id="5b0a5-113">Service Fabric aiuta a gestire il ciclo di vita di hello dei servizi, ma non apporta le decisioni sulle operazioni dei servizi.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-113">Service Fabric helps manage hello lifecycle of your services but it does not make decisions about what your services do.</span></span> <span data-ttu-id="5b0a5-114">incluse le comunicazioni.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-114">This includes communication.</span></span> <span data-ttu-id="5b0a5-115">Quando il servizio viene aperto dall'infrastruttura di servizio, ovvero tooset opportunità del servizio backup di un endpoint per le richieste in ingresso, utilizzando qualsiasi stack di comunicazione o di protocollo desiderato.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-115">When your service is opened by Service Fabric, that's your service's opportunity tooset up an endpoint for incoming requests, using whatever protocol or communication stack you want.</span></span> <span data-ttu-id="5b0a5-116">Il servizio rimarrà in ascolto su un indirizzo **IP:porta** normale usando qualsiasi schema di indirizzamento, ad esempio un URI.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-116">Your service will listen on a normal **IP:port** address using any addressing scheme, such as a URI.</span></span> <span data-ttu-id="5b0a5-117">Più istanze del servizio o repliche possono condividere un processo host, nel qual caso viene verrà necessita di porte diverse toouse o utilizzare un meccanismo di condivisione delle porte, ad esempio driver di kernel hello http.sys in Windows.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-117">Multiple service instances or replicas may share a host process, in which case they will either need toouse different ports or use a port-sharing mechanism, such as hello http.sys kernel driver in Windows.</span></span> <span data-ttu-id="5b0a5-118">In entrambi i casi, ogni istanza o replica del servizio in un processo host deve essere indirizzabile in modo univoco.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-118">In either case, each service instance or replica in a host process must be uniquely addressable.</span></span>

![Endpoint del servizio][1]

## <a name="service-discovery-and-resolution"></a><span data-ttu-id="5b0a5-120">Individuazione e risoluzione del servizio</span><span class="sxs-lookup"><span data-stu-id="5b0a5-120">Service discovery and resolution</span></span>
<span data-ttu-id="5b0a5-121">In un sistema distribuito, servizi possono spostarsi da una macchina tooanother nel tempo.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-121">In a distributed system, services may move from one machine tooanother over time.</span></span> <span data-ttu-id="5b0a5-122">per vari motivi, incluso il bilanciamento delle risorse, aggiornamenti, failover o aumento del numero di istanze. Ciò significa che gli indirizzi degli endpoint di servizio modificare come servizio hello Sposta toonodes con indirizzi IP diversi e può aprire su porte diverse se il servizio di hello utilizza una porta selezionata in modo dinamico.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-122">This can happen for various reasons, including resource balancing, upgrades, failovers, or scale-out. This means service endpoint addresses change as hello service moves toonodes with different IP addresses, and may open on different ports if hello service uses a dynamically selected port.</span></span>

![Distribuzione dei servizi][7]

<span data-ttu-id="5b0a5-124">Service Fabric fornisce un rilevamento e la chiamata del servizio di risoluzione hello Naming Service.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-124">Service Fabric provides a discovery and resolution service called hello Naming Service.</span></span> <span data-ttu-id="5b0a5-125">Hello Naming Service mantiene una tabella in cui viene eseguito il mapping denominato le istanze del servizio sono in ascolto su toohello indirizzi dell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-125">hello Naming Service maintains a table that maps named service instances toohello endpoint addresses they listen on.</span></span> <span data-ttu-id="5b0a5-126">Tutte le istanze del servizio denominato in Service Fabric hanno nomi univoci rappresentati come URI, ad esempio `"fabric:/MyApplication/MyService"`.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-126">All named service instances in Service Fabric have unique names represented as URIs, for example, `"fabric:/MyApplication/MyService"`.</span></span> <span data-ttu-id="5b0a5-127">nome Hello del servizio di hello non cambia nel corso della durata del servizio hello hello, solo gli indirizzi endpoint hello che possono cambiare quando sposta servizi.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-127">hello name of hello service does not change over hello lifetime of hello service, it's only hello endpoint addresses that can change when services move.</span></span> <span data-ttu-id="5b0a5-128">Si tratta di toowebsites analoga che dispongono di URL costante, ma in cui è possibile modificare l'indirizzo IP hello.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-128">This is analogous toowebsites that have constant URLs but where hello IP address may change.</span></span> <span data-ttu-id="5b0a5-129">TooDNS simile nel web hello, che risolve gli URL tooIP indirizzi dei siti Web, Service Fabric è un registrar che esegue il mapping indirizzo endpoint del servizio nomi tootheir.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-129">And similar tooDNS on hello web, which resolves website URLs tooIP addresses, Service Fabric has a registrar that maps service names tootheir endpoint address.</span></span>

![Endpoint del servizio][2]

<span data-ttu-id="5b0a5-131">Risoluzione e la connessione tooservices comporta hello seguendo i passaggi eseguiti in un ciclo:</span><span class="sxs-lookup"><span data-stu-id="5b0a5-131">Resolving and connecting tooservices involves hello following steps run in a loop:</span></span>

* <span data-ttu-id="5b0a5-132">**Risolvere**: endpoint hello Get che un servizio pubblicato da hello Naming Service.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-132">**Resolve**: Get hello endpoint that a service has published from hello Naming Service.</span></span>
* <span data-ttu-id="5b0a5-133">**Connettersi**: servizio toohello di connettersi tramite il protocollo viene utilizzato tale endpoint.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-133">**Connect**: Connect toohello service over whatever protocol it uses on that endpoint.</span></span>
* <span data-ttu-id="5b0a5-134">**Ripetere**: un tentativo di connessione potrebbe non riuscire per diversi motivi, ad esempio se il servizio di hello è stato spostato dall'indirizzo endpoint hello hello ultima ora è stato risolto.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-134">**Retry**: A connection attempt may fail for any number of reasons, for example if hello service has moved since hello last time hello endpoint address was resolved.</span></span> <span data-ttu-id="5b0a5-135">In tal caso, hello precedente risoluzione e connettersi toobe ritentata necessario passaggi e il ciclo viene ripetuto fino a quando non hello connessione ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-135">In that case, hello preceding resolve and connect steps need toobe retried, and this cycle is repeated until hello connection succeeds.</span></span>

## <a name="connecting-tooother-services"></a><span data-ttu-id="5b0a5-136">La connessione di servizi tooother</span><span class="sxs-lookup"><span data-stu-id="5b0a5-136">Connecting tooother services</span></span>
<span data-ttu-id="5b0a5-137">Servizi che si connettono tooeach altro all'interno di un cluster in genere possibile accedere direttamente a endpoint hello di altri servizi poiché nodi hello in un cluster si trovano in hello stessa rete locale.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-137">Services connecting tooeach other inside a cluster generally can directly access hello endpoints of other services because hello nodes in a cluster are on hello same local network.</span></span> <span data-ttu-id="5b0a5-138">toomake è più facile tooconnect tra servizi, Service Fabric fornisce altri servizi che utilizzano hello Naming Service.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-138">toomake is easier tooconnect between services, Service Fabric provides additional services that use hello Naming Service.</span></span> <span data-ttu-id="5b0a5-139">un servizio DNS e un servizio di proxy inverso.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-139">A DNS service and a reverse proxy service.</span></span>


### <a name="dns-service"></a><span data-ttu-id="5b0a5-140">Servizio DNS</span><span class="sxs-lookup"><span data-stu-id="5b0a5-140">DNS service</span></span>
<span data-ttu-id="5b0a5-141">Poiché molti servizi, in particolare nei contenitori, possono avere un nome URL esistente, viene tooresolve in grado di utilizzare hello protocollo DNS standard (anziché il protocollo di Naming Service hello) è molto utile, soprattutto nell'applicazione "accuratezza e shift" scenari.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-141">Since many services, especially containerized services, can have an existing URL name, being able tooresolve these using hello standard DNS protocol (rather than hello Naming Service protocol) is very convenient, especially in application "lift and shift" scenarios.</span></span> <span data-ttu-id="5b0a5-142">Questo è esattamente il servizio DNS hello.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-142">This is exactly what hello DNS service does.</span></span> <span data-ttu-id="5b0a5-143">Consente di toomap nomi tooa servizio nome DNS e quindi risolvere indirizzi IP degli endpoint.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-143">It enables you toomap DNS names tooa service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="5b0a5-144">Come hello illustrato nel diagramma seguente, hello servizio DNS, in esecuzione nel cluster di Service Fabric hello, esegue il mapping nomi tooservice dei nomi DNS vengono risolte quindi hello Naming Service tooreturn hello endpoint indirizzi tooconnect per.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-144">As shown in hello following diagram, hello DNS service, running in hello Service Fabric cluster, maps DNS names tooservice names which are then resolved by hello Naming Service tooreturn hello endpoint addresses tooconnect to.</span></span> <span data-ttu-id="5b0a5-145">nome DNS Hello hello servizio viene fornito al momento di hello della creazione.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-145">hello DNS name for hello service is provided at hello time of creation.</span></span> 

![Endpoint del servizio][9]

<span data-ttu-id="5b0a5-147">Per ulteriori informazioni su come toouse hello servizio DNS vedere [servizio DNS in Azure Service Fabric](service-fabric-dnsservice.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-147">For more details on how toouse hello DNS service see [DNS service in Azure Service Fabric](service-fabric-dnsservice.md) article.</span></span>

### <a name="reverse-proxy-service"></a><span data-ttu-id="5b0a5-148">Servizio di proxy inverso</span><span class="sxs-lookup"><span data-stu-id="5b0a5-148">Reverse proxy service</span></span>
<span data-ttu-id="5b0a5-149">proxy inverso Hello indirizzi servizi in cluster hello che espone gli endpoint HTTP inclusi HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-149">hello reverse proxy addresses services in hello cluster that exposes HTTP endpoints including HTTPS.</span></span> <span data-ttu-id="5b0a5-150">proxy inverso Hello semplifica notevolmente la chiamata di altri servizi e i relativi metodi con uno specifico formato URI hello risolvere, gli handle di connessione, passaggi ripetizione necessari per toocommunicate un servizio con un altro utilizzando hello servizio di denominazione.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-150">hello reverse proxy greatly simplifies calling other services and their methods by having a specific URI format and handles hello resolve, connect, retry steps required for one service toocommunicate with another using hello Naming Serivce.</span></span> <span data-ttu-id="5b0a5-151">In altre parole, nasconde hello Naming Service da parte dell'utente quando si chiama altri servizi, eseguendo questo semplice come la chiamata a un URL.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-151">In other words, it hides hello Naming Service from you when calling other services by making this as simple as calling a URL.</span></span>

![Endpoint del servizio][10]

<span data-ttu-id="5b0a5-153">Per ulteriori informazioni su come toouse hello inversa servizio proxy vedere [inverso in Azure Service Fabric](service-fabric-reverseproxy.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-153">For more details on how toouse hello reverse proxy service see [Reverse proxy in Azure Service Fabric](service-fabric-reverseproxy.md) article.</span></span>

## <a name="connections-from-external-clients"></a><span data-ttu-id="5b0a5-154">Connessioni da client esterni</span><span class="sxs-lookup"><span data-stu-id="5b0a5-154">Connections from external clients</span></span>
<span data-ttu-id="5b0a5-155">Servizi che si connettono tooeach altro all'interno di un cluster in genere possibile accedere direttamente a endpoint hello di altri servizi poiché nodi hello in un cluster si trovano in hello stessa rete locale.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-155">Services connecting tooeach other inside a cluster generally can directly access hello endpoints of other services because hello nodes in a cluster are on hello same local network.</span></span> <span data-ttu-id="5b0a5-156">In alcuni ambienti, tuttavia, è possibile che un cluster si trovi dietro un servizio di bilanciamento del carico che indirizza il traffico esterno in ingresso attraverso un set limitato di porte.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-156">In some environments, however, a cluster may be behind a load balancer that routes external ingress traffic through a limited set of ports.</span></span> <span data-ttu-id="5b0a5-157">In questi casi, possono comunque comunicare tra loro e risolvere gli indirizzi tramite hello Naming Service, ma passaggi aggiuntivi devono essere prese tooallow client esterni tooconnect tooservices.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-157">In these cases, services can still communicate with each other and resolve addresses using hello Naming Service, but extra steps must be taken tooallow external clients tooconnect tooservices.</span></span>

## <a name="service-fabric-in-azure"></a><span data-ttu-id="5b0a5-158">Service Fabric in Azure</span><span class="sxs-lookup"><span data-stu-id="5b0a5-158">Service Fabric in Azure</span></span>
<span data-ttu-id="5b0a5-159">Un cluster di Service Fabric in Azure viene posizionato dietro un servizio di bilanciamento del carico di Azure.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-159">A Service Fabric cluster in Azure is placed behind an Azure Load Balancer.</span></span> <span data-ttu-id="5b0a5-160">Tutti i cluster toohello traffico esterno deve passare tramite servizio di bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-160">All external traffic toohello cluster must pass through hello load balancer.</span></span> <span data-ttu-id="5b0a5-161">Hello bilanciamento del carico verrà automaticamente inoltrare il traffico in entrata per tooa una determinata porta casuale *nodo* con hello aprire stessa porta.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-161">hello load balancer will automatically forward traffic inbound on a given port tooa random *node* that has hello same port open.</span></span> <span data-ttu-id="5b0a5-162">Hello bilanciamento del carico di Azure riconosce solo sulle porte aperte sul hello *nodi*, non è a conoscenza sull'apertura delle porte per singoli *servizi*.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-162">hello Azure Load Balancer only knows about ports open on hello *nodes*, it does not know about ports open by individual *services*.</span></span>

![Servizio di bilanciamento del carico di Azure e topologia di Service Fabric][3]

<span data-ttu-id="5b0a5-164">Ad esempio, in ordine tooaccept il traffico di esterno sulla porta **80**, deve essere configurato hello seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="5b0a5-164">For example, in order tooaccept external traffic on port **80**, hello following things must be configured:</span></span>

1. <span data-ttu-id="5b0a5-165">Scrivere un servizio che resta in ascolto sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-165">Write a service that listens on port 80.</span></span> <span data-ttu-id="5b0a5-166">Configurare la porta 80 in ServiceManifest.xml del servizio hello e aprire un listener nel servizio di hello, ad esempio, un server web self-hosted.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-166">Configure port 80 in hello service's ServiceManifest.xml and open a listener in hello service, for example, a self-hosted web server.</span></span>

    ```xml
    <Resources>
        <Endpoints>
            <Endpoint Name="WebEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>
    ```
    ```csharp
        class HttpCommunicationListener : ICommunicationListener
        {
            ...

            public Task<string> OpenAsync(CancellationToken cancellationToken)
            {
                EndpointResourceDescription endpoint =
                    serviceContext.CodePackageActivationContext.GetEndpoint("WebEndpoint");

                string uriPrefix = $"{endpoint.Protocol}://+:{endpoint.Port}/myapp/";

                this.httpListener = new HttpListener();
                this.httpListener.Prefixes.Add(uriPrefix);
                this.httpListener.Start();

                string publishUri = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
                return Task.FromResult(publishUri);
            }

            ...
        }

        class WebService : StatelessService
        {
            ...

            protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
            {
                return new[] { new ServiceInstanceListener(context => new HttpCommunicationListener(context))};
            }

            ...
        }
    ```
    ```java
        class HttpCommunicationlistener implements CommunicationListener {
            ...

            @Override
            public CompletableFuture<String> openAsync(CancellationToken arg0) {
                EndpointResourceDescription endpoint =
                    this.serviceContext.getCodePackageActivationContext().getEndpoint("WebEndpoint");
                try {
                    HttpServer server = com.sun.net.httpserver.HttpServer.create(new InetSocketAddress(endpoint.getPort()), 0);
                    server.start();

                    String publishUri = String.format("http://%s:%d/",
                        this.serviceContext.getNodeContext().getIpAddressOrFQDN(), endpoint.getPort());
                    return CompletableFuture.completedFuture(publishUri);
                } catch (IOException e) {
                    throw new RuntimeException(e);
                }
            }

            ...
        }

        class WebService extends StatelessService {
            ...

            @Override
            protected List<ServiceInstanceListener> createServiceInstanceListeners() {
                <ServiceInstanceListener> listeners = new ArrayList<ServiceInstanceListener>();
                listeners.add(new ServiceInstanceListener((context) -> new HttpCommunicationlistener(context)));
                return listeners;       
            }

            ...
        }
    ```
2. <span data-ttu-id="5b0a5-167">Creare un Cluster di Service Fabric in Azure e specificare la porta **80** come una porta dell'endpoint personalizzato per il tipo di nodo hello che ospiterà il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-167">Create a Service Fabric Cluster in Azure and specify port **80** as a custom endpoint port for hello node type that will host hello service.</span></span> <span data-ttu-id="5b0a5-168">Se si dispone di più di un tipo di nodo, è possibile impostare un *vincoli di posizionamento* su tooensure servizio hello viene eseguito solo sul tipo di nodo hello dotato di porta dell'endpoint personalizzata hello aperto.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-168">If you have more than one node type, you can set up a *placement constraint* on hello service tooensure it only runs on hello node type that has hello custom endpoint port opened.</span></span>

    ![Apertura di una porta su un tipo di nodo][4]
3. <span data-ttu-id="5b0a5-170">Dopo aver creato il cluster hello, configurare hello Azure servizio di bilanciamento del carico del traffico tooforward gruppo di risorse del cluster hello sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-170">Once hello cluster has been created, configure hello Azure Load Balancer in hello cluster's Resource Group tooforward traffic on port 80.</span></span> <span data-ttu-id="5b0a5-171">Quando si crea un cluster tramite hello portale di Azure, questo viene configurato automaticamente per ogni porta di endpoint personalizzato che è stato configurato.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-171">When creating a cluster through hello Azure portal, this is set up automatically for each custom endpoint port that was configured.</span></span>

    ![Inoltrare il traffico in hello bilanciamento del carico di Azure][5]
4. <span data-ttu-id="5b0a5-173">Hello se viene utilizzato il bilanciamento del carico Azure toodetermine un probe o non toosend traffico tooa determinato nodo.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-173">hello Azure Load Balancer uses a probe toodetermine whether or not toosend traffic tooa particular node.</span></span> <span data-ttu-id="5b0a5-174">periodicamente Hello probe controlli di un endpoint in ogni nodo di toodetermine o meno risponde nodo hello.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-174">hello probe periodically checks an endpoint on each node toodetermine whether or not hello node is responding.</span></span> <span data-ttu-id="5b0a5-175">Caso di probe hello tooreceive una risposta dopo un numero di volte configurato, bilanciamento del carico hello interrompe l'invio di nodo toothat traffico.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-175">If hello probe fails tooreceive a response after a configured number of times, hello load balancer stops sending traffic toothat node.</span></span> <span data-ttu-id="5b0a5-176">Quando si crea un cluster tramite hello portale di Azure, un probe viene automaticamente configurato per ogni porta di endpoint personalizzato che è stato configurato.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-176">When creating a cluster through hello Azure portal, a probe is automatically set up for each custom endpoint port that was configured.</span></span>

    ![Inoltrare il traffico in hello bilanciamento del carico di Azure][8]

<span data-ttu-id="5b0a5-178">È importante tooremember che hello bilanciamento del carico di Azure e un probe hello riconosce solo hello *nodi*, non hello *servizi* in esecuzione in nodi hello.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-178">It's important tooremember that hello Azure Load Balancer and hello probe only know about hello *nodes*, not hello *services* running on hello nodes.</span></span> <span data-ttu-id="5b0a5-179">Hello bilanciamento del carico di Azure inviano sempre toonodes di traffico che rispondono toohello probe, pertanto prestare attenzione tooensure services sono disponibili nei nodi hello che sono in grado di toorespond toohello probe.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-179">hello Azure Load Balancer will always send traffic toonodes that respond toohello probe, so care must be taken tooensure services are available on hello nodes that are able toorespond toohello probe.</span></span>

## <a name="reliable-services-built-in-communication-api-options"></a><span data-ttu-id="5b0a5-180">Reliable Services: opzioni predefinite per l'API di comunicazione</span><span class="sxs-lookup"><span data-stu-id="5b0a5-180">Reliable Services: Built-in communication API options</span></span>
<span data-ttu-id="5b0a5-181">framework servizi affidabili Hello viene fornito con diverse opzioni di comunicazione preesistente.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-181">hello Reliable Services framework ships with several pre-built communication options.</span></span> <span data-ttu-id="5b0a5-182">su quali uno più adatta per la decisione di Hello dipende dalla scelta hello del modello di programmazione, il framework di comunicazione hello e i servizi vengono scritti nel linguaggio di programmazione hello hello.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-182">hello decision about which one will work best for you depends on hello choice of hello programming model, hello communication framework, and hello programming language that your services are written in.</span></span>

* <span data-ttu-id="5b0a5-183">**Nessun protocollo specifico:** se non si dispone di una particolare scelta del framework di comunicazione, ma si desidera tooget qualcosa di attivare ed eseguire rapidamente, sarà hello ideale dell'opzione [comunicazione remota del servizio](service-fabric-reliable-services-communication-remoting.md), che consente fortemente tipizzata di procedura remota chiama i servizi affidabili e Reliable Actors.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-183">**No specific protocol:**  If you don't have a particular choice of communication framework, but you want tooget something up and running quickly, then hello ideal option for you is [service remoting](service-fabric-reliable-services-communication-remoting.md), which allows strongly-typed remote procedure calls for Reliable Services and Reliable Actors.</span></span> <span data-ttu-id="5b0a5-184">Questo è più semplice hello e tooget modo più rapido avviato comunicazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-184">This is hello easiest and fastest way tooget started with service communication.</span></span> <span data-ttu-id="5b0a5-185">Le comunicazioni remote del servizio gestiscono la risoluzione degli indirizzi del servizio, la connessione, la ripetizione dei tentativi e la gestione degli errori.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-185">Service remoting handles resolution of service addresses, connection, retry, and error handling.</span></span> <span data-ttu-id="5b0a5-186">Questo è disponibile sia per applicazioni C# che per applicazioni Java.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-186">This is available for both C# and Java applications.</span></span>
* <span data-ttu-id="5b0a5-187">**HTTP**: per comunicazioni indipendenti dal linguaggio, HTTP costituisce la scelta standard di settore, con strumenti e server HTTP disponibili in molti linguaggi diversi, tutti supportati da Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-187">**HTTP**: For language-agnostic communication, HTTP provides an industry-standard choice with tools and HTTP servers available in many different languages, all supported by Service Fabric.</span></span> <span data-ttu-id="5b0a5-188">I servizi possono usare qualsiasi stack HTTP disponibile, inclusa l'[API Web ASP.NET](service-fabric-reliable-services-communication-webapi.md) per applicazioni C#.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-188">Services can use any HTTP stack available, including [ASP.NET Web API](service-fabric-reliable-services-communication-webapi.md) for C# applications.</span></span> <span data-ttu-id="5b0a5-189">I client scritti in c# possono sfruttare hello `ICommunicationClient` e `ServicePartitionClient` classi, mentre per Java, utilizzare hello `CommunicationClient` e `FabricServicePartitionClient` classi, [per la risoluzione per il servizio, le connessioni HTTP e cicli di ripetizione](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="5b0a5-189">Clients written in C# can leverage hello `ICommunicationClient` and `ServicePartitionClient` classes, whereas for Java, use hello `CommunicationClient` and `FabricServicePartitionClient` classes, [for service resolution, HTTP connections, and retry loops](service-fabric-reliable-services-communication.md).</span></span>
* <span data-ttu-id="5b0a5-190">**WCF**: se si dispone di codice esistente che utilizza il framework di comunicazione WCF, è quindi possibile utilizzare hello `WcfCommunicationListener` sul lato server hello e `WcfCommunicationClient` e `ServicePartitionClient` classi per i client hello.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-190">**WCF**: If you have existing code that uses WCF as your communication framework, then you can use hello `WcfCommunicationListener` for hello server side and `WcfCommunicationClient` and `ServicePartitionClient` classes for hello client.</span></span> <span data-ttu-id="5b0a5-191">Questo comunque è disponibile solo per applicazioni C# in cluster basati su Windows.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-191">This however is only available for C# applications on Windows based clusters.</span></span> <span data-ttu-id="5b0a5-192">Per ulteriori informazioni, vedere l'articolo [implementazione basata su WCF di stack di comunicazione hello](service-fabric-reliable-services-communication-wcf.md).</span><span class="sxs-lookup"><span data-stu-id="5b0a5-192">For more details, see this article about [WCF-based implementation of hello communication stack](service-fabric-reliable-services-communication-wcf.md).</span></span>

## <a name="using-custom-protocols-and-other-communication-frameworks"></a><span data-ttu-id="5b0a5-193">Uso di protocolli personalizzati e altri framework di comunicazione</span><span class="sxs-lookup"><span data-stu-id="5b0a5-193">Using custom protocols and other communication frameworks</span></span>
<span data-ttu-id="5b0a5-194">I servizi possono usare qualsiasi protocollo o framework per le comunicazioni, ad esempio un protocollo binario personalizzato su socket TCP o eventi di streaming tramite l'[Hub eventi di Azure](https://azure.microsoft.com/services/event-hubs/) o l'[Hub IoT di Azure](https://azure.microsoft.com/services/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="5b0a5-194">Services can use any protocol or framework for communication, whether its a custom binary protocol over TCP sockets, or streaming events through [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) or [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/).</span></span> <span data-ttu-id="5b0a5-195">Service Fabric fornisce astrazione comunicazione API che è possibile collegare lo stack di comunicazione, mentre tutti hello toodiscover di lavoro e la connessione da parte dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-195">Service Fabric provides communication APIs that you can plug your communication stack into, while all hello work toodiscover and connect is abstracted from you.</span></span> <span data-ttu-id="5b0a5-196">Vedere l'articolo relativo hello [il modello di comunicazione affidabile servizio](service-fabric-reliable-services-communication.md) per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="5b0a5-196">See this article about hello [Reliable Service communication model](service-fabric-reliable-services-communication.md) for more details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b0a5-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5b0a5-197">Next steps</span></span>
<span data-ttu-id="5b0a5-198">Informazioni su concetti hello e API disponibili in hello [il modello di comunicazione di servizi affidabili](service-fabric-reliable-services-communication.md), quindi iniziare a usare velocemente [comunicazione remota del servizio](service-fabric-reliable-services-communication-remoting.md) o toolearn approfondita come toowrite un listener di comunicazione utilizzando [API Web con OWIN indipendente](service-fabric-reliable-services-communication-webapi.md).</span><span class="sxs-lookup"><span data-stu-id="5b0a5-198">Learn more about hello concepts and APIs available in hello [Reliable Services communication model](service-fabric-reliable-services-communication.md), then get started quickly with [service remoting](service-fabric-reliable-services-communication-remoting.md) or go in-depth toolearn how toowrite a communication listener using [Web API with OWIN self-host](service-fabric-reliable-services-communication-webapi.md).</span></span>

[1]: ./media/service-fabric-connect-and-communicate-with-services/serviceendpoints.png
[2]: ./media/service-fabric-connect-and-communicate-with-services/namingservice.png
[3]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancertopology.png
[4]: ./media/service-fabric-connect-and-communicate-with-services/nodeport.png
[5]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerport.png
[7]: ./media/service-fabric-connect-and-communicate-with-services/distributedservices.png
[8]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerprobe.png
[9]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[10]: ./media/service-fabric-reverseproxy/internal-communication.png
