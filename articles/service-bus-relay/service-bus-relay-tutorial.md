---
title: esercitazione di inoltro di Service Bus WCF aaaAzure | Documenti Microsoft
description: Creare un'applicazione client e un servizio del bus di servizio usando Inoltro WCF.
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 53dfd236-97f1-4778-b376-be91aa14b842
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: sethm
ms.openlocfilehash: 78cd52ef51e9fcfcda2f13ec54bde3af50d76476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-tutorial"></a>Esercitazione sull'inoltro WCF di Azure

Questa esercitazione viene descritto come toobuild WCF semplice inoltro applicazione client e un servizio usando l'inoltro di Azure. Per un'esercitazione simile che usa la [messaggistica](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging) del bus di servizio, vedere [Introduzione alle code del bus di servizio](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).

Esecuzione di questa esercitazione consente di conoscere i passaggi di hello toocreate richiesto un'applicazione client e il servizio di inoltro WCF. Come per le rispettive controparti WCF originali, un servizio è un costrutto che espone uno o più endpoint, ognuno dei quali espone a sua volta una o più operazioni del servizio. endpoint Hello di un servizio specifica un indirizzo in cui è possibile trovare il servizio di hello, un'associazione che contiene informazioni hello che un client deve comunicare con il servizio di hello e un contratto che definisce funzionalità hello fornita dal client di tooits hello del servizio. Hello differenza principale tra WCF e di inoltro WCF è che tale endpoint hello è esposto nel cloud hello anziché in locale nel computer.

Dopo aver eseguito la sequenza di hello di argomenti in questa esercitazione, si disporrà di un servizio in esecuzione e un client che è possibile richiamare le operazioni del servizio hello hello. Hello primo argomento viene descritto come tooset un account. passaggi successivi Hello descrivono come toodefine un servizio che usa un contratto, come tooimplement hello servizio e come tooconfigure hello servizio nel codice. Vengono inoltre descritte come servizio hello toohost ed eseguire. Hello servizio creato è Self-hosted e hello client e servizio eseguito hello stesso computer. È possibile configurare il servizio di hello tramite codice o un file di configurazione.

Hello finale tre descritta come toocreate un'applicazione client, configurare un'applicazione client, hello e creare e utilizzare un client che è possibile accedere alla funzionalità hello dell'host hello.

## <a name="prerequisites"></a>Prerequisiti

toocomplete questa esercitazione, è necessario hello seguenti:

* [Microsoft Visual Studio 2015 o versione successiva](http://visualstudio.com). Questa esercitazione usa Visual Studio 2017.
* Un account Azure attivo. Se non si ha un account, è possibile crearne uno gratuito in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/free/).

## <a name="create-a-service-namespace"></a>Creare uno spazio dei nomi del servizio

primo passaggio Hello è toocreate uno spazio dei nomi e tooobtain un [firma di accesso condiviso (SAS)](../service-bus-messaging/service-bus-sas.md) chiave. Uno spazio dei nomi fornisce un limite per ogni applicazione esposta attraverso il servizio di inoltro hello. Una chiave di firma di accesso condiviso viene generata automaticamente dal sistema hello quando viene creato uno spazio dei nomi del servizio. combinazione di Hello di spazio dei nomi servizio e la chiave di firma di accesso condiviso fornisce le credenziali di hello per applicazione tooan di accesso tooauthenticate Azure. Seguire hello [le istruzioni qui](relay-create-namespace-portal.md) toocreate uno spazio dei nomi di inoltro.

## <a name="define-a-wcf-service-contract"></a>Definire un contratto del servizio WCF

contratto di servizio Hello specifica il servizio supporta hello operations (hello web terminologia relativa ai servizi per i metodi o funzioni). I contratti vengono creati definendo un'interfaccia C++, C# o Visual Basic. Ogni metodo nell'interfaccia hello corrisponde tooa operazione del servizio specifica. Ogni interfaccia deve essere hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) tooit applicare l'attributo e ogni operazione deve essere hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) tooit attributo applicato. Se un metodo in un'interfaccia con hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attributo non dispone di hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attributo, questo metodo non è esposto. Nell'esempio hello hello procedura viene fornito codice di Hello per le attività. Per una descrizione più ampia dei contratti e servizi, vedere [progettazione e implementazione di servizi](https://msdn.microsoft.com/library/ms729746.aspx) in hello documentazione WCF.

### <a name="create-a-relay-contract-with-an-interface"></a>Creare un contratto di inoltro con un'interfaccia

1. Aprire Visual Studio come amministratore facendo clic con il programma hello in hello **avviare** menu e selezionando **Esegui come amministratore**.
2. Creare un nuovo progetto di applicazione console. Fare clic su hello **File** dal menu **New**, quindi fare clic su **progetto**. In hello **nuovo progetto** finestra di dialogo, fare clic su **Visual c#** (se **Visual c#** non è visualizzato, cercarlo in **altri linguaggi**). Fare clic su hello **applicazione Console (.NET Framework)** , modello e denominarlo **EchoService**. Fare clic su **OK** progetto hello toocreate.

    ![][2]

3. Installare il pacchetto NuGet di Service Bus hello. Questo pacchetto aggiunge automaticamente le librerie del Bus di servizio toohello riferimenti, nonché hello WCF **System. ServiceModel**. [System. ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) spazio dei nomi hello consente tooprogrammatically accesso hello funzionalità di base di WCF. Bus di servizio Usa molti degli oggetti hello e degli attributi WCF toodefine di contratti di servizio.

    In Esplora soluzioni, fare clic sul progetto hello e quindi fare clic su **Gestisci pacchetti NuGet... **. Fare clic su hello **Sfoglia** tab, quindi cercare `Microsoft Azure Service Bus`. Selezionare il nome del progetto hello hello **versioni** casella. Fare clic su **installare**e accettare le condizioni di hello d'uso.

    ![][3]
4. In Esplora soluzioni fare doppio clic su hello Program.cs file tooopen possa nell'editor di hello, se non è già aperta.
5. Aggiungere il seguente hello istruzioni using all'inizio di hello del file hello:

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. Spazio dei nomi hello Modifica nome predefinito di **EchoService** troppo**ServiceBus**.

   > [!IMPORTANT]
   > Questa esercitazione viene utilizzato lo spazio dei nomi hello c# **ServiceBus**, ovvero hello dello spazio dei nomi di hello basati su contratto di tipo che viene utilizzato nel file di configurazione hello in hello gestito [configurare il client WCF hello](#configure-the-wcf-client) passaggio. È possibile specificare qualsiasi spazio dei nomi desiderato quando si compila questo esempio. Tuttavia, esercitazione hello non funzionerà a meno che non è quindi modificare hello gli spazi dei nomi del contratto hello e del servizio di conseguenza, nel file di configurazione dell'applicazione hello. spazio dei nomi Hello specificato nel file app. config file deve essere hello hello uguale allo spazio dei nomi hello specificato nel file c#.
   >
   >
7. Direttamente dopo hello `Microsoft.ServiceBus.Samples` dichiarazione dello spazio dei nomi, ma nello spazio dei nomi hello, definire una nuova interfaccia denominata `IEchoContract` e applicare hello `ServiceContractAttribute` interfaccia toohello attributo con il valore dello spazio dei nomi `http://samples.microsoft.com/ServiceModel/Relay/`. il valore di spazio dei nomi Hello è diverso dallo spazio dei nomi hello usato nell'ambito di hello del codice. Al contrario, il valore di spazio dei nomi hello viene utilizzato come identificatore univoco per questo contratto. Specificare in modo esplicito lo spazio dei nomi hello impedisce l'aggiunta il nome del contratto toohello valore dello spazio dei nomi predefinito di hello. Incollare hello seguente codice dopo la dichiarazione dello spazio dei nomi hello:

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > Spazio dei nomi del contratto di servizio hello contiene in genere, uno schema di denominazione che include informazioni sulla versione. Inclusione di informazioni sulla versione nello spazio dei nomi del contratto di servizio hello consente modifiche principali di servizio tooisolate definendo un nuovo contratto di servizio con un nuovo spazio dei nomi ed esponendolo in un nuovo endpoint. In questo modo, i client possono continuare contratto del servizio precedente toouse hello senza toobe aggiornato. Le informazioni sulla versione possono essere costituite da una data o da un numero di build. Per altre informazioni, vedere [Controllo delle versioni del servizio](http://go.microsoft.com/fwlink/?LinkID=180498). Ai fini di hello di questa esercitazione, hello denominazione dello spazio dei nomi di contratto di servizio hello non contiene informazioni sulla versione.
   >
   >
8. All'interno di hello `IEchoContract` l'interfaccia, dichiarare un metodo per hello singola operazione hello `IEchoContract` espone contratto in hello interfaccia e applicare hello `OperationContractAttribute` metodo toohello di attributo che si desidera tooexpose come parte di hello pubblica inoltro WCF contratto, come indicato di seguito:

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. Direttamente dopo hello `IEchoContract` definizione dell'interfaccia, dichiarare un canale che eredita sia da `IEchoContract` e anche toohello `IClientChannel` interfaccia, come illustrato di seguito:

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    Un canale è l'oggetto WCF hello attraverso cui client e host hello passare informazioni tooeach altri. In un secondo momento, si scriverà codice in base a informazioni di tooecho hello del canale tra due applicazioni hello.
10. Da hello **compilare** menu, fare clic su **Compila soluzione** o premere **Ctrl + MAIUSC + B** accuratezza hello tooconfirm del lavoro svolto finora.

### <a name="example"></a>Esempio

Hello di codice seguente mostra un'interfaccia di base che definisce un contratto di inoltro WCF.

```csharp
using System;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

Dopo aver creato hello interfaccia, è possibile implementare l'interfaccia hello.

## <a name="implement-hello-wcf-contract"></a>Contratto di implementare hello WCF

Creazione di un server di inoltro di Azure è necessario innanzitutto creare contratto hello, che viene definito tramite un'interfaccia. Per ulteriori informazioni sulla creazione di hello interfaccia, vedere il passaggio precedente di hello. passaggio successivo Hello è interfaccia hello tooimplement. Ciò comporta la creazione di una classe denominata `EchoService` che implementa hello definito dall'utente `IEchoContract` interfaccia. Dopo avere implementato l'interfaccia di hello, configurare l'interfaccia hello utilizzando un file di configurazione App. config. file di configurazione Hello contiene le informazioni necessarie per un'applicazione hello, ad esempio nome hello del servizio di hello, il nome di hello del contratto hello e tipo hello di protocollo è toocommunicate utilizzato con il servizio di inoltro hello. Nell'esempio hello hello procedura viene fornito codice di Hello utilizzato per queste attività. Per una discussione più generale su come un servizio tooimplement contratto, vedere [contratti di servizio che implementa](https://msdn.microsoft.com/library/ms733764.aspx) in hello documentazione WCF.

1. Creare una nuova classe denominata `EchoService` direttamente dopo la definizione di hello di hello `IEchoContract` interfaccia. Hello `EchoService` implementa hello `IEchoContract` interfaccia.

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    Le implementazioni di interfaccia tooother simili, è possibile implementare definizione hello in un file diverso. Tuttavia, per questa esercitazione, implementazione hello si trova in hello lo stesso file di definizione dell'interfaccia hello e hello `Main` metodo.
2. Applicare hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attributo toohello `IEchoContract` interfaccia. attributo di Hello Specifica spazio dei nomi e nome del servizio hello. Al termine dell'operazione, hello `EchoService` classe viene visualizzata come indicato di seguito:

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. Hello implementare `Echo` metodo definito in hello `IEchoContract` interfaccia hello `EchoService` classe.

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. Fare clic su **compilare**, quindi fare clic su **Compila soluzione** accuratezza hello tooconfirm del lavoro.

### <a name="define-hello-configuration-for-hello-service-host"></a>Definire la configurazione per l'host del servizio hello hello

1. file di configurazione Hello è molto simile file di configurazione WCF tooa. Include il nome del servizio hello, endpoint (vale a dire hello percorso inoltro Azure espone per i client e host toocommunicate reciprocamente) e hello associazione (tipo hello di protocollo utilizzato toocommunicate). Hello differenza principale è che l'endpoint del servizio si riferisce tooa [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) binding, che non fa parte di .NET Framework hello. [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) è una delle associazioni hello definite dal servizio hello.
2. In **Esplora**, fare doppio clic su hello app. config file tooopen nell'editor di Visual Studio hello.
3. In hello `<appSettings>` elemento, sostituire i segnaposto hello con nome hello dello spazio dei nomi di servizio e hello chiave di firma di accesso condiviso che è stato copiato in un passaggio precedente.
4. All'interno di hello `<system.serviceModel>` tag, aggiungere un `<services>` elemento. È possibile definire più applicazioni di inoltro in un singolo file di configurazione. In questa esercitazione ne viene tuttavia definita solo una.

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. All'interno di hello `<services>` elemento, aggiungere un `<service>` nome del servizio hello hello toodefine dell'elemento.

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. All'interno di hello `<service>` elemento, definire il percorso di hello del contratto dell'endpoint hello e hello anche tipo di associazione per l'endpoint di hello.

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    endpoint Hello definisce dove client hello cercherà un'applicazione hello host. In un secondo momento, esercitazione hello utilizza questo toocreate passaggio un URI che espone completamente host hello tramite inoltro di Azure. associazione di Hello dichiara che si sta usando TCP come hello toocommunicate protocollo con il servizio di inoltro hello.
7. Da hello **compilare** menu, fare clic su **Compila soluzione** accuratezza hello tooconfirm del lavoro.

### <a name="example"></a>Esempio

Hello codice riportato di seguito viene illustrata hello implementazione del contratto di servizio hello.

```csharp
[ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]

    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }
```

Hello codice riportato di seguito viene illustrato hello base formato del file app. config hello associato all'host del servizio hello.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <services>
      <service name="Microsoft.ServiceBus.Samples.EchoService">
        <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding" />
      </service>
    </services>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="host-and-run-a-basic-web-service-tooregister-with-hello-relay-service"></a>Ospitare ed eseguire un tooregister di servizio web di base con il servizio di inoltro hello

Questo passaggio viene descritto come toorun un Azure inoltro servizio.

### <a name="create-hello-relay-credentials"></a>Creare le credenziali di inoltro di hello

1. In `Main()`, creare due variabili nello spazio dei nomi di hello quali toostore e chiave di firma di accesso condiviso che vengono letti dalla finestra della console hello hello.

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    chiave di firma di accesso condiviso Hello sarà usato tooaccess successive al progetto. spazio dei nomi Hello viene passato come parametro troppo`CreateServiceUri` toocreate un URI del servizio.
2. Utilizzando un [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) di oggetti, dichiarare che si utilizzerà una chiave di firma di accesso condiviso come tipo di credenziale hello. Aggiungere hello seguente codice immediatamente dopo il codice hello aggiunto nell'ultimo passaggio hello.

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="create-a-base-address-for-hello-service"></a>Creare un indirizzo di base per il servizio hello

Dopo il codice hello aggiunto nell'ultimo passaggio hello, creare un `Uri` istanza per l'indirizzo di base hello del servizio di hello. Questo URI specifica lo schema di Service Bus hello, hello dello spazio dei nomi e il percorso di hello dell'interfaccia di servizio hello.

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

"sb" è un'abbreviazione per lo schema di Service Bus hello e indica che si sta usando TCP come protocollo di hello. Questo è stato indicato anche in precedenza nel file di configurazione hello quando [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) come associazione hello è stato specificato.

Per questa esercitazione, hello URI è `sb://putServiceNamespaceHere.windows.net/EchoService`.

### <a name="create-and-configure-hello-service-host"></a>Creare e configurare l'host del servizio hello

1. Impostare la modalità di connettività hello troppo`AutoDetect`.

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    modalità di connettività Hello descrive toocommunicate hello protocollo hello servizio viene utilizzato con il servizio di inoltro hello. HTTP o TCP. Usa impostazione predefinita hello `AutoDetect`, servizio hello tenta tooconnect tooAzure inoltro su TCP se disponibile e HTTP se TCP non è disponibile. Si noti che questo comportamento è diverso dal servizio di hello protocollo hello specifica per la comunicazione client. Tale protocollo è determinato dall'associazione hello utilizzata. Ad esempio, un servizio può utilizzare hello [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) binding, che specifica che l'endpoint comunica con i client su HTTP. Che è possibile specificare il servizio stesso **Connectivitymode** in modo che il servizio di hello comunica con Azure inoltro tramite TCP.
2. Creare l'host del servizio hello, tramite hello che URI creato in precedenza in questa sezione.

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    host del servizio Hello è oggetto WCF hello che crea un'istanza del servizio hello. In questo caso, si passa il tipo di hello del servizio si desidera toocreate (un `EchoService` tipo) e anche l'indirizzo toohello in corrispondenza del quale si desidera che il servizio di hello tooexpose.
3. Nella parte superiore di hello del file Program.cs hello, aggiungere i riferimenti troppo[ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) e [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. In `Main()`, configurare l'accesso pubblico tooenable endpoint hello.

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    Questo passaggio segnala al servizio di inoltro hello di che l'applicazione può essere trovata pubblicamente esaminando il feed ATOM hello per il progetto. Se si imposta **DiscoveryType** troppo**privata**, un client sarà comunque servizio hello in grado di tooaccess. Tuttavia, il servizio di hello non sarebbe stato visualizzato durante la ricerca dello spazio dei nomi di inoltro hello. Invece, client hello avrebbe percorso dell'endpoint tooknow hello in anticipo.
5. Applicare le credenziali del servizio di hello toohello gli endpoint del servizio definiti nel file app. config hello:

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    Come indicato nel passaggio precedente hello, si potrebbero avere dichiarati più servizi ed endpoint nel file di configurazione hello. Se si dispone, questo codice scorrerebbe il file di configurazione di hello e ricerca per toowhich ogni endpoint è necessario applicare le credenziali. Per questa esercitazione, tuttavia, i file di configurazione hello ha solo un endpoint.

### <a name="open-hello-service-host"></a>Host del servizio aprire hello

1. Aprire il servizio di hello.

    ```csharp
    host.Open();
    ```
2. Informare l'utente hello hello servizio è in esecuzione e spiegare come tooshut servizio hello.

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. Al termine, chiudere l'host del servizio hello.

    ```csharp
    host.Close();
    ```
4. Premere **Ctrl + MAIUSC + B** progetto hello toobuild.

### <a name="example"></a>Esempio

Il codice del servizio completato comparirà come indicato di seguito. codice Hello include il contratto di servizio hello e l'implementazione dai passaggi precedenti nell'esercitazione hello e host hello servizio in un'applicazione console.

```csharp
using System;
using System.ServiceModel;
using System.ServiceModel.Description;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Description;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { };

    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {

            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;         

            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS key: ");
            string sasKey = Console.ReadLine();

           // Create hello credentials object for hello endpoint.
            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            // Create hello service URI based on hello service namespace.
            Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            // Create hello service host reading hello configuration.
            ServiceHost host = new ServiceHost(typeof(EchoService), address);

            // Create hello ServiceRegistrySettings behavior for hello endpoint.
            IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);

            // Add hello Relay credentials tooall endpoints specified in configuration.
            foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
            {
                endpoint.Behaviors.Add(serviceRegistrySettings);
                endpoint.Behaviors.Add(sasCredential);
            }

            // Open hello service.
            host.Open();

            Console.WriteLine("Service address: " + address);
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            // Close hello service.
            host.Close();
        }
    }
}
```

## <a name="create-a-wcf-client-for-hello-service-contract"></a>Creare un client WCF per il contratto di servizio hello

passaggio successivo Hello è un'applicazione client toocreate e definire il contratto di servizio hello implementerà nei passaggi successivi. Si noti che molti di questi passaggi sono simili a passaggi hello usare toocreate un servizio: la definizione di un contratto, la modifica di un file app. config file, usare un servizio di inoltro di credenziali tooconnect toohello e così via. Nell'esempio hello hello procedura viene fornito codice di Hello utilizzato per queste attività.

1. Creare un nuovo progetto nella soluzione Visual Studio corrente hello per client hello eseguendo hello seguenti:

   1. In Esplora soluzioni in hello stessa soluzione che contiene il servizio di hello, fare doppio clic hello corrente soluzione (non il progetto hello) e fare clic su **Aggiungi**. Fare clic su **Nuovo progetto**.
   2. In hello **Aggiungi nuovo progetto** la finestra di dialogo, fare clic su **Visual c#** (se **Visual c#** non è visualizzato, cercarlo in **altri linguaggi**), selezionare hello **Applicazione console (.NET Framework)** , modello e denominarlo **EchoClient**.
   3. Fare clic su **OK**.
      <br />
2. In Esplora soluzioni fare doppio clic sul file Program.cs hello in hello **EchoClient** progetto tooopen possa nell'editor di hello, se non è già aperta.
3. Spazio dei nomi hello Modifica nome predefinito di `EchoClient` troppo`Microsoft.ServiceBus.Samples`.
4. Installare hello [pacchetto NuGet di Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus): in Esplora soluzioni fare doppio clic su hello **EchoClient** del progetto e quindi fare clic su **Gestisci pacchetti NuGet**. Fare clic su hello **Sfoglia** tab, quindi cercare `Microsoft Azure Service Bus`. Fare clic su **installare**e accettare le condizioni di hello d'uso.

    ![][3]
5. Aggiungere un `using` istruzione per hello [System. ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) dello spazio dei nomi nel file Program.cs hello.

    ```csharp
    using System.ServiceModel;
    ```
6. Aggiungere hello contratto definizione toohello spazio dei nomi servizio, come illustrato nell'esempio seguente hello. Si noti che questa definizione è identica toohello definizione hello **servizio** progetto. È necessario aggiungere il codice nella parte superiore di hello di hello `Microsoft.ServiceBus.Samples` dello spazio dei nomi.

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. Premere **Ctrl + MAIUSC + B** client hello toobuild.

### <a name="example"></a>Esempio

Hello codice seguente viene illustrato lo stato corrente di hello del file Program.cs hello in hello **EchoClient** progetto.

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }


    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="configure-hello-wcf-client"></a>Configurare il client WCF hello

In questo passaggio si crea un file app. config per un'applicazione client di base che accede al servizio hello creato in precedenza in questa esercitazione. Questo file app. config definisce il contratto di hello, associazione e nome dell'endpoint hello. Nell'esempio hello hello procedura viene fornito codice di Hello utilizzato per queste attività.

1. In Esplora soluzioni, in hello **EchoClient** progetto, fare doppio clic su **app** file hello tooopen nell'editor di Visual Studio hello.
2. In hello `<appSettings>` elemento, sostituire i segnaposto hello con nome hello dello spazio dei nomi di servizio e hello chiave di firma di accesso condiviso che è stato copiato in un passaggio precedente.
3. Nell'elemento System. ServiceModel hello, aggiungere un `<client>` elemento.

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <client>
        </client>
      </system.serviceModel>
    </configuration>
    ```

    Questo passaggio dichiara che si sta definendo un'applicazione client di tipo WCF.
4. All'interno di hello `client` elemento, definire il nome di hello, contratto e il tipo di associazione per l'endpoint di hello.

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    Questo passaggio definisce il nome di hello dell'endpoint hello contratto hello definito nel servizio hello e dei fatti hello che un'applicazione hello client utilizza toocommunicate TCP con l'inoltro di Azure. Hello nome dell'endpoint viene usato in hello passaggio successivo toolink questa configurazione endpoint con l'URI del servizio hello.
5. Fare clic su **File** quindi su **Salva tutto**.

## <a name="example"></a>Esempio

Hello codice seguente viene illustrato il file app. config hello per client Echo hello.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <client>
      <endpoint name="RelayEndpoint"
                      contract="Microsoft.ServiceBus.Samples.IEchoContract"
                      binding="netTcpRelayBinding"/>
    </client>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="implement-hello-wcf-client"></a>Client WCF di implementare hello
In questo passaggio è implementare un'applicazione client di base che accede al servizio hello creato in precedenza in questa esercitazione. Servizio toohello simile, hello client esegue molte delle hello stesso operazioni tooaccess inoltro di Azure:

1. Imposta la modalità di connettività hello.
2. Crea hello URI che individua il servizio host hello.
3. Definisce le credenziali di sicurezza hello.
4. Si applica hello credenziali toohello connessione.
5. Apre connessione hello.
6. Esegue attività specifiche dell'applicazione hello.
7. Chiude la connessione hello.

Tuttavia, una delle principali differenze hello è che un'applicazione hello client utilizza un servizio di inoltro toohello tooconnect di canale, mentre il servizio hello utilizza una chiamata troppo**ServiceHost**. Nell'esempio hello hello procedura viene fornito codice di Hello utilizzato per queste attività.

### <a name="implement-a-client-application"></a>Implementare un'applicazione client
1. Impostare la modalità di connettività hello troppo**AutoDetect**. Aggiungere hello seguente codice all'interno di hello `Main()` metodo hello **EchoClient** dell'applicazione.

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. Definire toohold hello i valori delle variabili per spazio dei nomi servizio hello e la chiave di firma di accesso condiviso che vengono letti dalla console hello.

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. Creare hello URI che definisce il percorso di hello dell'host hello nel progetto di inoltro.

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. Creare l'oggetto credenziale hello per l'endpoint dello spazio dei nomi del servizio.

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. Creare hello channel factory che carica la configurazione di hello descritte nel file app. config hello.

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    Una channel factory è un oggetto WCF che crea un canale attraverso il quale comunicano hello servizi e applicazioni client.
6. Applicare le credenziali di hello.

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. Creare e aprire il canale toohello servizio hello.

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. Scrivere l'interfaccia utente di base hello e funzionalità per echo hello.

    ```csharp
    Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
    string input = Console.ReadLine();
    while (input != String.Empty)
    {
        try
        {
            Console.WriteLine("Server echoed: {0}", channel.Echo(input));
        }
        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.Message);
        }
        input = Console.ReadLine();
    }
    ```

    Si noti che il codice hello utilizza istanza hello oggetto channel hello come proxy per il servizio di hello.
9. Chiudere il canale hello e factory hello Chiudi.

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="example"></a>Esempio

Il codice completato compariranno come indicato di seguito, che mostra come toocreate un'applicazione client, come toocall hello operazioni del servizio hello e come tooclose hello client dopo un'operazione di hello chiama viene completato.

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;


            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS Key: ");
            string sasKey = Console.ReadLine();



            Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));

            channelFactory.Endpoint.Behaviors.Add(sasCredential);

            IEchoChannel channel = channelFactory.CreateChannel();
            channel.Open();

            Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
            string input = Console.ReadLine();
            while (input != String.Empty)
            {
                try
                {
                    Console.WriteLine("Server echoed: {0}", channel.Echo(input));
                }
                catch (Exception e)
                {
                    Console.WriteLine("Error: " + e.Message);
                }
                input = Console.ReadLine();
            }

            channel.Close();
            channelFactory.Close();

        }
    }
}
```

## <a name="run-hello-applications"></a>Eseguire applicazioni hello

1. Premere **Ctrl + MAIUSC + B** soluzione hello toobuild. Verranno compilati il progetto di client hello sia progetto servizio hello creato nei passaggi precedenti hello.
2. Prima dell'applicazione client hello in esecuzione, è necessario assicurarsi che un'applicazione hello servizio sia in esecuzione. In Esplora soluzioni in Visual Studio, fare doppio clic su hello **EchoService** soluzione, quindi fare clic su **proprietà**.
3. Nella finestra proprietà di hello soluzione, fare clic su **progetto di avvio**, quindi fare clic su hello **più progetti di avvio** pulsante. Assicurarsi che **EchoService** visualizzata per prima nell'elenco di hello.
4. Set hello **azione** casella per entrambi hello **EchoService** e **EchoClient** progetti troppo**avviare**.

    ![][5]
5. Fare clic su **Dipendenze progetto**. In hello **progetti** , quindi selezionare **EchoClient**. In hello **dipende** verificare **EchoService** è selezionata.

    ![][6]
6. Fare clic su **OK** toodismiss hello **proprietà** finestra di dialogo.
7. Premere **F5** toorun entrambi i progetti.
8. Richiesto per il nome dello spazio dei nomi hello in entrambe le finestre della console della finestra. Hello servizio deve essere eseguito in primo luogo, in hello **EchoService** finestra della console, immettere lo spazio dei nomi hello e quindi premere **invio**.
9. Verrà quindi chiesto di specificare la chiave di firma di accesso condiviso. Immettere una chiave SAS hello e premere INVIO.

    Di seguito è riportato l'output dalla finestra di console hello. Si noti che i valori hello fornito di seguito sono ad esempio a solo scopo.

    `Your Service Namespace: myNamespace``Your SAS Key: <SAS key value>`

    applicazione di servizio Hello stampa indirizzo hello finestra console toohello su cui è in ascolto, come illustrato nel seguente esempio hello.

    `Service address: sb://mynamespace.servicebus.windows.net/EchoService/``Press [Enter] tooexit`
10. In hello **EchoClient** finestra della console, immettere hello corrispondono a quelle immesse in precedenza per l'applicazione di servizio hello. Seguire hello tooenter passaggi precedenti di hello stesso spazio dei nomi servizio e SAS valori per un'applicazione client hello di chiave.
11. Dopo aver immesso questi valori, client hello apre un servizio toohello di canale e richiede tooenter è testo, come illustrato nel seguente esempio di output di console hello.

    `Enter text tooecho (or [Enter] tooexit):`

    Immettere un'applicazione di servizio toohello toosend testo e premere INVIO. Questo testo viene inviato toohello servizio tramite l'operazione del servizio Echo hello e viene visualizzato nella finestra della console hello servizio come illustrato di seguito l'output di esempio hello.

    `Echoing: My sample text`

    un'applicazione Hello client riceve il valore restituito di hello di hello `Echo` operazione, che è il testo originale hello e stampato tooits finestra della console. esempio Hello è riportato l'output dalla finestra di console client hello.

    `Server echoed: My sample text`
12. È possibile continuare a inviare messaggi di testo dal servizio di toohello hello client in questo modo. Al termine, premere INVIO in hello tooend windows console client e servizio entrambe le applicazioni.

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione è stato illustrato come toobuild un'applicazione client di inoltro di Azure e un servizio usando hello funzionalità di inoltro WCF del Bus di servizio. Per un'esercitazione simile che usa la [messaggistica](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging) del bus di servizio, vedere [Introduzione alle code del bus di servizio](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).

toolearn ulteriori informazioni sull'inoltro di Azure, vedere i seguenti argomenti hello.

* [Panoramica dell'architettura del bus di servizio di Azure](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [Panoramica del servizio di inoltro di Azure](relay-what-is-it.md)
* [Come servizio con .NET di inoltro toouse hello WCF](relay-wcf-dotnet-get-started.md)

[Azure classic portal]: http://manage.windowsazure.com

[2]: ./media/service-bus-relay-tutorial/create-console-app.png
[3]: ./media/service-bus-relay-tutorial/install-nuget.png
[5]: ./media/service-bus-relay-tutorial/set-projects.png
[6]: ./media/service-bus-relay-tutorial/set-depend.png
