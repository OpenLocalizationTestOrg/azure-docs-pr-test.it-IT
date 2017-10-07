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
# <a name="connect-and-communicate-with-services-in-service-fabric"></a>Connettersi e comunicare con i servizi in Service Fabric
In Service Fabric un servizio viene eseguito in una posizione nel cluster di Service Fabric, in genere distribuito su più macchine virtuali. Può essere spostato da un'unica posizione tooanother, dal proprietario del servizio hello o automaticamente dall'infrastruttura del servizio. Servizi non sono collegati in modo statico tooa specifico computer o l'indirizzo.

Un'applicazione di Service Fabric è in genere costituita da molti servizi diversi, ognuno dei quali esegue un'attività specializzata. Questi servizi possono comunicare tra loro tooform una funzione completa, ad esempio parti diverse di rendering di un'applicazione web. Sono disponibili anche le applicazioni che si connettono tooand comunicano con i servizi client. Questo documento vengono illustrate come tooset delle comunicazioni con e tra i servizi di Service Fabric.

Questo video di Microsoft Virtual Academy illustra anche la comunicazione tra servizi: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965">  
<img src="./media/service-fabric-connect-and-communicate-with-services/CommunicationVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="bring-your-own-protocol"></a>Usare un protocollo personalizzato
Service Fabric aiuta a gestire il ciclo di vita di hello dei servizi, ma non apporta le decisioni sulle operazioni dei servizi. incluse le comunicazioni. Quando il servizio viene aperto dall'infrastruttura di servizio, ovvero tooset opportunità del servizio backup di un endpoint per le richieste in ingresso, utilizzando qualsiasi stack di comunicazione o di protocollo desiderato. Il servizio rimarrà in ascolto su un indirizzo **IP:porta** normale usando qualsiasi schema di indirizzamento, ad esempio un URI. Più istanze del servizio o repliche possono condividere un processo host, nel qual caso viene verrà necessita di porte diverse toouse o utilizzare un meccanismo di condivisione delle porte, ad esempio driver di kernel hello http.sys in Windows. In entrambi i casi, ogni istanza o replica del servizio in un processo host deve essere indirizzabile in modo univoco.

![Endpoint del servizio][1]

## <a name="service-discovery-and-resolution"></a>Individuazione e risoluzione del servizio
In un sistema distribuito, servizi possono spostarsi da una macchina tooanother nel tempo. per vari motivi, incluso il bilanciamento delle risorse, aggiornamenti, failover o aumento del numero di istanze. Ciò significa che gli indirizzi degli endpoint di servizio modificare come servizio hello Sposta toonodes con indirizzi IP diversi e può aprire su porte diverse se il servizio di hello utilizza una porta selezionata in modo dinamico.

![Distribuzione dei servizi][7]

Service Fabric fornisce un rilevamento e la chiamata del servizio di risoluzione hello Naming Service. Hello Naming Service mantiene una tabella in cui viene eseguito il mapping denominato le istanze del servizio sono in ascolto su toohello indirizzi dell'endpoint. Tutte le istanze del servizio denominato in Service Fabric hanno nomi univoci rappresentati come URI, ad esempio `"fabric:/MyApplication/MyService"`. nome Hello del servizio di hello non cambia nel corso della durata del servizio hello hello, solo gli indirizzi endpoint hello che possono cambiare quando sposta servizi. Si tratta di toowebsites analoga che dispongono di URL costante, ma in cui è possibile modificare l'indirizzo IP hello. TooDNS simile nel web hello, che risolve gli URL tooIP indirizzi dei siti Web, Service Fabric è un registrar che esegue il mapping indirizzo endpoint del servizio nomi tootheir.

![Endpoint del servizio][2]

Risoluzione e la connessione tooservices comporta hello seguendo i passaggi eseguiti in un ciclo:

* **Risolvere**: endpoint hello Get che un servizio pubblicato da hello Naming Service.
* **Connettersi**: servizio toohello di connettersi tramite il protocollo viene utilizzato tale endpoint.
* **Ripetere**: un tentativo di connessione potrebbe non riuscire per diversi motivi, ad esempio se il servizio di hello è stato spostato dall'indirizzo endpoint hello hello ultima ora è stato risolto. In tal caso, hello precedente risoluzione e connettersi toobe ritentata necessario passaggi e il ciclo viene ripetuto fino a quando non hello connessione ha esito positivo.

## <a name="connecting-tooother-services"></a>La connessione di servizi tooother
Servizi che si connettono tooeach altro all'interno di un cluster in genere possibile accedere direttamente a endpoint hello di altri servizi poiché nodi hello in un cluster si trovano in hello stessa rete locale. toomake è più facile tooconnect tra servizi, Service Fabric fornisce altri servizi che utilizzano hello Naming Service. un servizio DNS e un servizio di proxy inverso.


### <a name="dns-service"></a>Servizio DNS
Poiché molti servizi, in particolare nei contenitori, possono avere un nome URL esistente, viene tooresolve in grado di utilizzare hello protocollo DNS standard (anziché il protocollo di Naming Service hello) è molto utile, soprattutto nell'applicazione "accuratezza e shift" scenari. Questo è esattamente il servizio DNS hello. Consente di toomap nomi tooa servizio nome DNS e quindi risolvere indirizzi IP degli endpoint. 

Come hello illustrato nel diagramma seguente, hello servizio DNS, in esecuzione nel cluster di Service Fabric hello, esegue il mapping nomi tooservice dei nomi DNS vengono risolte quindi hello Naming Service tooreturn hello endpoint indirizzi tooconnect per. nome DNS Hello hello servizio viene fornito al momento di hello della creazione. 

![Endpoint del servizio][9]

Per ulteriori informazioni su come toouse hello servizio DNS vedere [servizio DNS in Azure Service Fabric](service-fabric-dnsservice.md) articolo.

### <a name="reverse-proxy-service"></a>Servizio di proxy inverso
proxy inverso Hello indirizzi servizi in cluster hello che espone gli endpoint HTTP inclusi HTTPS. proxy inverso Hello semplifica notevolmente la chiamata di altri servizi e i relativi metodi con uno specifico formato URI hello risolvere, gli handle di connessione, passaggi ripetizione necessari per toocommunicate un servizio con un altro utilizzando hello servizio di denominazione. In altre parole, nasconde hello Naming Service da parte dell'utente quando si chiama altri servizi, eseguendo questo semplice come la chiamata a un URL.

![Endpoint del servizio][10]

Per ulteriori informazioni su come toouse hello inversa servizio proxy vedere [inverso in Azure Service Fabric](service-fabric-reverseproxy.md) articolo.

## <a name="connections-from-external-clients"></a>Connessioni da client esterni
Servizi che si connettono tooeach altro all'interno di un cluster in genere possibile accedere direttamente a endpoint hello di altri servizi poiché nodi hello in un cluster si trovano in hello stessa rete locale. In alcuni ambienti, tuttavia, è possibile che un cluster si trovi dietro un servizio di bilanciamento del carico che indirizza il traffico esterno in ingresso attraverso un set limitato di porte. In questi casi, possono comunque comunicare tra loro e risolvere gli indirizzi tramite hello Naming Service, ma passaggi aggiuntivi devono essere prese tooallow client esterni tooconnect tooservices.

## <a name="service-fabric-in-azure"></a>Service Fabric in Azure
Un cluster di Service Fabric in Azure viene posizionato dietro un servizio di bilanciamento del carico di Azure. Tutti i cluster toohello traffico esterno deve passare tramite servizio di bilanciamento del carico hello. Hello bilanciamento del carico verrà automaticamente inoltrare il traffico in entrata per tooa una determinata porta casuale *nodo* con hello aprire stessa porta. Hello bilanciamento del carico di Azure riconosce solo sulle porte aperte sul hello *nodi*, non è a conoscenza sull'apertura delle porte per singoli *servizi*.

![Servizio di bilanciamento del carico di Azure e topologia di Service Fabric][3]

Ad esempio, in ordine tooaccept il traffico di esterno sulla porta **80**, deve essere configurato hello seguenti operazioni:

1. Scrivere un servizio che resta in ascolto sulla porta 80. Configurare la porta 80 in ServiceManifest.xml del servizio hello e aprire un listener nel servizio di hello, ad esempio, un server web self-hosted.

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
2. Creare un Cluster di Service Fabric in Azure e specificare la porta **80** come una porta dell'endpoint personalizzato per il tipo di nodo hello che ospiterà il servizio di hello. Se si dispone di più di un tipo di nodo, è possibile impostare un *vincoli di posizionamento* su tooensure servizio hello viene eseguito solo sul tipo di nodo hello dotato di porta dell'endpoint personalizzata hello aperto.

    ![Apertura di una porta su un tipo di nodo][4]
3. Dopo aver creato il cluster hello, configurare hello Azure servizio di bilanciamento del carico del traffico tooforward gruppo di risorse del cluster hello sulla porta 80. Quando si crea un cluster tramite hello portale di Azure, questo viene configurato automaticamente per ogni porta di endpoint personalizzato che è stato configurato.

    ![Inoltrare il traffico in hello bilanciamento del carico di Azure][5]
4. Hello se viene utilizzato il bilanciamento del carico Azure toodetermine un probe o non toosend traffico tooa determinato nodo. periodicamente Hello probe controlli di un endpoint in ogni nodo di toodetermine o meno risponde nodo hello. Caso di probe hello tooreceive una risposta dopo un numero di volte configurato, bilanciamento del carico hello interrompe l'invio di nodo toothat traffico. Quando si crea un cluster tramite hello portale di Azure, un probe viene automaticamente configurato per ogni porta di endpoint personalizzato che è stato configurato.

    ![Inoltrare il traffico in hello bilanciamento del carico di Azure][8]

È importante tooremember che hello bilanciamento del carico di Azure e un probe hello riconosce solo hello *nodi*, non hello *servizi* in esecuzione in nodi hello. Hello bilanciamento del carico di Azure inviano sempre toonodes di traffico che rispondono toohello probe, pertanto prestare attenzione tooensure services sono disponibili nei nodi hello che sono in grado di toorespond toohello probe.

## <a name="reliable-services-built-in-communication-api-options"></a>Reliable Services: opzioni predefinite per l'API di comunicazione
framework servizi affidabili Hello viene fornito con diverse opzioni di comunicazione preesistente. su quali uno più adatta per la decisione di Hello dipende dalla scelta hello del modello di programmazione, il framework di comunicazione hello e i servizi vengono scritti nel linguaggio di programmazione hello hello.

* **Nessun protocollo specifico:** se non si dispone di una particolare scelta del framework di comunicazione, ma si desidera tooget qualcosa di attivare ed eseguire rapidamente, sarà hello ideale dell'opzione [comunicazione remota del servizio](service-fabric-reliable-services-communication-remoting.md), che consente fortemente tipizzata di procedura remota chiama i servizi affidabili e Reliable Actors. Questo è più semplice hello e tooget modo più rapido avviato comunicazione del servizio. Le comunicazioni remote del servizio gestiscono la risoluzione degli indirizzi del servizio, la connessione, la ripetizione dei tentativi e la gestione degli errori. Questo è disponibile sia per applicazioni C# che per applicazioni Java.
* **HTTP**: per comunicazioni indipendenti dal linguaggio, HTTP costituisce la scelta standard di settore, con strumenti e server HTTP disponibili in molti linguaggi diversi, tutti supportati da Service Fabric. I servizi possono usare qualsiasi stack HTTP disponibile, inclusa l'[API Web ASP.NET](service-fabric-reliable-services-communication-webapi.md) per applicazioni C#. I client scritti in c# possono sfruttare hello `ICommunicationClient` e `ServicePartitionClient` classi, mentre per Java, utilizzare hello `CommunicationClient` e `FabricServicePartitionClient` classi, [per la risoluzione per il servizio, le connessioni HTTP e cicli di ripetizione](service-fabric-reliable-services-communication.md).
* **WCF**: se si dispone di codice esistente che utilizza il framework di comunicazione WCF, è quindi possibile utilizzare hello `WcfCommunicationListener` sul lato server hello e `WcfCommunicationClient` e `ServicePartitionClient` classi per i client hello. Questo comunque è disponibile solo per applicazioni C# in cluster basati su Windows. Per ulteriori informazioni, vedere l'articolo [implementazione basata su WCF di stack di comunicazione hello](service-fabric-reliable-services-communication-wcf.md).

## <a name="using-custom-protocols-and-other-communication-frameworks"></a>Uso di protocolli personalizzati e altri framework di comunicazione
I servizi possono usare qualsiasi protocollo o framework per le comunicazioni, ad esempio un protocollo binario personalizzato su socket TCP o eventi di streaming tramite l'[Hub eventi di Azure](https://azure.microsoft.com/services/event-hubs/) o l'[Hub IoT di Azure](https://azure.microsoft.com/services/iot-hub/). Service Fabric fornisce astrazione comunicazione API che è possibile collegare lo stack di comunicazione, mentre tutti hello toodiscover di lavoro e la connessione da parte dell'utente. Vedere l'articolo relativo hello [il modello di comunicazione affidabile servizio](service-fabric-reliable-services-communication.md) per altri dettagli.

## <a name="next-steps"></a>Passaggi successivi
Informazioni su concetti hello e API disponibili in hello [il modello di comunicazione di servizi affidabili](service-fabric-reliable-services-communication.md), quindi iniziare a usare velocemente [comunicazione remota del servizio](service-fabric-reliable-services-communication-remoting.md) o toolearn approfondita come toowrite un listener di comunicazione utilizzando [API Web con OWIN indipendente](service-fabric-reliable-services-communication-webapi.md).

[1]: ./media/service-fabric-connect-and-communicate-with-services/serviceendpoints.png
[2]: ./media/service-fabric-connect-and-communicate-with-services/namingservice.png
[3]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancertopology.png
[4]: ./media/service-fabric-connect-and-communicate-with-services/nodeport.png
[5]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerport.png
[7]: ./media/service-fabric-connect-and-communicate-with-services/distributedservices.png
[8]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerprobe.png
[9]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[10]: ./media/service-fabric-reverseproxy/internal-communication.png
