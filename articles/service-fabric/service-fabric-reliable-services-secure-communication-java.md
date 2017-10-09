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
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a>Proteggere le comunicazioni per i servizi in Azure Service Fabric
> [!div class="op_single_selector"]
> * [C# su Windows](service-fabric-reliable-services-secure-communication.md)
> * [Java su Linux](service-fabric-reliable-services-secure-communication-java.md)
>
>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a>Proteggere un servizio quando si usa la comunicazione remota dei servizi
Verrà usato un oggetto esistente [esempio](service-fabric-reliable-services-communication-remoting-java.md) che spiega come tooset backup remoto per servizi affidabili. toohelp proteggere un servizio quando si usa la comunicazione remota del servizio, seguire questi passaggi:

1. Creare un'interfaccia, `HelloWorldStateless`, che definisce i metodi di hello che saranno disponibili per una chiamata di procedura remota nel servizio. Il servizio utilizzerà `FabricTransportServiceRemotingListener`, dichiarato in hello `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` pacchetto. Si tratta di un’implementazione `CommunicationListener` che fornisce funzionalità di accesso remoto.

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
2. Aggiungere le impostazioni del listener e le credenziali di sicurezza.

    Assicurarsi che il certificato hello che si desidera toohelp toouse sicuro che delle comunicazioni di servizio sono installata in tutti i nodi nel cluster hello hello. Esistono due modi per specificare le impostazioni del listener e le credenziali di sicurezza:

   1. Specificarle tramite un [pacchetto di configurazione](service-fabric-application-model.md):

       Aggiungere un `TransportSettings` sezione nel file Settings hello.

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

       In questo caso, hello `createServiceInstanceListeners` metodo sarà simile al seguente:

       ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this, FabricTransportRemotingListenerSettings.loadFrom(HelloWorldStatelessTransportSettings));
            }));
            return listeners;
        }
       ```

        Se si aggiunge un `TransportSettings` sezione nel file Settings hello senza alcun prefisso, `FabricTransportListenerSettings` caricherà tutte le impostazioni di hello in questa sezione per impostazione predefinita.

        ```xml
        <!--"TransportSettings" section without any prefix.-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        In questo caso, hello `CreateServiceInstanceListeners` metodo sarà simile al seguente:

        ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
            return listeners;
        }
       ```
3. Quando si chiamano metodi su un servizio protetto tramite stack di comunicazione remota di hello, anziché utilizzare hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` toocreate classe un proxy del servizio, utilizzare `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.

    Se il codice client hello è in esecuzione come parte di un servizio, è possibile caricare `FabricTransportSettings` dal file Settings hello. Creare una sezione TransportSettings codice servizio toohello simile, come illustrato in precedenza. Apportare hello il codice client toohello le modifiche seguenti:

    ```java

    FabricServiceProxyFactory serviceProxyFactory = new FabricServiceProxyFactory(c -> {
            return new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.loadFrom("TransportPrefixTransportSettings"), null, null, null, null);
        }, null)

    HelloWorldStateless client = serviceProxyFactory.createServiceProxy(HelloWorldStateless.class,
        new URI("fabric:/MyApplication/MyHelloWorldService"));

    CompletableFuture<String> message = client.getHelloWorld();

    ```
