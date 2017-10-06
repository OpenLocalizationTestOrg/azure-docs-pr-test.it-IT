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
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a>Proteggere le comunicazioni per i servizi in Azure Service Fabric
> [!div class="op_single_selector"]
> * [C# su Windows](service-fabric-reliable-services-secure-communication.md)
> * [Java su Linux](service-fabric-reliable-services-secure-communication-java.md)
>
>

La sicurezza è uno degli aspetti più importanti di hello di comunicazione. Hello servizi affidabili application framework fornisce alcuni stack di comunicazione predefiniti e gli strumenti che è possibile utilizzare la sicurezza tooimprove. In questo articolo illustra come tooimprove sicurezza quando si utilizza il servizio remoto e hello stack di comunicazione di Windows Communication Foundation (WCF).

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a>Proteggere un servizio quando si usa la comunicazione remota dei servizi
Si sta usando un oggetto esistente [esempio](service-fabric-reliable-services-communication-remoting.md) che spiega come tooset backup remoto per servizi affidabili. toohelp proteggere un servizio quando si usa la comunicazione remota del servizio, seguire questi passaggi:

1. Creare un'interfaccia, `IHelloWorldStateful`, che definisce i metodi di hello che saranno disponibili per una chiamata di procedura remota nel servizio. Il servizio utilizzerà `FabricTransportServiceRemotingListener`, dichiarato in hello `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` dello spazio dei nomi. Si tratta di un’implementazione `ICommunicationListener` che fornisce funzionalità di accesso remoto.

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
2. Aggiungere le impostazioni del listener e le credenziali di sicurezza.

    Assicurarsi che il certificato hello che si desidera toohelp toouse sicuro che delle comunicazioni di servizio sono installata in tutti i nodi nel cluster hello hello. Esistono due modi per specificare le impostazioni del listener e le credenziali di sicurezza:

   1. Fornire loro direttamente nel codice del servizio hello:

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
   2. Specificarle tramite un [pacchetto di configurazione](service-fabric-application-model.md):

       Aggiungere un `TransportSettings` sezione nel file Settings hello.

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

       In questo caso, hello `CreateServiceReplicaListeners` metodo sarà simile al seguente:

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

        Se si aggiunge un `TransportSettings` sezione nel file Settings hello `FabricTransportRemotingListenerSettings ` caricherà tutte le impostazioni di hello in questa sezione per impostazione predefinita.

        ```xml
        <!--"TransportSettings" section .-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        In questo caso, hello `CreateServiceReplicaListeners` metodo sarà simile al seguente:

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
3. Quando si chiamano metodi su un servizio protetto tramite stack di comunicazione remota di hello, anziché utilizzare hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` toocreate classe un proxy del servizio, utilizzare `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`. Specificare `FabricTransportRemotingSettings`, che contiene `SecurityCredentials`.

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

    Se il codice client hello è in esecuzione come parte di un servizio, è possibile caricare `FabricTransportRemotingSettings` dal file Settings hello. Creare una sezione HelloWorldClientTransportSettings codice del servizio toohello simili, come illustrato in precedenza. Apportare hello il codice client toohello le modifiche seguenti:

    ```csharp
    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.LoadFrom("HelloWorldClientTransportSettings")));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    Se il client di hello non è in esecuzione come parte di un servizio, è possibile creare un file client_name.settings.xml in hello stessa posizione in cui client_name.exe hello. Creare quindi una sezione TransportSettings in tale file.

    Servizio toohello simile, se si aggiunge un `TransportSettings` sezione client settings.xml/client_name.settings.xml, `FabricTransportRemotingSettings` carica tutte le impostazioni di hello in questa sezione per impostazione predefinita.

    In tal caso, hello codice precedenti viene ulteriormente semplificata:  

    ```csharp

    IHelloWorldStateful client = ServiceProxy.Create<IHelloWorldStateful>(
                 new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

## <a name="help-secure-a-service-when-youre-using-a-wcf-based-communication-stack"></a>Proteggere un servizio quando si usa uno stack di comunicazione basato su WCF
Si sta usando un oggetto esistente [esempio](service-fabric-reliable-services-communication-wcf.md) che spiega come tooset di una comunicazione WCF basato su stack per servizi affidabili. toohelp proteggere un servizio quando si utilizza uno stack di comunicazione basata su WCF, seguire questi passaggi:

1. Per il servizio di hello, è necessario listener di comunicazione WCF protetto hello toohelp (`WcfCommunicationListener`) creati. toodo, modificare hello `CreateServiceReplicaListeners` metodo.

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
2. Nel client hello hello `WcfCommunicationClient` classe che è stato creato in hello precedente [esempio](service-fabric-reliable-services-communication-wcf.md) rimane invariato. Ma è necessario hello toooverride `CreateClientAsync` metodo `WcfCommunicationClientFactory`:

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

    Utilizzare `SecureWcfCommunicationClientFactory` toocreate un client di comunicazione WCF (`WcfCommunicationClient`). Utilizzare i metodi del servizio tooinvoke hello client.

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

## <a name="next-steps"></a>Passaggi successivi
* [Web API con OWIN in Reliable Services](service-fabric-reliable-services-communication-webapi.md)
