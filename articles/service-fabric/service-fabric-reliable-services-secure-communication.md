---
title: Proteggere le comunicazioni per i servizi in Azure Service Fabric | Microsoft Docs
description: Panoramica relativa a come proteggere le comunicazioni per servizi Reliable Services in esecuzione in un cluster di Azure Service Fabric.
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
ms.openlocfilehash: 53119244f8f09c0c6c43f43761af1cc074f8d0af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="10b6b-103">Proteggere le comunicazioni per i servizi in Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="10b6b-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="10b6b-104">C# su Windows</span><span class="sxs-lookup"><span data-stu-id="10b6b-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="10b6b-105">Java su Linux</span><span class="sxs-lookup"><span data-stu-id="10b6b-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

<span data-ttu-id="10b6b-106">La sicurezza è uno degli aspetti essenziali delle comunicazioni.</span><span class="sxs-lookup"><span data-stu-id="10b6b-106">Security is one of the most important aspects of communication.</span></span> <span data-ttu-id="10b6b-107">Il framework di applicazioni di Reliable Services offre alcuni stack e strumenti predefiniti che è possibile usare per migliorare la sicurezza.</span><span class="sxs-lookup"><span data-stu-id="10b6b-107">The Reliable Services application framework provides a few prebuilt communication stacks and tools that you can use to improve security.</span></span> <span data-ttu-id="10b6b-108">In questo articolo viene illustrato come migliorare la sicurezza quando si usa la comunicazione remota dei servizi e lo stack di comunicazione di Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="10b6b-108">This article talks about how to improve security when you're using service remoting and the Windows Communication Foundation (WCF) communication stack.</span></span>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="10b6b-109">Proteggere un servizio quando si usa la comunicazione remota dei servizi</span><span class="sxs-lookup"><span data-stu-id="10b6b-109">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="10b6b-110">Verrà usato un [esempio](service-fabric-reliable-services-communication-remoting.md) esistente che spiega come configurare la comunicazione remota per Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="10b6b-110">We are using an existing [example](service-fabric-reliable-services-communication-remoting.md) that explains how to set up remoting for reliable services.</span></span> <span data-ttu-id="10b6b-111">Per proteggere un servizio quando si usa la comunicazione remota, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="10b6b-111">To help secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="10b6b-112">Creare un'interfaccia, `IHelloWorldStateful`, che definisce i metodi che saranno disponibili per la Remote Procedure Call del servizio.</span><span class="sxs-lookup"><span data-stu-id="10b6b-112">Create an interface, `IHelloWorldStateful`, that defines the methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="10b6b-113">Il servizio userà il metodo `FabricTransportServiceRemotingListener`, dichiarato nello spazio dei nomi `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime`.</span><span class="sxs-lookup"><span data-stu-id="10b6b-113">Your service will use `FabricTransportServiceRemotingListener`, which is declared in the `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` namespace.</span></span> <span data-ttu-id="10b6b-114">Si tratta di un'implementazione `ICommunicationListener` che fornisce funzionalità di accesso remoto.</span><span class="sxs-lookup"><span data-stu-id="10b6b-114">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span>

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
2. <span data-ttu-id="10b6b-115">Aggiungere le impostazioni del listener e le credenziali di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="10b6b-115">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="10b6b-116">Assicurarsi che il certificato da usare per proteggere le comunicazioni dei servizi sia installato in tutti i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="10b6b-116">Make sure that the certificate that you want to use to help secure your service communication is installed on all the nodes in the cluster.</span></span> <span data-ttu-id="10b6b-117">Esistono due modi per specificare le impostazioni del listener e le credenziali di sicurezza:</span><span class="sxs-lookup"><span data-stu-id="10b6b-117">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="10b6b-118">Specificarle direttamente nel codice del servizio:</span><span class="sxs-lookup"><span data-stu-id="10b6b-118">Provide them directly in the service code:</span></span>

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
   2. <span data-ttu-id="10b6b-119">Specificarle tramite un [pacchetto di configurazione](service-fabric-application-model.md):</span><span class="sxs-lookup"><span data-stu-id="10b6b-119">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="10b6b-120">Aggiungere una sezione `TransportSettings` nel file settings.xml.</span><span class="sxs-lookup"><span data-stu-id="10b6b-120">Add a `TransportSettings` section in the settings.xml file.</span></span>

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

       <span data-ttu-id="10b6b-121">In questo caso il metodo `CreateServiceReplicaListeners` avrà un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="10b6b-121">In this case, the `CreateServiceReplicaListeners` method will look like this:</span></span>

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

        <span data-ttu-id="10b6b-122">Se si aggiunge una sezione `TransportSettings` al file settings.xml, `FabricTransportRemotingListenerSettings ` caricherà tutte le impostazioni da questa sezione per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="10b6b-122">If you add a `TransportSettings` section in the settings.xml file , `FabricTransportRemotingListenerSettings ` will load all the settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section .-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="10b6b-123">In questo caso il metodo `CreateServiceReplicaListeners` avrà un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="10b6b-123">In this case, the `CreateServiceReplicaListeners` method will look like this:</span></span>

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
3. <span data-ttu-id="10b6b-124">Quando si chiamano metodi in un servizio protetto tramite lo stack di comunicazione remota, anziché usare la classe `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` per creare un proxy del servizio, usare `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="10b6b-124">When you call methods on a secured service by using the remoting stack, instead of using the `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class to create a service proxy, use `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span></span> <span data-ttu-id="10b6b-125">Specificare `FabricTransportRemotingSettings`, che contiene `SecurityCredentials`.</span><span class="sxs-lookup"><span data-stu-id="10b6b-125">Pass in `FabricTransportRemotingSettings`, which contains `SecurityCredentials`.</span></span>

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

    <span data-ttu-id="10b6b-126">Se il codice client viene eseguito come parte del servizio, è possibile caricare `FabricTransportRemotingSettings` dal file settings.xml.</span><span class="sxs-lookup"><span data-stu-id="10b6b-126">If the client code is running as part of a service, you can load `FabricTransportRemotingSettings` from the settings.xml file.</span></span> <span data-ttu-id="10b6b-127">Creare una sezione HelloWorldClientTransportSettings simile al codice del servizio, come illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="10b6b-127">Create a HelloWorldClientTransportSettings section that is similar to the service code, as shown earlier.</span></span> <span data-ttu-id="10b6b-128">Apportare le modifiche seguenti al codice client:</span><span class="sxs-lookup"><span data-stu-id="10b6b-128">Make the following changes to the client code:</span></span>

    ```csharp
    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.LoadFrom("HelloWorldClientTransportSettings")));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    <span data-ttu-id="10b6b-129">Se il client non è in esecuzione come parte di un servizio, è possibile creare un file client_name.settings.xml nello stesso percorso del file client_name.exe.</span><span class="sxs-lookup"><span data-stu-id="10b6b-129">If the client is not running as part of a service, you can create a client_name.settings.xml file in the same location where the client_name.exe is.</span></span> <span data-ttu-id="10b6b-130">Creare quindi una sezione TransportSettings in tale file.</span><span class="sxs-lookup"><span data-stu-id="10b6b-130">Then create a TransportSettings section in that file.</span></span>

    <span data-ttu-id="10b6b-131">Come con il servizio, se si aggiunge una sezione `TransportSettings` nel file settings.xml/client_name.settings.xml del client, `FabricTransportRemotingSettings` carica tutte le impostazioni da questa sezione per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="10b6b-131">Similar to the service, if you add a `TransportSettings` section in client settings.xml/client_name.settings.xml, `FabricTransportRemotingSettings` loads all the settings from this section by default.</span></span>

    <span data-ttu-id="10b6b-132">In questo caso il codice precedente risulta ancora più semplice:</span><span class="sxs-lookup"><span data-stu-id="10b6b-132">In that case, the earlier code is even further simplified:</span></span>  

    ```csharp

    IHelloWorldStateful client = ServiceProxy.Create<IHelloWorldStateful>(
                 new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

## <a name="help-secure-a-service-when-youre-using-a-wcf-based-communication-stack"></a><span data-ttu-id="10b6b-133">Proteggere un servizio quando si usa uno stack di comunicazione basato su WCF</span><span class="sxs-lookup"><span data-stu-id="10b6b-133">Help secure a service when you're using a WCF-based communication stack</span></span>
<span data-ttu-id="10b6b-134">Verrà usato un [esempio](service-fabric-reliable-services-communication-wcf.md) esistente che spiega come configurare uno stack di comunicazione basato su WCF per Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="10b6b-134">We are using an existing [example](service-fabric-reliable-services-communication-wcf.md) that explains how to set up a WCF-based communication stack for reliable services.</span></span> <span data-ttu-id="10b6b-135">Per proteggere un sevizio quando si usa uno stack di comunicazione basato su WCF, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="10b6b-135">To help secure a service when you're using a WCF-based communication stack, follow these steps:</span></span>

1. <span data-ttu-id="10b6b-136">Per il servizio, è necessario proteggere il listener di comunicazione WCF (`WcfCommunicationListener`) che viene creato.</span><span class="sxs-lookup"><span data-stu-id="10b6b-136">For the service, you need to help secure the WCF communication listener (`WcfCommunicationListener`) that you create.</span></span> <span data-ttu-id="10b6b-137">A tale scopo, modificare il metodo `CreateServiceReplicaListeners` .</span><span class="sxs-lookup"><span data-stu-id="10b6b-137">To do this, modify the `CreateServiceReplicaListeners` method.</span></span>

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

        // Add certificate details in the ServiceHost credentials.
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
2. <span data-ttu-id="10b6b-138">Nel client la classe `WcfCommunicationClient` creata nell' [esempio](service-fabric-reliable-services-communication-wcf.md) precedente rimane invariata.</span><span class="sxs-lookup"><span data-stu-id="10b6b-138">In the client, the `WcfCommunicationClient` class that was created in the previous [example](service-fabric-reliable-services-communication-wcf.md) remains unchanged.</span></span> <span data-ttu-id="10b6b-139">È però necessario eseguire l'override del metodo `CreateClientAsync` di `WcfCommunicationClientFactory`:</span><span class="sxs-lookup"><span data-stu-id="10b6b-139">But you need to override the `CreateClientAsync` method of `WcfCommunicationClientFactory`:</span></span>

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
            // Add certificate details to the ChannelFactory credentials.
            // These credentials will be used by the clients created by
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

    <span data-ttu-id="10b6b-140">Usare il metodo `SecureWcfCommunicationClientFactory` per creare un client di comunicazione WCF (`WcfCommunicationClient`).</span><span class="sxs-lookup"><span data-stu-id="10b6b-140">Use `SecureWcfCommunicationClientFactory` to create a WCF communication client (`WcfCommunicationClient`).</span></span> <span data-ttu-id="10b6b-141">Usare il client per richiamare i metodi del servizio.</span><span class="sxs-lookup"><span data-stu-id="10b6b-141">Use the client to invoke service methods.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="10b6b-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="10b6b-142">Next steps</span></span>
* [<span data-ttu-id="10b6b-143">Web API con OWIN in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="10b6b-143">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
