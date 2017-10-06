---
title: aaaHelp comunicazione protetta per i servizi in Azure Service Fabric | Documenti Microsoft
description: Panoramica di come toohelp proteggere le comunicazioni per i servizi affidabile che sono in esecuzione in un cluster di Azure Service Fabric.
services: service-fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: vturecek
ms.assetid: fc129c1a-fbe4-4339-83ae-0e69a41654e0
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/20/2017
ms.author: suchiagicha
ms.openlocfilehash: 15201eb503322b17db329b319f1f42860b0f0c6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="976f4-103">Proteggere le comunicazioni per i servizi in Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="976f4-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="976f4-104">C# su Windows</span><span class="sxs-lookup"><span data-stu-id="976f4-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="976f4-105">Java su Linux</span><span class="sxs-lookup"><span data-stu-id="976f4-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

<span data-ttu-id="976f4-106">La sicurezza è uno degli aspetti più importanti di hello di comunicazione.</span><span class="sxs-lookup"><span data-stu-id="976f4-106">Security is one of hello most important aspects of communication.</span></span> <span data-ttu-id="976f4-107">Hello servizi affidabili application framework fornisce alcuni stack di comunicazione predefiniti e gli strumenti che è possibile utilizzare la sicurezza tooimprove.</span><span class="sxs-lookup"><span data-stu-id="976f4-107">hello Reliable Services application framework provides a few prebuilt communication stacks and tools that you can use tooimprove security.</span></span> <span data-ttu-id="976f4-108">In questo articolo illustra come tooimprove sicurezza quando si utilizza il servizio remoto e hello stack di comunicazione di Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="976f4-108">This article talks about how tooimprove security when you're using service remoting and hello Windows Communication Foundation (WCF) communication stack.</span></span>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="976f4-109">Proteggere un servizio quando si usa la comunicazione remota dei servizi</span><span class="sxs-lookup"><span data-stu-id="976f4-109">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="976f4-110">Si sta usando un oggetto esistente [esempio](service-fabric-reliable-services-communication-remoting.md) che spiega come tooset backup remoto per servizi affidabili.</span><span class="sxs-lookup"><span data-stu-id="976f4-110">We are using an existing [example](service-fabric-reliable-services-communication-remoting.md) that explains how tooset up remoting for reliable services.</span></span> <span data-ttu-id="976f4-111">toohelp proteggere un servizio quando si usa la comunicazione remota del servizio, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="976f4-111">toohelp secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="976f4-112">Creare un'interfaccia, `IHelloWorldStateful`, che definisce i metodi di hello che saranno disponibili per una chiamata di procedura remota nel servizio.</span><span class="sxs-lookup"><span data-stu-id="976f4-112">Create an interface, `IHelloWorldStateful`, that defines hello methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="976f4-113">Il servizio utilizzerà `FabricTransportServiceRemotingListener`, dichiarato in hello `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="976f4-113">Your service will use `FabricTransportServiceRemotingListener`, which is declared in hello `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` namespace.</span></span> <span data-ttu-id="976f4-114">Si tratta di un’implementazione `ICommunicationListener` che fornisce funzionalità di accesso remoto.</span><span class="sxs-lookup"><span data-stu-id="976f4-114">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span>

    ```csharp
    public interface IHelloWorldStateful : IService
    {
        Task<string> GetHelloWorld();
    }

    internal class HelloWorldStateful : StatefulService, IHelloWorldStateful
    {
        protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
        {
            return new[]{
                    new ServiceReplicaListener(
                        (context) => new FabricTransportServiceRemotingListener(context,this))};
        }

        public Task<string> GetHelloWorld()
        {
            return Task.FromResult("Hello World!");
        }
    }
    ```
2. <span data-ttu-id="976f4-115">Aggiungere le impostazioni del listener e le credenziali di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="976f4-115">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="976f4-116">Assicurarsi che il certificato hello che si desidera toohelp toouse sicuro che delle comunicazioni di servizio sono installata in tutti i nodi nel cluster hello hello.</span><span class="sxs-lookup"><span data-stu-id="976f4-116">Make sure that hello certificate that you want toouse toohelp secure your service communication is installed on all hello nodes in hello cluster.</span></span> <span data-ttu-id="976f4-117">Esistono due modi per specificare le impostazioni del listener e le credenziali di sicurezza:</span><span class="sxs-lookup"><span data-stu-id="976f4-117">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="976f4-118">Fornire loro direttamente nel codice del servizio hello:</span><span class="sxs-lookup"><span data-stu-id="976f4-118">Provide them directly in hello service code:</span></span>

       ```csharp
       protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
       {
           FabricTransportRemotingListenerSettings  listenerSettings = new FabricTransportRemotingListenerSettings
           {
               MaxMessageSize = 10000000,
               SecurityCredentials = GetSecurityCredentials()
           };
           return new[]
           {
               new ServiceReplicaListener(
                   (context) => new FabricTransportServiceRemotingListener(context,this,listenerSettings))
           };
       }

       private static SecurityCredentials GetSecurityCredentials()
       {
           // Provide certificate details.
           var x509Credentials = new X509Credentials
           {
               FindType = X509FindType.FindByThumbprint,
               FindValue = "4FEF3950642138446CC364A396E1E881DB76B48C",
               StoreLocation = StoreLocation.LocalMachine,
               StoreName = "My",
               ProtectionLevel = ProtectionLevel.EncryptAndSign
           };
           x509Credentials.RemoteCommonNames.Add("ServiceFabric-Test-Cert");
           x509Credentials.RemoteCertThumbprints.Add("9FEF3950642138446CC364A396E1E881DB76B483");
           return x509Credentials;
       }
       ```
   2. <span data-ttu-id="976f4-119">Specificarle tramite un [pacchetto di configurazione](service-fabric-application-model.md):</span><span class="sxs-lookup"><span data-stu-id="976f4-119">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="976f4-120">Aggiungere un `TransportSettings` sezione nel file Settings hello.</span><span class="sxs-lookup"><span data-stu-id="976f4-120">Add a `TransportSettings` section in hello settings.xml file.</span></span>

       ```xml
       <Section Name="HelloWorldStatefulTransportSettings">
           <Parameter Name="MaxMessageSize" Value="10000000" />
           <Parameter Name="SecurityCredentialsType" Value="X509" />
           <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
           <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
           <Parameter Name="CertificateRemoteThumbprints" Value="9FEF3950642138446CC364A396E1E881DB76B483" />
           <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
           <Parameter Name="CertificateStoreName" Value="My" />
           <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
           <Parameter Name="CertificateRemoteCommonNames" Value="ServiceFabric-Test-Cert" />
       </Section>
       ```

       <span data-ttu-id="976f4-121">In questo caso, hello `CreateServiceReplicaListeners` metodo sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="976f4-121">In this case, hello `CreateServiceReplicaListeners` method will look like this:</span></span>

       ```csharp
       protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
       {
           return new[]
           {
               new ServiceReplicaListener(
                   (context) => new FabricTransportServiceRemotingListener(
                       context,this,FabricTransportRemotingListenerSettings .LoadFrom("HelloWorldStatefulTransportSettings")))
           };
       }
       ```

        <span data-ttu-id="976f4-122">Se si aggiunge un `TransportSettings` sezione nel file Settings hello `FabricTransportRemotingListenerSettings ` caricherà tutte le impostazioni di hello in questa sezione per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="976f4-122">If you add a `TransportSettings` section in hello settings.xml file , `FabricTransportRemotingListenerSettings ` will load all hello settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section .-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="976f4-123">In questo caso, hello `CreateServiceReplicaListeners` metodo sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="976f4-123">In this case, hello `CreateServiceReplicaListeners` method will look like this:</span></span>

        ```csharp
        protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
        {
            return new[]
            {
                return new[]{
                        new ServiceReplicaListener(
                            (context) => new FabricTransportServiceRemotingListener(context,this))};
            };
        }
        ```
3. <span data-ttu-id="976f4-124">Quando si chiamano metodi su un servizio protetto tramite stack di comunicazione remota di hello, anziché utilizzare hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` toocreate classe un proxy del servizio, utilizzare `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="976f4-124">When you call methods on a secured service by using hello remoting stack, instead of using hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class toocreate a service proxy, use `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span></span> <span data-ttu-id="976f4-125">Specificare `FabricTransportRemotingSettings`, che contiene `SecurityCredentials`.</span><span class="sxs-lookup"><span data-stu-id="976f4-125">Pass in `FabricTransportRemotingSettings`, which contains `SecurityCredentials`.</span></span>

    ```csharp

    var x509Credentials = new X509Credentials
    {
        FindType = X509FindType.FindByThumbprint,
        FindValue = "9FEF3950642138446CC364A396E1E881DB76B483",
        StoreLocation = StoreLocation.LocalMachine,
        StoreName = "My",
        ProtectionLevel = ProtectionLevel.EncryptAndSign
    };
    x509Credentials.RemoteCommonNames.Add("ServiceFabric-Test-Cert");
    x509Credentials.RemoteCertThumbprints.Add("4FEF3950642138446CC364A396E1E881DB76B48C");

    FabricTransportRemotingSettings transportSettings = new FabricTransportRemotingSettings
    {
        SecurityCredentials = x509Credentials,
    };

    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(transportSettings));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    <span data-ttu-id="976f4-126">Se il codice client hello è in esecuzione come parte di un servizio, è possibile caricare `FabricTransportRemotingSettings` dal file Settings hello.</span><span class="sxs-lookup"><span data-stu-id="976f4-126">If hello client code is running as part of a service, you can load `FabricTransportRemotingSettings` from hello settings.xml file.</span></span> <span data-ttu-id="976f4-127">Creare una sezione HelloWorldClientTransportSettings codice del servizio toohello simili, come illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="976f4-127">Create a HelloWorldClientTransportSettings section that is similar toohello service code, as shown earlier.</span></span> <span data-ttu-id="976f4-128">Apportare hello il codice client toohello le modifiche seguenti:</span><span class="sxs-lookup"><span data-stu-id="976f4-128">Make hello following changes toohello client code:</span></span>

    ```csharp
    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.LoadFrom("HelloWorldClientTransportSettings")));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    <span data-ttu-id="976f4-129">Se il client di hello non è in esecuzione come parte di un servizio, è possibile creare un file client_name.settings.xml in hello stessa posizione in cui client_name.exe hello.</span><span class="sxs-lookup"><span data-stu-id="976f4-129">If hello client is not running as part of a service, you can create a client_name.settings.xml file in hello same location where hello client_name.exe is.</span></span> <span data-ttu-id="976f4-130">Creare quindi una sezione TransportSettings in tale file.</span><span class="sxs-lookup"><span data-stu-id="976f4-130">Then create a TransportSettings section in that file.</span></span>

    <span data-ttu-id="976f4-131">Servizio toohello simile, se si aggiunge un `TransportSettings` sezione client settings.xml/client_name.settings.xml, `FabricTransportRemotingSettings` carica tutte le impostazioni di hello in questa sezione per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="976f4-131">Similar toohello service, if you add a `TransportSettings` section in client settings.xml/client_name.settings.xml, `FabricTransportRemotingSettings` loads all hello settings from this section by default.</span></span>

    <span data-ttu-id="976f4-132">In tal caso, hello codice precedenti viene ulteriormente semplificata:</span><span class="sxs-lookup"><span data-stu-id="976f4-132">In that case, hello earlier code is even further simplified:</span></span>  

    ```csharp

    IHelloWorldStateful client = ServiceProxy.Create<IHelloWorldStateful>(
                 new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

## <a name="help-secure-a-service-when-youre-using-a-wcf-based-communication-stack"></a><span data-ttu-id="976f4-133">Proteggere un servizio quando si usa uno stack di comunicazione basato su WCF</span><span class="sxs-lookup"><span data-stu-id="976f4-133">Help secure a service when you're using a WCF-based communication stack</span></span>
<span data-ttu-id="976f4-134">Si sta usando un oggetto esistente [esempio](service-fabric-reliable-services-communication-wcf.md) che spiega come tooset di una comunicazione WCF basato su stack per servizi affidabili.</span><span class="sxs-lookup"><span data-stu-id="976f4-134">We are using an existing [example](service-fabric-reliable-services-communication-wcf.md) that explains how tooset up a WCF-based communication stack for reliable services.</span></span> <span data-ttu-id="976f4-135">toohelp proteggere un servizio quando si utilizza uno stack di comunicazione basata su WCF, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="976f4-135">toohelp secure a service when you're using a WCF-based communication stack, follow these steps:</span></span>

1. <span data-ttu-id="976f4-136">Per il servizio di hello, è necessario listener di comunicazione WCF protetto hello toohelp (`WcfCommunicationListener`) creati.</span><span class="sxs-lookup"><span data-stu-id="976f4-136">For hello service, you need toohelp secure hello WCF communication listener (`WcfCommunicationListener`) that you create.</span></span> <span data-ttu-id="976f4-137">toodo, modificare hello `CreateServiceReplicaListeners` metodo.</span><span class="sxs-lookup"><span data-stu-id="976f4-137">toodo this, modify hello `CreateServiceReplicaListeners` method.</span></span>

    ```csharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
        return new[]
        {
            new ServiceReplicaListener(
                this.CreateWcfCommunicationListener)
        };
    }

    private WcfCommunicationListener<ICalculator> CreateWcfCommunicationListener(StatefulServiceContext context)
    {
       var wcfCommunicationListener = new WcfCommunicationListener<ICalculator>(
            serviceContext:context,
            wcfServiceObject:this,
            // For this example, we will be using NetTcpBinding.
            listenerBinding: GetNetTcpBinding(),
            endpointResourceName:"WcfServiceEndpoint");

        // Add certificate details in hello ServiceHost credentials.
        wcfCommunicationListener.ServiceHost.Credentials.ServiceCertificate.SetCertificate(
            StoreLocation.LocalMachine,
            StoreName.My,
            X509FindType.FindByThumbprint,
            "9DC906B169DC4FAFFD1697AC781E806790749D2F");
        return wcfCommunicationListener;
    }

    private static NetTcpBinding GetNetTcpBinding()
    {
        NetTcpBinding b = new NetTcpBinding(SecurityMode.TransportWithMessageCredential);
        b.Security.Message.ClientCredentialType = MessageCredentialType.Certificate;
        return b;
    }
    ```
2. <span data-ttu-id="976f4-138">Nel client hello hello `WcfCommunicationClient` classe che è stato creato in hello precedente [esempio](service-fabric-reliable-services-communication-wcf.md) rimane invariato.</span><span class="sxs-lookup"><span data-stu-id="976f4-138">In hello client, hello `WcfCommunicationClient` class that was created in hello previous [example](service-fabric-reliable-services-communication-wcf.md) remains unchanged.</span></span> <span data-ttu-id="976f4-139">Ma è necessario hello toooverride `CreateClientAsync` metodo `WcfCommunicationClientFactory`:</span><span class="sxs-lookup"><span data-stu-id="976f4-139">But you need toooverride hello `CreateClientAsync` method of `WcfCommunicationClientFactory`:</span></span>

    ```csharp
    public class SecureWcfCommunicationClientFactory<TServiceContract> : WcfCommunicationClientFactory<TServiceContract> where TServiceContract : class
    {
        private readonly Binding clientBinding;
        private readonly object callbackObject;
        public SecureWcfCommunicationClientFactory(
            Binding clientBinding,
            IEnumerable<IExceptionHandler> exceptionHandlers = null,
            IServicePartitionResolver servicePartitionResolver = null,
            string traceId = null,
            object callback = null)
            : base(clientBinding, exceptionHandlers, servicePartitionResolver,traceId,callback)
        {
            this.clientBinding = clientBinding;
            this.callbackObject = callback;
        }

        protected override Task<WcfCommunicationClient<TServiceContract>> CreateClientAsync(string endpoint, CancellationToken cancellationToken)
        {
            var endpointAddress = new EndpointAddress(new Uri(endpoint));
            ChannelFactory<TServiceContract> channelFactory;
            if (this.callbackObject != null)
            {
                channelFactory = new DuplexChannelFactory<TServiceContract>(
                this.callbackObject,
                this.clientBinding,
                endpointAddress);
            }
            else
            {
                channelFactory = new ChannelFactory<TServiceContract>(this.clientBinding, endpointAddress);
            }
            // Add certificate details toohello ChannelFactory credentials.
            // These credentials will be used by hello clients created by
            // SecureWcfCommunicationClientFactory.  
            channelFactory.Credentials.ClientCertificate.SetCertificate(
                StoreLocation.LocalMachine,
                StoreName.My,
                X509FindType.FindByThumbprint,
                "9DC906B169DC4FAFFD1697AC781E806790749D2F");
            var channel = channelFactory.CreateChannel();
            var clientChannel = ((IClientChannel)channel);
            clientChannel.OperationTimeout = this.clientBinding.ReceiveTimeout;
            return Task.FromResult(this.CreateWcfCommunicationClient(channel));
        }
    }
    ```

    <span data-ttu-id="976f4-140">Utilizzare `SecureWcfCommunicationClientFactory` toocreate un client di comunicazione WCF (`WcfCommunicationClient`).</span><span class="sxs-lookup"><span data-stu-id="976f4-140">Use `SecureWcfCommunicationClientFactory` toocreate a WCF communication client (`WcfCommunicationClient`).</span></span> <span data-ttu-id="976f4-141">Utilizzare i metodi del servizio tooinvoke hello client.</span><span class="sxs-lookup"><span data-stu-id="976f4-141">Use hello client tooinvoke service methods.</span></span>

    ```csharp
    IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();

    var wcfClientFactory = new SecureWcfCommunicationClientFactory<ICalculator>(clientBinding: GetNetTcpBinding(), servicePartitionResolver: partitionResolver);

    var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
        wcfClientFactory,
        ServiceUri,
        ServicePartitionKey.Singleton);

    var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
        client => client.Channel.Add(2, 3)).Result;
    ```

## <a name="next-steps"></a><span data-ttu-id="976f4-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="976f4-142">Next steps</span></span>
* [<span data-ttu-id="976f4-143">Web API con OWIN in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="976f4-143">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
