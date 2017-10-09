---
title: aaaHelp comunicazione protetta per i servizi in Azure Service Fabric | Documenti Microsoft
description: Panoramica di come toohelp proteggere le comunicazioni per i servizi affidabile che sono in esecuzione in un cluster di Azure Service Fabric.
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
ms.openlocfilehash: 14db54d50c35478c1f2c156de0dba36f1427c8cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="52527-103">Proteggere le comunicazioni per i servizi in Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="52527-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="52527-104">C# su Windows</span><span class="sxs-lookup"><span data-stu-id="52527-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="52527-105">Java su Linux</span><span class="sxs-lookup"><span data-stu-id="52527-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="52527-106">Proteggere un servizio quando si usa la comunicazione remota dei servizi</span><span class="sxs-lookup"><span data-stu-id="52527-106">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="52527-107">Verrà usato un oggetto esistente [esempio](service-fabric-reliable-services-communication-remoting-java.md) che spiega come tooset backup remoto per servizi affidabili.</span><span class="sxs-lookup"><span data-stu-id="52527-107">We'll be using an existing [example](service-fabric-reliable-services-communication-remoting-java.md) that explains how tooset up remoting for reliable services.</span></span> <span data-ttu-id="52527-108">toohelp proteggere un servizio quando si usa la comunicazione remota del servizio, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="52527-108">toohelp secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="52527-109">Creare un'interfaccia, `HelloWorldStateless`, che definisce i metodi di hello che saranno disponibili per una chiamata di procedura remota nel servizio.</span><span class="sxs-lookup"><span data-stu-id="52527-109">Create an interface, `HelloWorldStateless`, that defines hello methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="52527-110">Il servizio utilizzerà `FabricTransportServiceRemotingListener`, dichiarato in hello `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` pacchetto.</span><span class="sxs-lookup"><span data-stu-id="52527-110">Your service will use `FabricTransportServiceRemotingListener`, which is declared in hello `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` package.</span></span> <span data-ttu-id="52527-111">Si tratta di un’implementazione `CommunicationListener` che fornisce funzionalità di accesso remoto.</span><span class="sxs-lookup"><span data-stu-id="52527-111">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span>

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
2. <span data-ttu-id="52527-112">Aggiungere le impostazioni del listener e le credenziali di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="52527-112">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="52527-113">Assicurarsi che il certificato hello che si desidera toohelp toouse sicuro che delle comunicazioni di servizio sono installata in tutti i nodi nel cluster hello hello.</span><span class="sxs-lookup"><span data-stu-id="52527-113">Make sure that hello certificate that you want toouse toohelp secure your service communication is installed on all hello nodes in hello cluster.</span></span> <span data-ttu-id="52527-114">Esistono due modi per specificare le impostazioni del listener e le credenziali di sicurezza:</span><span class="sxs-lookup"><span data-stu-id="52527-114">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="52527-115">Specificarle tramite un [pacchetto di configurazione](service-fabric-application-model.md):</span><span class="sxs-lookup"><span data-stu-id="52527-115">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="52527-116">Aggiungere un `TransportSettings` sezione nel file Settings hello.</span><span class="sxs-lookup"><span data-stu-id="52527-116">Add a `TransportSettings` section in hello settings.xml file.</span></span>

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

       <span data-ttu-id="52527-117">In questo caso, hello `createServiceInstanceListeners` metodo sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="52527-117">In this case, hello `createServiceInstanceListeners` method will look like this:</span></span>

       ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this, FabricTransportRemotingListenerSettings.loadFrom(HelloWorldStatelessTransportSettings));
            }));
            return listeners;
        }
       ```

        <span data-ttu-id="52527-118">Se si aggiunge un `TransportSettings` sezione nel file Settings hello senza alcun prefisso, `FabricTransportListenerSettings` caricherà tutte le impostazioni di hello in questa sezione per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="52527-118">If you add a `TransportSettings` section in hello settings.xml file without any prefix, `FabricTransportListenerSettings` will load all hello settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section without any prefix.-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="52527-119">In questo caso, hello `CreateServiceInstanceListeners` metodo sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="52527-119">In this case, hello `CreateServiceInstanceListeners` method will look like this:</span></span>

        ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
            return listeners;
        }
       ```
3. <span data-ttu-id="52527-120">Quando si chiamano metodi su un servizio protetto tramite stack di comunicazione remota di hello, anziché utilizzare hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` toocreate classe un proxy del servizio, utilizzare `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="52527-120">When you call methods on a secured service by using hello remoting stack, instead of using hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class toocreate a service proxy, use `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span></span>

    <span data-ttu-id="52527-121">Se il codice client hello è in esecuzione come parte di un servizio, è possibile caricare `FabricTransportSettings` dal file Settings hello.</span><span class="sxs-lookup"><span data-stu-id="52527-121">If hello client code is running as part of a service, you can load `FabricTransportSettings` from hello settings.xml file.</span></span> <span data-ttu-id="52527-122">Creare una sezione TransportSettings codice servizio toohello simile, come illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="52527-122">Create a TransportSettings section that is similar toohello service code, as shown earlier.</span></span> <span data-ttu-id="52527-123">Apportare hello il codice client toohello le modifiche seguenti:</span><span class="sxs-lookup"><span data-stu-id="52527-123">Make hello following changes toohello client code:</span></span>

    ```java

    FabricServiceProxyFactory serviceProxyFactory = new FabricServiceProxyFactory(c -> {
            return new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.loadFrom("TransportPrefixTransportSettings"), null, null, null, null);
        }, null)

    HelloWorldStateless client = serviceProxyFactory.createServiceProxy(HelloWorldStateless.class,
        new URI("fabric:/MyApplication/MyHelloWorldService"));

    CompletableFuture<String> message = client.getHelloWorld();

    ```
