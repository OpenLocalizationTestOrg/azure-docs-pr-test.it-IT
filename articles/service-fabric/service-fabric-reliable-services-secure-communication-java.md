---
title: Proteggere le comunicazioni per i servizi in Azure Service Fabric | Microsoft Docs
description: Panoramica relativa a come proteggere le comunicazioni per servizi Reliable Services in esecuzione in un cluster di Azure Service Fabric.
services: service-fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: 
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/30/2017
ms.author: pakunapa
ms.openlocfilehash: c4634e3d8efb1745fffcfe3e647e43d867038716
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="9b5e6-103">Proteggere le comunicazioni per i servizi in Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9b5e6-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9b5e6-104">C# su Windows</span><span class="sxs-lookup"><span data-stu-id="9b5e6-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="9b5e6-105">Java su Linux</span><span class="sxs-lookup"><span data-stu-id="9b5e6-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="9b5e6-106">Proteggere un servizio quando si usa la comunicazione remota dei servizi</span><span class="sxs-lookup"><span data-stu-id="9b5e6-106">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="9b5e6-107">Verrà usato un [esempio](service-fabric-reliable-services-communication-remoting-java.md) esistente che spiega come configurare la comunicazione remota per Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="9b5e6-107">We'll be using an existing [example](service-fabric-reliable-services-communication-remoting-java.md) that explains how to set up remoting for reliable services.</span></span> <span data-ttu-id="9b5e6-108">Per proteggere un servizio quando si usa la comunicazione remota, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="9b5e6-108">To help secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="9b5e6-109">Creare un'interfaccia, `HelloWorldStateless`, che definisce i metodi che saranno disponibili per la Remote Procedure Call del servizio.</span><span class="sxs-lookup"><span data-stu-id="9b5e6-109">Create an interface, `HelloWorldStateless`, that defines the methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="9b5e6-110">Il servizio userà il metodo `FabricTransportServiceRemotingListener`, dichiarato nel pacchetto `microsoft.serviceFabric.services.remoting.fabricTransport.runtime`.</span><span class="sxs-lookup"><span data-stu-id="9b5e6-110">Your service will use `FabricTransportServiceRemotingListener`, which is declared in the `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` package.</span></span> <span data-ttu-id="9b5e6-111">Si tratta di un’implementazione `CommunicationListener` che fornisce funzionalità di accesso remoto.</span><span class="sxs-lookup"><span data-stu-id="9b5e6-111">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span>

    ```java
    public interface HelloWorldStateless extends Service {
        CompletableFuture<String> getHelloWorld();
    }

    class HelloWorldStatelessImpl extends StatelessService implements HelloWorldStateless {
        @Override
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
        return listeners;
        }

        public CompletableFuture<String> getHelloWorld() {
            return CompletableFuture.completedFuture("Hello World!");
        }
    }
    ```
2. <span data-ttu-id="9b5e6-112">Aggiungere le impostazioni del listener e le credenziali di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="9b5e6-112">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="9b5e6-113">Assicurarsi che il certificato da usare per proteggere le comunicazioni dei servizi sia installato in tutti i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="9b5e6-113">Make sure that the certificate that you want to use to help secure your service communication is installed on all the nodes in the cluster.</span></span> <span data-ttu-id="9b5e6-114">Esistono due modi per specificare le impostazioni del listener e le credenziali di sicurezza:</span><span class="sxs-lookup"><span data-stu-id="9b5e6-114">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="9b5e6-115">Specificarle tramite un [pacchetto di configurazione](service-fabric-application-model.md):</span><span class="sxs-lookup"><span data-stu-id="9b5e6-115">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="9b5e6-116">Aggiungere una sezione `TransportSettings` nel file settings.xml.</span><span class="sxs-lookup"><span data-stu-id="9b5e6-116">Add a `TransportSettings` section in the settings.xml file.</span></span>

       ```xml
       <!--Section name should always end with "TransportSettings".-->
       <!--Here we are using a prefix "HelloWorldStateless".-->
        <Section Name="HelloWorldStatelessTransportSettings">
            <Parameter Name="MaxMessageSize" Value="10000000" />
            <Parameter Name="SecurityCredentialsType" Value="X509_2" />
            <Parameter Name="CertificatePath" Value="/path/to/cert/BD1C71E248B8C6834C151174DECDBDC02DE1D954.crt" />
            <Parameter Name="CertificateProtectionLevel" Value="EncryptandSign" />
            <Parameter Name="CertificateRemoteThumbprints" Value="BD1C71E248B8C6834C151174DECDBDC02DE1D954" />
        </Section>

       ```

       <span data-ttu-id="9b5e6-117">In questo caso il metodo `createServiceInstanceListeners` avrà un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="9b5e6-117">In this case, the `createServiceInstanceListeners` method will look like this:</span></span>

       ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this, FabricTransportRemotingListenerSettings.loadFrom(HelloWorldStatelessTransportSettings));
            }));
            return listeners;
        }
       ```

        <span data-ttu-id="9b5e6-118">Se si aggiunge una sezione `TransportSettings` al file settings.xml senza alcun prefisso, `FabricTransportListenerSettings` caricherà tutte le impostazioni da questa sezione per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="9b5e6-118">If you add a `TransportSettings` section in the settings.xml file without any prefix, `FabricTransportListenerSettings` will load all the settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section without any prefix.-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="9b5e6-119">In questo caso il metodo `CreateServiceInstanceListeners` avrà un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="9b5e6-119">In this case, the `CreateServiceInstanceListeners` method will look like this:</span></span>

        ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
            return listeners;
        }
       ```
3. <span data-ttu-id="9b5e6-120">Quando si chiamano metodi in un servizio protetto tramite lo stack di comunicazione remota, anziché usare la classe `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` per creare un proxy del servizio, usare `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="9b5e6-120">When you call methods on a secured service by using the remoting stack, instead of using the `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class to create a service proxy, use `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span></span>

    <span data-ttu-id="9b5e6-121">Se il codice client viene eseguito come parte del servizio, è possibile caricare `FabricTransportSettings` dal file settings.xml.</span><span class="sxs-lookup"><span data-stu-id="9b5e6-121">If the client code is running as part of a service, you can load `FabricTransportSettings` from the settings.xml file.</span></span> <span data-ttu-id="9b5e6-122">Creare una sezione TransportSettings simile al codice del servizio, come illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9b5e6-122">Create a TransportSettings section that is similar to the service code, as shown earlier.</span></span> <span data-ttu-id="9b5e6-123">Apportare le modifiche seguenti al codice client:</span><span class="sxs-lookup"><span data-stu-id="9b5e6-123">Make the following changes to the client code:</span></span>

    ```java

    FabricServiceProxyFactory serviceProxyFactory = new FabricServiceProxyFactory(c -> {
            return new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.loadFrom("TransportPrefixTransportSettings"), null, null, null, null);
        }, null)

    HelloWorldStateless client = serviceProxyFactory.createServiceProxy(HelloWorldStateless.class,
        new URI("fabric:/MyApplication/MyHelloWorldService"));

    CompletableFuture<String> message = client.getHelloWorld();

    ```
