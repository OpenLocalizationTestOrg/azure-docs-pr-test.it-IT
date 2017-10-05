---
title: Connettersi e comunicare con i servizi in Azure Service Fabric | Documentazione Microsoft
description: Informazioni su come risolvere, connettersi e comunicare con i servizi in Service Fabric.
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
ms.openlocfilehash: 3e61ad19df34c6a57da43e26bd2ab9d7ecdbf98e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="connect-and-communicate-with-services-in-service-fabric"></a><span data-ttu-id="1d22e-103">Connettersi e comunicare con i servizi in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1d22e-103">Connect and communicate with services in Service Fabric</span></span>
<span data-ttu-id="1d22e-104">In Service Fabric un servizio viene eseguito in una posizione nel cluster di Service Fabric, in genere distribuito su più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="1d22e-104">In Service Fabric, a service runs somewhere in a Service Fabric cluster, typically distributed across multiple VMs.</span></span> <span data-ttu-id="1d22e-105">Può essere spostato da una posizione all'altra, dal proprietario del servizio o automaticamente da Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1d22e-105">It can be moved from one place to another, either by the service owner, or automatically by Service Fabric.</span></span> <span data-ttu-id="1d22e-106">I servizi non sono statisticamente associati a un computer o a un indirizzo specifico.</span><span class="sxs-lookup"><span data-stu-id="1d22e-106">Services are not statically tied to a particular machine or address.</span></span>

<span data-ttu-id="1d22e-107">Un'applicazione di Service Fabric è in genere costituita da molti servizi diversi, ognuno dei quali esegue un'attività specializzata.</span><span class="sxs-lookup"><span data-stu-id="1d22e-107">A Service Fabric application is generally composed of many different services, where each service performs a specialized task.</span></span> <span data-ttu-id="1d22e-108">Questi servizi possono comunicare tra loro per formare una funzione completa, ad esempio il rendering di diverse parti di un'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="1d22e-108">These services may communicate with each other to form a complete function, such as rendering different parts of a web application.</span></span> <span data-ttu-id="1d22e-109">Sono inoltre presenti applicazioni client che si connettono ai servizi e comunicano con essi.</span><span class="sxs-lookup"><span data-stu-id="1d22e-109">There are also client applications that connect to and communicate with services.</span></span> <span data-ttu-id="1d22e-110">Questo documento illustra come configurare la comunicazione con e tra i servizi in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1d22e-110">This document discusses how to set up communication with and between your services in Service Fabric.</span></span>

<span data-ttu-id="1d22e-111">Questo video di Microsoft Virtual Academy illustra anche la comunicazione tra servizi: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965"></span><span class="sxs-lookup"><span data-stu-id="1d22e-111">This Microsoft Virtual Academy video also discusses service communication: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965"></span></span>  
<img src="./media/service-fabric-connect-and-communicate-with-services/CommunicationVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="bring-your-own-protocol"></a><span data-ttu-id="1d22e-112">Usare un protocollo personalizzato</span><span class="sxs-lookup"><span data-stu-id="1d22e-112">Bring your own protocol</span></span>
<span data-ttu-id="1d22e-113">Service Fabric semplifica la gestione del ciclo di vita dei servizi ma non prende alcuna decisione sulle operazioni che devono essere eseguite dai servizi, incluse le comunicazioni.</span><span class="sxs-lookup"><span data-stu-id="1d22e-113">Service Fabric helps manage the lifecycle of your services but it does not make decisions about what your services do.</span></span> <span data-ttu-id="1d22e-114">incluse le comunicazioni.</span><span class="sxs-lookup"><span data-stu-id="1d22e-114">This includes communication.</span></span> <span data-ttu-id="1d22e-115">Quando il servizio viene aperto da Service Fabric, può configurare un endpoint per le richieste in ingresso, usando qualsiasi protocollo o stack di comunicazione.</span><span class="sxs-lookup"><span data-stu-id="1d22e-115">When your service is opened by Service Fabric, that's your service's opportunity to set up an endpoint for incoming requests, using whatever protocol or communication stack you want.</span></span> <span data-ttu-id="1d22e-116">Il servizio rimarrà in ascolto su un indirizzo **IP:porta** normale usando qualsiasi schema di indirizzamento, ad esempio un URI.</span><span class="sxs-lookup"><span data-stu-id="1d22e-116">Your service will listen on a normal **IP:port** address using any addressing scheme, such as a URI.</span></span> <span data-ttu-id="1d22e-117">In questo caso, dovranno usare porte diverse o un meccanismo di condivisione di porte, ad esempio il driver del kernel http.sys in Windows.</span><span class="sxs-lookup"><span data-stu-id="1d22e-117">Multiple service instances or replicas may share a host process, in which case they will either need to use different ports or use a port-sharing mechanism, such as the http.sys kernel driver in Windows.</span></span> <span data-ttu-id="1d22e-118">In entrambi i casi, ogni istanza o replica del servizio in un processo host deve essere indirizzabile in modo univoco.</span><span class="sxs-lookup"><span data-stu-id="1d22e-118">In either case, each service instance or replica in a host process must be uniquely addressable.</span></span>

![Endpoint del servizio][1]

## <a name="service-discovery-and-resolution"></a><span data-ttu-id="1d22e-120">Individuazione e risoluzione del servizio</span><span class="sxs-lookup"><span data-stu-id="1d22e-120">Service discovery and resolution</span></span>
<span data-ttu-id="1d22e-121">In un sistema distribuito è possibile che i servizi si spostino da un computer a un altro nel tempo</span><span class="sxs-lookup"><span data-stu-id="1d22e-121">In a distributed system, services may move from one machine to another over time.</span></span> <span data-ttu-id="1d22e-122">per vari motivi, incluso il bilanciamento delle risorse, aggiornamenti, failover o aumento del numero di istanze.</span><span class="sxs-lookup"><span data-stu-id="1d22e-122">This can happen for various reasons, including resource balancing, upgrades, failovers, or scale-out.</span></span> <span data-ttu-id="1d22e-123">Gli indirizzi dell'endpoint di servizio subiscono quindi modifiche quando il servizio si sposta in nodi con indirizzi IP diversi ed è possibile che si aprano su porte diverse se il servizio usa una porta selezionata in modo dinamico.</span><span class="sxs-lookup"><span data-stu-id="1d22e-123">This means service endpoint addresses change as the service moves to nodes with different IP addresses, and may open on different ports if the service uses a dynamically selected port.</span></span>

![Distribuzione dei servizi][7]

<span data-ttu-id="1d22e-125">Service Fabric offre un servizio di individuazione e risoluzione denominato servizio Naming.</span><span class="sxs-lookup"><span data-stu-id="1d22e-125">Service Fabric provides a discovery and resolution service called the Naming Service.</span></span> <span data-ttu-id="1d22e-126">Il servizio Naming gestisce una tabella che esegue il mapping delle istanze del servizio denominato agli indirizzi dell'endpoint su cui rimangono in ascolto.</span><span class="sxs-lookup"><span data-stu-id="1d22e-126">The Naming Service maintains a table that maps named service instances to the endpoint addresses they listen on.</span></span> <span data-ttu-id="1d22e-127">Tutte le istanze del servizio denominato in Service Fabric hanno nomi univoci rappresentati come URI, ad esempio `"fabric:/MyApplication/MyService"`.</span><span class="sxs-lookup"><span data-stu-id="1d22e-127">All named service instances in Service Fabric have unique names represented as URIs, for example, `"fabric:/MyApplication/MyService"`.</span></span> <span data-ttu-id="1d22e-128">Il nome del servizio non cambia per tutta la durata del servizio. Solo gli indirizzi dell'endpoint possono essere modificati quando i servizi si spostano.</span><span class="sxs-lookup"><span data-stu-id="1d22e-128">The name of the service does not change over the lifetime of the service, it's only the endpoint addresses that can change when services move.</span></span> <span data-ttu-id="1d22e-129">analogamente ai siti Web che hanno URL costanti, ma il cui indirizzo IP può cambiare.</span><span class="sxs-lookup"><span data-stu-id="1d22e-129">This is analogous to websites that have constant URLs but where the IP address may change.</span></span> <span data-ttu-id="1d22e-130">Analogamente a DNS sul Web, che risolve URL di siti Web in indirizzi IP, Service Fabric ha un registrar che esegue il mapping dei nomi di servizio ai rispettivi indirizzi di endpoint.</span><span class="sxs-lookup"><span data-stu-id="1d22e-130">And similar to DNS on the web, which resolves website URLs to IP addresses, Service Fabric has a registrar that maps service names to their endpoint address.</span></span>

![Endpoint del servizio][2]

<span data-ttu-id="1d22e-132">La risoluzione e la connessione ai servizi prevedono l'esecuzione in ciclo dei passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1d22e-132">Resolving and connecting to services involves the following steps run in a loop:</span></span>

* <span data-ttu-id="1d22e-133">**Risoluzione**: ottenere dal servizio Naming l'endpoint pubblicato da un servizio.</span><span class="sxs-lookup"><span data-stu-id="1d22e-133">**Resolve**: Get the endpoint that a service has published from the Naming Service.</span></span>
* <span data-ttu-id="1d22e-134">**Connessione**: connettersi al servizio sul protocollo usato nell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="1d22e-134">**Connect**: Connect to the service over whatever protocol it uses on that endpoint.</span></span>
* <span data-ttu-id="1d22e-135">**Ripetizione dei tentativi**: è possibile che un tentativo di connessione abbia esito negativo per svariati motivi, ad esempio se il servizio si è spostato dopo l'ultima risoluzione dell'indirizzo dell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="1d22e-135">**Retry**: A connection attempt may fail for any number of reasons, for example if the service has moved since the last time the endpoint address was resolved.</span></span> <span data-ttu-id="1d22e-136">In questo caso, è necessario provare a ripetere i passaggi precedenti di risoluzione e connessione e il ciclo viene ripetuto finché la connessione non riesce.</span><span class="sxs-lookup"><span data-stu-id="1d22e-136">In that case, the preceding resolve and connect steps need to be retried, and this cycle is repeated until the connection succeeds.</span></span>

## <a name="connecting-to-other-services"></a><span data-ttu-id="1d22e-137">Connessione ad altri servizi</span><span class="sxs-lookup"><span data-stu-id="1d22e-137">Connecting to other services</span></span>
<span data-ttu-id="1d22e-138">I servizi che si connettono tra loro in un cluster possono in genere accedere direttamente agli endpoint di altri servizi perché i nodi di un cluster si trovano nella stessa rete locale.</span><span class="sxs-lookup"><span data-stu-id="1d22e-138">Services connecting to each other inside a cluster generally can directly access the endpoints of other services because the nodes in a cluster are on the same local network.</span></span> <span data-ttu-id="1d22e-139">Per facilitare la connessione tra servizi, Service Fabric offre servizi aggiuntivi che usano Naming Service,</span><span class="sxs-lookup"><span data-stu-id="1d22e-139">To make is easier to connect between services, Service Fabric provides additional services that use the Naming Service.</span></span> <span data-ttu-id="1d22e-140">un servizio DNS e un servizio di proxy inverso.</span><span class="sxs-lookup"><span data-stu-id="1d22e-140">A DNS service and a reverse proxy service.</span></span>


### <a name="dns-service"></a><span data-ttu-id="1d22e-141">Servizio DNS</span><span class="sxs-lookup"><span data-stu-id="1d22e-141">DNS service</span></span>
<span data-ttu-id="1d22e-142">Poiché molti servizi, in particolare quelli in contenitori, possono avere un nome di URL esistente, la possibilità di risolverli usando il protocollo DNS standard, anziché il protocollo Naming Service, è molto utile, in particolare negli scenari di applicazioni "lift-and-shift".</span><span class="sxs-lookup"><span data-stu-id="1d22e-142">Since many services, especially containerized services, can have an existing URL name, being able to resolve these using the standard DNS protocol (rather than the Naming Service protocol) is very convenient, especially in application "lift and shift" scenarios.</span></span> <span data-ttu-id="1d22e-143">Questo è esattamente ciò che fa il servizio DNS.</span><span class="sxs-lookup"><span data-stu-id="1d22e-143">This is exactly what the DNS service does.</span></span> <span data-ttu-id="1d22e-144">Consente di eseguire il mapping di nomi DNS a nomi di servizi e di conseguenza di risolvere gli indirizzi IP degli endpoint.</span><span class="sxs-lookup"><span data-stu-id="1d22e-144">It enables you to map DNS names to a service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="1d22e-145">Come mostrato nel diagramma seguente, il servizio DNS, in esecuzione sul cluster di Service Fabric, esegue il mapping dei nomi DNS ai nomi dei servizi, che vengono quindi risolti da Naming Service per restituire gli indirizzi degli endpoint a cui connettersi.</span><span class="sxs-lookup"><span data-stu-id="1d22e-145">As shown in the following diagram, the DNS service, running in the Service Fabric cluster, maps DNS names to service names which are then resolved by the Naming Service to return the endpoint addresses to connect to.</span></span> <span data-ttu-id="1d22e-146">Il nome DNS per il servizio viene fornito al momento della creazione.</span><span class="sxs-lookup"><span data-stu-id="1d22e-146">The DNS name for the service is provided at the time of creation.</span></span> 

![Endpoint del servizio][9]

<span data-ttu-id="1d22e-148">Per altre informazioni su come usare il servizio DNS, vedere l'articolo [DNS service in Azure Service Fabric](service-fabric-dnsservice.md) (Servizio DNS in Azure Service Fabric).</span><span class="sxs-lookup"><span data-stu-id="1d22e-148">For more details on how to use the DNS service see [DNS service in Azure Service Fabric](service-fabric-dnsservice.md) article.</span></span>

### <a name="reverse-proxy-service"></a><span data-ttu-id="1d22e-149">Servizio di proxy inverso</span><span class="sxs-lookup"><span data-stu-id="1d22e-149">Reverse proxy service</span></span>
<span data-ttu-id="1d22e-150">Il proxy inverso indirizza i servizi presenti nel cluster che espongono endpoint HTTP, incluso HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1d22e-150">The reverse proxy addresses services in the cluster that exposes HTTP endpoints including HTTPS.</span></span> <span data-ttu-id="1d22e-151">Il proxy inverso semplifica in misura significativa la chiamata di altri servizi e dei relativi metodi grazie alla disponibilità di un formato URI specifico. Gestisce inoltre i passaggi di risoluzione, connessione e ripetizione necessari per consentire a un servizio di comunicare con un altro servizio mediante Naming Serivce.</span><span class="sxs-lookup"><span data-stu-id="1d22e-151">The reverse proxy greatly simplifies calling other services and their methods by having a specific URI format and handles the resolve, connect, retry steps required for one service to communicate with another using the Naming Serivce.</span></span> <span data-ttu-id="1d22e-152">In altri termini, durante la chiamata di altri servizi nasconde Naming Service all'utente, rendendo l'operazione semplice quanto la chiamata a un URL.</span><span class="sxs-lookup"><span data-stu-id="1d22e-152">In other words, it hides the Naming Service from you when calling other services by making this as simple as calling a URL.</span></span>

![Endpoint del servizio][10]

<span data-ttu-id="1d22e-154">Per altre informazioni su come usare il servizio di proxy inverso, vedere l'articolo [Proxy inverso in Azure Service Fabric](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="1d22e-154">For more details on how to use the reverse proxy service see [Reverse proxy in Azure Service Fabric](service-fabric-reverseproxy.md) article.</span></span>

## <a name="connections-from-external-clients"></a><span data-ttu-id="1d22e-155">Connessioni da client esterni</span><span class="sxs-lookup"><span data-stu-id="1d22e-155">Connections from external clients</span></span>
<span data-ttu-id="1d22e-156">I servizi che si connettono tra loro in un cluster possono in genere accedere direttamente agli endpoint di altri servizi perché i nodi di un cluster si trovano nella stessa rete locale.</span><span class="sxs-lookup"><span data-stu-id="1d22e-156">Services connecting to each other inside a cluster generally can directly access the endpoints of other services because the nodes in a cluster are on the same local network.</span></span> <span data-ttu-id="1d22e-157">In alcuni ambienti, tuttavia, è possibile che un cluster si trovi dietro un servizio di bilanciamento del carico che indirizza il traffico esterno in ingresso attraverso un set limitato di porte.</span><span class="sxs-lookup"><span data-stu-id="1d22e-157">In some environments, however, a cluster may be behind a load balancer that routes external ingress traffic through a limited set of ports.</span></span> <span data-ttu-id="1d22e-158">In questi casi, i servizi possono comunicare comunque tra di loro e risolvere gli indirizzi usando il servizio Naming, ma sono necessari passaggi aggiuntivi per consentire ai client esterni di connettersi ai servizi.</span><span class="sxs-lookup"><span data-stu-id="1d22e-158">In these cases, services can still communicate with each other and resolve addresses using the Naming Service, but extra steps must be taken to allow external clients to connect to services.</span></span>

## <a name="service-fabric-in-azure"></a><span data-ttu-id="1d22e-159">Service Fabric in Azure</span><span class="sxs-lookup"><span data-stu-id="1d22e-159">Service Fabric in Azure</span></span>
<span data-ttu-id="1d22e-160">Un cluster di Service Fabric in Azure viene posizionato dietro un servizio di bilanciamento del carico di Azure.</span><span class="sxs-lookup"><span data-stu-id="1d22e-160">A Service Fabric cluster in Azure is placed behind an Azure Load Balancer.</span></span> <span data-ttu-id="1d22e-161">Tutto il traffico esterno verso il cluster deve passare attraverso il servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="1d22e-161">All external traffic to the cluster must pass through the load balancer.</span></span> <span data-ttu-id="1d22e-162">Il servizio di bilanciamento del carico inoltrerà automaticamente il traffico in ingresso su una porta specifica verso un *nodo* casuale che ha la stessa porta aperta.</span><span class="sxs-lookup"><span data-stu-id="1d22e-162">The load balancer will automatically forward traffic inbound on a given port to a random *node* that has the same port open.</span></span> <span data-ttu-id="1d22e-163">Il servizio di bilanciamento del carico di Azure riconosce solo le porte aperte sui *nodi*, non le porte aperte dai singoli *servizi*.</span><span class="sxs-lookup"><span data-stu-id="1d22e-163">The Azure Load Balancer only knows about ports open on the *nodes*, it does not know about ports open by individual *services*.</span></span>

![Servizio di bilanciamento del carico di Azure e topologia di Service Fabric][3]

<span data-ttu-id="1d22e-165">Ad esempio, per accettare il traffico esterno sulla porta **80**, è necessario configurare gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1d22e-165">For example, in order to accept external traffic on port **80**, the following things must be configured:</span></span>

1. <span data-ttu-id="1d22e-166">Scrivere un servizio che resta in ascolto sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="1d22e-166">Write a service that listens on port 80.</span></span> <span data-ttu-id="1d22e-167">Configurare la porta 80 nel file ServiceManifest.xml del servizio e aprire un listener nel servizio, ad esempio un server Web self-hosted.</span><span class="sxs-lookup"><span data-stu-id="1d22e-167">Configure port 80 in the service's ServiceManifest.xml and open a listener in the service, for example, a self-hosted web server.</span></span>

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
2. <span data-ttu-id="1d22e-168">Creare un cluster di Service Fabric in Azure e specificare la porta **80** come porta di endpoint personalizzata per il tipo di nodo che ospiterà il servizio.</span><span class="sxs-lookup"><span data-stu-id="1d22e-168">Create a Service Fabric Cluster in Azure and specify port **80** as a custom endpoint port for the node type that will host the service.</span></span> <span data-ttu-id="1d22e-169">Se sono presenti più tipi di nodo, è possibile configurare un *vincolo di posizionamento* sul servizio per assicurare che venga eseguito solo sul tipo di nodo con la porta di endpoint personalizzata aperta.</span><span class="sxs-lookup"><span data-stu-id="1d22e-169">If you have more than one node type, you can set up a *placement constraint* on the service to ensure it only runs on the node type that has the custom endpoint port opened.</span></span>

    ![Apertura di una porta su un tipo di nodo][4]
3. <span data-ttu-id="1d22e-171">Dopo la creazione del cluster, configurare il servizio di bilanciamento del carico di Azure nel gruppo di risorse del cluster per inoltrare il traffico sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="1d22e-171">Once the cluster has been created, configure the Azure Load Balancer in the cluster's Resource Group to forward traffic on port 80.</span></span> <span data-ttu-id="1d22e-172">Quando si crea un cluster tramite il portale di Azure, il cluster viene configurato automaticamente per ogni porta di endpoint personalizzata configurata.</span><span class="sxs-lookup"><span data-stu-id="1d22e-172">When creating a cluster through the Azure portal, this is set up automatically for each custom endpoint port that was configured.</span></span>

    ![Inoltro di traffico nel servizio di bilanciamento del carico di Azure][5]
4. <span data-ttu-id="1d22e-174">Il servizio di bilanciamento del carico di Azure usa un probe per determinare se inviare o meno il traffico a un nodo specifico.</span><span class="sxs-lookup"><span data-stu-id="1d22e-174">The Azure Load Balancer uses a probe to determine whether or not to send traffic to a particular node.</span></span> <span data-ttu-id="1d22e-175">Il probe controlla periodicamente un endpoint su ogni nodo per determinare se il nodo risponde o meno.</span><span class="sxs-lookup"><span data-stu-id="1d22e-175">The probe periodically checks an endpoint on each node to determine whether or not the node is responding.</span></span> <span data-ttu-id="1d22e-176">Se il probe non riesce a ricevere una risposta dopo un numero configurato di volte, il servizio di bilanciamento del carico smette di inviare traffico a quel nodo.</span><span class="sxs-lookup"><span data-stu-id="1d22e-176">If the probe fails to receive a response after a configured number of times, the load balancer stops sending traffic to that node.</span></span> <span data-ttu-id="1d22e-177">Quando si crea un cluster tramite il portale di Azure, viene configurato automaticamente un probe per ogni porta di endpoint personalizzata configurata.</span><span class="sxs-lookup"><span data-stu-id="1d22e-177">When creating a cluster through the Azure portal, a probe is automatically set up for each custom endpoint port that was configured.</span></span>

    ![Inoltro di traffico nel servizio di bilanciamento del carico di Azure][8]

<span data-ttu-id="1d22e-179">È importante ricordare che il servizio di bilanciamento del carico di Azure e il probe riconoscono solo i *nodi*, non i *servizi* in esecuzione sui nodi.</span><span class="sxs-lookup"><span data-stu-id="1d22e-179">It's important to remember that the Azure Load Balancer and the probe only know about the *nodes*, not the *services* running on the nodes.</span></span> <span data-ttu-id="1d22e-180">Il servizio di bilanciamento del carico di Azure invierà sempre il traffico ai nodi che rispondono al probe, quindi occorre assicurarsi che i servizi siano disponibili sui nodi che sono in grado di rispondere al probe.</span><span class="sxs-lookup"><span data-stu-id="1d22e-180">The Azure Load Balancer will always send traffic to nodes that respond to the probe, so care must be taken to ensure services are available on the nodes that are able to respond to the probe.</span></span>

## <a name="reliable-services-built-in-communication-api-options"></a><span data-ttu-id="1d22e-181">Reliable Services: opzioni predefinite per l'API di comunicazione</span><span class="sxs-lookup"><span data-stu-id="1d22e-181">Reliable Services: Built-in communication API options</span></span>
<span data-ttu-id="1d22e-182">Il framework Reliable Services include alcune opzioni di comunicazione predefinite.</span><span class="sxs-lookup"><span data-stu-id="1d22e-182">The Reliable Services framework ships with several pre-built communication options.</span></span> <span data-ttu-id="1d22e-183">la cui scelta dipende dal modello di programmazione adottato, dal framework di comunicazione e dal linguaggio di programmazione usato per scrivere i servizi.</span><span class="sxs-lookup"><span data-stu-id="1d22e-183">The decision about which one will work best for you depends on the choice of the programming model, the communication framework, and the programming language that your services are written in.</span></span>

* <span data-ttu-id="1d22e-184">**Nessun protocollo specifico:** se non si ha una preferenza particolare per il framework di comunicazione, ma si vuole essere immediatamente operativi, l'opzione ideale è costituita dalle [comunicazioni remote del servizio](service-fabric-reliable-services-communication-remoting.md), che consentono chiamate a procedure remote fortemente tipizzate per Reliable Services e Reliable Actors.</span><span class="sxs-lookup"><span data-stu-id="1d22e-184">**No specific protocol:**  If you don't have a particular choice of communication framework, but you want to get something up and running quickly, then the ideal option for you is [service remoting](service-fabric-reliable-services-communication-remoting.md), which allows strongly-typed remote procedure calls for Reliable Services and Reliable Actors.</span></span> <span data-ttu-id="1d22e-185">Questo è il modo più semplice e veloce per iniziare a comunicare con i servizi.</span><span class="sxs-lookup"><span data-stu-id="1d22e-185">This is the easiest and fastest way to get started with service communication.</span></span> <span data-ttu-id="1d22e-186">Le comunicazioni remote del servizio gestiscono la risoluzione degli indirizzi del servizio, la connessione, la ripetizione dei tentativi e la gestione degli errori.</span><span class="sxs-lookup"><span data-stu-id="1d22e-186">Service remoting handles resolution of service addresses, connection, retry, and error handling.</span></span> <span data-ttu-id="1d22e-187">Questo è disponibile sia per applicazioni C# che per applicazioni Java.</span><span class="sxs-lookup"><span data-stu-id="1d22e-187">This is available for both C# and Java applications.</span></span>
* <span data-ttu-id="1d22e-188">**HTTP**: per comunicazioni indipendenti dal linguaggio, HTTP costituisce la scelta standard di settore, con strumenti e server HTTP disponibili in molti linguaggi diversi, tutti supportati da Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1d22e-188">**HTTP**: For language-agnostic communication, HTTP provides an industry-standard choice with tools and HTTP servers available in many different languages, all supported by Service Fabric.</span></span> <span data-ttu-id="1d22e-189">I servizi possono usare qualsiasi stack HTTP disponibile, inclusa l'[API Web ASP.NET](service-fabric-reliable-services-communication-webapi.md) per applicazioni C#.</span><span class="sxs-lookup"><span data-stu-id="1d22e-189">Services can use any HTTP stack available, including [ASP.NET Web API](service-fabric-reliable-services-communication-webapi.md) for C# applications.</span></span> <span data-ttu-id="1d22e-190">I client scritti in C# possono sfruttare le classi `ICommunicationClient` e `ServicePartitionClient`. Per Java usare invece le classi `CommunicationClient` e `FabricServicePartitionClient` [per la risoluzione del servizio, le connessioni HTTP e i cicli di ripetizione dei tentativi](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="1d22e-190">Clients written in C# can leverage the `ICommunicationClient` and `ServicePartitionClient` classes, whereas for Java, use the `CommunicationClient` and `FabricServicePartitionClient` classes, [for service resolution, HTTP connections, and retry loops](service-fabric-reliable-services-communication.md).</span></span>
* <span data-ttu-id="1d22e-191">**WCF**: se il codice esistente usa WCF come framework di comunicazione, è possibile scegliere `WcfCommunicationListener` per il lato server e le classi `WcfCommunicationClient` e `ServicePartitionClient` per il client.</span><span class="sxs-lookup"><span data-stu-id="1d22e-191">**WCF**: If you have existing code that uses WCF as your communication framework, then you can use the `WcfCommunicationListener` for the server side and `WcfCommunicationClient` and `ServicePartitionClient` classes for the client.</span></span> <span data-ttu-id="1d22e-192">Questo comunque è disponibile solo per applicazioni C# in cluster basati su Windows.</span><span class="sxs-lookup"><span data-stu-id="1d22e-192">This however is only available for C# applications on Windows based clusters.</span></span> <span data-ttu-id="1d22e-193">Per altre informazioni, vedere l'articolo [Stack di comunicazione basato su WCF per Reliable Services](service-fabric-reliable-services-communication-wcf.md).</span><span class="sxs-lookup"><span data-stu-id="1d22e-193">For more details, see this article about [WCF-based implementation of the communication stack](service-fabric-reliable-services-communication-wcf.md).</span></span>

## <a name="using-custom-protocols-and-other-communication-frameworks"></a><span data-ttu-id="1d22e-194">Uso di protocolli personalizzati e altri framework di comunicazione</span><span class="sxs-lookup"><span data-stu-id="1d22e-194">Using custom protocols and other communication frameworks</span></span>
<span data-ttu-id="1d22e-195">I servizi possono usare qualsiasi protocollo o framework per le comunicazioni, ad esempio un protocollo binario personalizzato su socket TCP o eventi di streaming tramite l'[Hub eventi di Azure](https://azure.microsoft.com/services/event-hubs/) o l'[Hub IoT di Azure](https://azure.microsoft.com/services/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="1d22e-195">Services can use any protocol or framework for communication, whether its a custom binary protocol over TCP sockets, or streaming events through [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) or [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/).</span></span> <span data-ttu-id="1d22e-196">Service Fabric fornisce API di comunicazione a cui è possibile collegare lo stack di comunicazione, mentre tutte le operazioni di individuazione e connessione vengono eseguite in modo indipendente dall'utente.</span><span class="sxs-lookup"><span data-stu-id="1d22e-196">Service Fabric provides communication APIs that you can plug your communication stack into, while all the work to discover and connect is abstracted from you.</span></span> <span data-ttu-id="1d22e-197">Per altre informazioni, vedere l'articolo [Modello di comunicazione Reliable Service](service-fabric-reliable-services-communication.md) .</span><span class="sxs-lookup"><span data-stu-id="1d22e-197">See this article about the [Reliable Service communication model](service-fabric-reliable-services-communication.md) for more details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d22e-198">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1d22e-198">Next steps</span></span>
<span data-ttu-id="1d22e-199">Per altre informazioni sui concetti e sulle API disponibili, vedere il [modello di comunicazione di Reliable Services](service-fabric-reliable-services-communication.md), quindi iniziare subito a usare le [del servizio](service-fabric-reliable-services-communication-remoting.md) oppure ottenere informazioni approfondite su come scrivere un listener di comunicazione usando l'[API Web con self-hosting OWIN](service-fabric-reliable-services-communication-webapi.md).</span><span class="sxs-lookup"><span data-stu-id="1d22e-199">Learn more about the concepts and APIs available in the [Reliable Services communication model](service-fabric-reliable-services-communication.md), then get started quickly with [service remoting](service-fabric-reliable-services-communication-remoting.md) or go in-depth to learn how to write a communication listener using [Web API with OWIN self-host](service-fabric-reliable-services-communication-webapi.md).</span></span>

[1]: ./media/service-fabric-connect-and-communicate-with-services/serviceendpoints.png
[2]: ./media/service-fabric-connect-and-communicate-with-services/namingservice.png
[3]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancertopology.png
[4]: ./media/service-fabric-connect-and-communicate-with-services/nodeport.png
[5]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerport.png
[7]: ./media/service-fabric-connect-and-communicate-with-services/distributedservices.png
[8]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerprobe.png
[9]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[10]: ./media/service-fabric-reverseproxy/internal-communication.png
