---
title: esercitazione REST Bus aaaService con l'inoltro di Azure | Documenti Microsoft
description: Compilare una semplice applicazione host di inoltro del bus di servizio di Azure che espone un'interfaccia basata su REST.
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1312b2db-94c4-4a48-b815-c5deb5b77a6a
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2017
ms.author: sethm
ms.openlocfilehash: b68650993a0390e7cef891ccb4236095cd86d4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-rest-tutorial"></a>Esercitazione su REST per l'inoltro WCF di Azure

In questa esercitazione viene descritto come un semplice inoltro Azure toobuild host applicazione che espone un'interfaccia basata su REST. REST consente a un client web, ad esempio un web browser, hello tooaccess le richieste API del Bus di servizio tramite HTTP.

esercitazione Hello utilizza tooconstruct programmazione modello hello REST di Windows Communication Foundation (WCF) un servizio REST sul Bus di servizio. Per ulteriori informazioni, vedere [il modello di programmazione REST WCF](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) e [progettazione e implementazione di servizi](/dotnet/framework/wcf/designing-and-implementing-services) in hello documentazione WCF.

## <a name="step-1-create-a-namespace"></a>Passaggio 1: Creare uno spazio dei nomi

utilizzando toobegin hello le funzionalità di inoltro in Azure, è innanzitutto necessario creare uno spazio dei nomi del servizio. Uno spazio dei nomi funge da contenitore di ambito in cui indirizzare le risorse di Azure nell'applicazione. Seguire hello [le istruzioni qui](relay-create-namespace-portal.md) toocreate uno spazio dei nomi di inoltro.

## <a name="step-2-define-a-rest-based-wcf-service-contract-toouse-with-azure-relay"></a>Passaggio 2: Definire un toouse contratto di servizio WCF basato su REST con l'inoltro di Azure

Quando si crea un servizio in stile REST WCF, è necessario definire il contratto di hello. contratto Hello specifica quali operazioni hello host supporta. Un'operazione di servizio può essere considerata come un metodo del servizio Web. I contratti vengono creati definendo un'interfaccia C++, C# o Visual Basic. Ogni metodo nell'interfaccia hello corrisponde tooa operazione del servizio specifica. Hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attributo deve essere applicato tooeach interfaccia e hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attributo deve essere applicato tooeach operazione. Se un metodo in un'interfaccia con hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) privo di hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), questo metodo non è esposto. codice Hello usato per queste attività è illustrata nell'esempio hello procedura hello.

la differenza principale tra un contratto WCF e un contratto in stile REST Hello è hello aggiunta di una proprietà di toohello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx). Questa proprietà consente di toomap un metodo al metodo di interfaccia tooa su hello altro lato dell'interfaccia hello. In questo caso, si utilizzerà [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) toolink tooHTTP un metodo GET. In questo modo il Bus di servizio tooaccurately recuperare e interpretare i comandi inviati toohello interfaccia.

### <a name="toocreate-a-contract-with-an-interface"></a>un contratto con un'interfaccia toocreate

1. Aprire Visual Studio come amministratore: il programma hello pulsante destro del mouse in hello **avviare** menu e quindi fare clic su **Esegui come amministratore**.
2. Creare un nuovo progetto di applicazione console. Fare clic su hello **File** dal menu **New**, quindi selezionare **progetto**. In hello **nuovo progetto** nella finestra di dialogo fare clic su **Visual c#**selezionare hello **applicazione Console** , modello e specificare il nome **ImageListener**. Utilizzare hello predefinito **percorso**. Fare clic su **OK** progetto hello toocreate.
3. Per un progetto C#, Visual Studio crea un file `Program.cs`. Questa classe contiene un oggetto vuoto `Main()` (metodo), necessari per un toobuild di progetto applicazione console in modo corretto.
4. Aggiungere riferimenti tooService Bus e **System.ServiceModel.dll** toohello progetto per l'installazione del pacchetto NuGet di Service Bus hello. Questo pacchetto aggiunge automaticamente le librerie del Bus di servizio toohello riferimenti, nonché hello WCF **System. ServiceModel**. In Esplora soluzioni fare doppio clic su hello **ImageListener** del progetto e quindi fare clic su **Gestisci pacchetti NuGet**. Fare clic su hello **Sfoglia** tab, quindi cercare `Microsoft Azure Service Bus`. Fare clic su **installare**e accettare le condizioni di hello d'uso.
5. È necessario aggiungere in modo esplicito un riferimento troppo**System.ServiceModel.Web.dll** toohello progetto:
   
    a. In Esplora soluzioni fare doppio clic su hello **riferimenti** nella cartella di progetto hello, quindi fare clic su **Aggiungi riferimento**.
   
    b. In hello **Aggiungi riferimento** finestra di dialogo fare clic su hello **Framework** scheda sul lato sinistro hello e hello **ricerca** digitare **System.ServiceModel.Web** . Seleziona hello **System.ServiceModel.Web** casella di controllo, quindi fare clic su **OK**.
6. Aggiungere il seguente hello `using` istruzioni nella parte superiore di hello del file Program.cs hello.
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    [System. ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) uno spazio dei nomi hello che abilita l'accesso programmatico toobasic funzionalità di WCF. Inoltro WCF Usa molti degli oggetti hello e degli attributi WCF toodefine di contratti di servizio. Questo spazio dei nomi viene usato nella maggior parte delle applicazioni di inoltro. Analogamente, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) consentono di definire il canale hello, ovvero hello oggetto usato per comunicare con l'inoltro di Azure e hello web browser client. Infine, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contiene i tipi di hello che consentono di applicazioni basate sul web toocreate.
7. Rinominare hello `ImageListener` dello spazio dei nomi troppo**ServiceBus**.
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. Dopo la parentesi graffa di dichiarazione dello spazio dei nomi hello di hello, è possibile definire direttamente una nuova interfaccia denominata **IImageContract** e applicare hello **ServiceContractAttribute** interfaccia toohello attributo con un valore di `http://samples.microsoft.com/ServiceModel/Relay/`. il valore di spazio dei nomi Hello è diverso dallo spazio dei nomi hello usato nell'ambito di hello del codice. valore dello spazio dei nomi Hello viene usato come identificatore univoco per questo contratto e deve disporre di informazioni sulla versione. Per altre informazioni, vedere [Controllo delle versioni del servizio](http://go.microsoft.com/fwlink/?LinkID=180498). Specificare in modo esplicito lo spazio dei nomi hello impedisce l'aggiunta il nome del contratto toohello valore dello spazio dei nomi predefinito di hello.
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. All'interno di hello `IImageContract` l'interfaccia, dichiarare un metodo per hello singola operazione hello `IImageContract` espone contratto in hello interfaccia e applicare hello `OperationContractAttribute` attributo toohello metodo che si vuole tooexpose come parte del servizio pubblico hello Bus contratto.
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. In hello **OperationContract** attributo, aggiungere hello **WebGet** valore.
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    In questo modo consente hello tooroute servizio di inoltro richieste HTTP GET troppo`GetImage`, hello tootranslate restituiscono i valori e `GetImage` in una risposta HTTP GETRESPONSE. Più avanti nell'esercitazione di hello, si utilizzerà un tooaccess browser web, questo metodo e immagine hello toodisplay nel browser hello.
11. Direttamente dopo hello `IImageContract` definizione, dichiarare un canale che eredita da entrambi hello `IImageContract` e `IClientChannel` interfacce.
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    Un canale è l'oggetto WCF hello attraverso cui client e servizio hello passare informazioni tooeach altri. In un secondo momento, si creerà il canale hello nell'applicazione host. Inoltro Azure utilizza quindi questo canale toopass hello richieste GET HTTP dal hello browser tooyour **GetImage** implementazione. inoltro Hello utilizza inoltre hello di hello canale tootake **GetImage** valore restituito e viene convertito in una risposta HTTP GETRESPONSE per browser client hello.
12. Da hello **compilare** menu, fare clic su **Compila soluzione** accuratezza hello tooconfirm del lavoro svolto finora.

### <a name="example"></a>Esempio
Hello di codice seguente mostra un'interfaccia di base che definisce un contratto di inoltro WCF.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="step-3-implement-a-rest-based-wcf-service-contract-toouse-service-bus"></a>Passaggio 3: Implementare un toouse di contratto del servizio Bus di servizio WCF basato su REST
Creazione di un servizio di inoltro WCF di tipo REST è necessario innanzitutto creare contratto hello, che viene definito tramite un'interfaccia. passaggio successivo Hello è interfaccia hello tooimplement. Ciò comporta la creazione di una classe denominata **ImageService** che implementa hello definito dall'utente **IImageContract** interfaccia. Dopo aver implementato il contratto di hello, configurare l'interfaccia hello utilizzando un file app. config. file di configurazione Hello contiene le informazioni necessarie per un'applicazione hello, ad esempio nome hello del servizio di hello, il nome di hello del contratto hello e tipo hello di protocollo è toocommunicate utilizzato con il servizio di inoltro hello. Nell'esempio hello hello procedura viene fornito codice di Hello utilizzato per queste attività.

Come con i passaggi precedenti hello, c'è differenza minima tra l'implementazione di un contratto in stile REST e un contratto di inoltro WCF.

### <a name="tooimplement-a-rest-style-service-bus-contract"></a>contratto del Bus di servizio tooimplement un stile REST
1. Creare una nuova classe denominata **ImageService** direttamente dopo la definizione di hello di hello **IImageContract** interfaccia. Hello **ImageService** implementa hello **IImageContract** interfaccia.
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    Le implementazioni di interfaccia tooother simili, è possibile implementare definizione hello in un file diverso. Tuttavia, per questa esercitazione, implementazione hello viene visualizzato in hello lo stesso file di definizione di interfaccia hello e `Main()` metodo.
2. Applicare hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attributo toohello **IImageService** tooindicate di classe che hello classe è un'implementazione di un contratto WCF.
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    Come accennato in precedenza, questo spazio dei nomi non è uno spazio dei nomi tradizionale. In alternativa, è parte dell'architettura WCF che identifica il contratto di hello hello. Per ulteriori informazioni, vedere hello [nomi di contratto dati](https://msdn.microsoft.com/library/ms731045.aspx) argomento nella documentazione di WCF hello.
3. Aggiungere un progetto di tooyour immagine jpg.  
   
    Si tratta di un'immagine contenente il servizio hello in hello browser di ricezione. Fare clic con il pulsante destro del mouse sul progetto e quindi scegliere **Aggiungi**. Fare clic su **Elemento esistente**. Hello utilizzare **Aggiungi elemento esistente** della finestra di dialogo toobrowse tooan appropriato. jpg e quindi fare clic su **Aggiungi**.
   
    Quando si aggiungono file hello, assicurarsi che **tutti i file** è selezionata in hello riepilogo Avanti toohello **nome File:** campo. rest Hello di questa esercitazione si presuppone che hello nome dell'immagine di hello sia "image.jpg". Se si dispone di un file diverso, si verrà toorename hello immagine o modificare il codice toocompensate.
4. Assicurarsi che hello in esecuzione del servizio è possibile trovare il file di immagine hello, in toomake **Esplora soluzioni** fare clic sul file di immagine hello, quindi fare clic su **proprietà**. In hello **proprietà** riquadro, impostare **copiare tooOutput Directory** troppo**copia se più recente**.
5. Aggiungere un riferimento toohello **System.Drawing.dll** toohello di assembly del progetto e aggiungere associate riportate di seguito hello `using` istruzioni.  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. In hello **ImageService** classe, aggiungere hello seguenti costruttore che carica hello bitmap e prepara toosend il browser client toohello.
   
    ```csharp
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";
   
        Image bitmap;
   
        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }
    }
    ```
7. Direttamente dopo il codice precedente hello, aggiungere il seguente hello **GetImage** metodo hello **ImageService** messaggio tooreturn HTTP di classe che contiene l'immagine di hello.
   
    ```csharp
    public Stream GetImage()
    {
        MemoryStream stream = new MemoryStream();
        this.bitmap.Save(stream, ImageFormat.Jpeg);
   
        stream.Position = 0;
        WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";
   
        return stream;
    }
    ```
   
    Questa implementazione utilizza **MemoryStream** tooretrieve hello immagine e prepararla per lo streaming toohello browser. Avvia la posizione del flusso hello da zero, dichiara il contenuto di flusso hello in formato jpeg e flussi di informazioni hello.
8. Da hello **compilare** menu, fare clic su **Compila soluzione**.

### <a name="toodefine-hello-configuration-for-running-hello-web-service-on-service-bus"></a>configurazione di hello toodefine per l'esecuzione del servizio web hello sul Bus di servizio
1. In **Esplora**, fare doppio clic su **app** tooopen nell'editor di Visual Studio hello.
   
    Hello **app** file include il nome di servizio hello endpoint (vale a dire hello location inoltro Azure espone per i client e host toocommunicate reciprocamente) e associazione (tipo hello di protocollo utilizzato toocommunicate). Hello differenza principale è tale endpoint di servizio hello configurato si riferisce tooa [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) associazione.
2. Hello `<system.serviceModel>` elemento XML è un elemento WCF che definisce uno o più servizi. In questo caso, è endpoint e nome del servizio utilizzato toodefine hello. Nella parte inferiore di hello di hello `<system.serviceModel>` elemento (ma si trovano all'interno `<system.serviceModel>`), aggiungere un `<bindings>` elemento che dispone di hello dopo contenuto. Definisce le associazioni hello usate in un'applicazione hello. È possibile definire più associazioni, ma per questa esercitazione se ne definisce una sola.
   
    ```xml
    <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
            <binding name="default">
                <security relayClientAuthenticationType="None" />
            </binding>
        </webHttpRelayBinding>
    </bindings>
    ```
   
    codice precedente Hello definisce un inoltro WCF [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding con **relayClientAuthenticationType** impostare troppo**Nessuno**. Questa impostazione indica che un endpoint che utilizza questa associazione non richiede le credenziali client.
3. Dopo aver hello `<bindings>` elemento, aggiungere un `<services>` elemento. Associazioni toohello simili, è possibile definire più servizi in un file di configurazione. Tuttavia, per questa esercitazione, se ne definisce solo uno.
   
    ```xml
    <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
            <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IImageContract"
                    binding="webHttpRelayBinding"
                    bindingConfiguration="default"
                    behaviorConfiguration="sbTokenProvider"
                    address="" />
        </service>
    </services>
    ```
   
    Questo passaggio Configura un servizio che utilizza valori predefiniti definito in precedenza hello **webHttpRelayBinding**. Utilizza inoltre il valore predefinito di hello **sbTokenProvider**, che è definito nel passaggio successivo hello.
4. Dopo aver hello `<services>` elemento, creare un `<behaviors>` elemento con hello contenuto seguente, sostituendo "SAS_KEY" con hello *firma di accesso condiviso* chiave (SAS) è stato ottenuto in precedenza da hello [portale di Azure ][Azure portal].
   
    ```xml
    <behaviors>
        <endpointBehaviors>
            <behavior name="sbTokenProvider">
                <transportClientEndpointBehavior>
                    <tokenProvider>
                        <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
                    </tokenProvider>
                </transportClientEndpointBehavior>
            </behavior>
            </endpointBehaviors>
            <serviceBehaviors>
                <behavior name="default">
                    <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
                </behavior>
            </serviceBehaviors>
    </behaviors>
    ```
5. Ancora in App. config, hello `<appSettings>` elemento, valore di stringa di sostituzione hello intera connessione con stringa di connessione hello ottenuto dal portale hello in precedenza. 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. Da hello **compilare** menu, fare clic su **Compila soluzione** dell'intera soluzione hello toobuild.

### <a name="example"></a>Esempio
Hello codice seguente viene illustrato implementazione hello di contratto e del servizio per un servizio basato su REST che è in esecuzione sul Bus di servizio utilizzando hello **WebHttpRelayBinding** associazione.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{


    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

Hello riportato di seguito hello file app. config associato al servizio hello.

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
    </startup>
    <system.serviceModel>
        <extensions>
            <!-- In this extension section we are introducing all known service bus extensions. User can remove hello ones they don't need. -->
            <behaviorExtensions>
                <add name="connectionStatusBehavior"
                    type="Microsoft.ServiceBus.Configuration.ConnectionStatusElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="transportClientEndpointBehavior"
                    type="Microsoft.ServiceBus.Configuration.TransportClientEndpointBehaviorElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="serviceRegistrySettings"
                    type="Microsoft.ServiceBus.Configuration.ServiceRegistrySettingsElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </behaviorExtensions>
            <bindingElementExtensions>
                <add name="netMessagingTransport"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingTransportExtensionElement, Microsoft.ServiceBus,  Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="tcpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.TcpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpsRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpsRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="onewayRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.RelayedOnewayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingElementExtensions>
            <bindingExtensions>
                <add name="basicHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.BasicHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="webHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WebHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="ws2007HttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WS2007HttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netOnewayRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetOnewayRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netEventRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetEventRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netMessagingBinding"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingExtensions>
        </extensions>
      <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
          <binding name="default">
            <security relayClientAuthenticationType="None" />
          </binding>
        </webHttpRelayBinding>
      </bindings>
      <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
          <endpoint name="RelayEndpoint"
                  contract="Microsoft.ServiceBus.Samples.IImageContract"
                  binding="webHttpRelayBinding"
                  bindingConfiguration="default"
                  behaviorConfiguration="sbTokenProvider"
                  address="" />
        </service>
      </services>
      <behaviors>
        <endpointBehaviors>
          <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
              <tokenProvider>
                <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
              </tokenProvider>
            </transportClientEndpointBehavior>
          </behavior>
        </endpointBehaviors>
        <serviceBehaviors>
          <behavior name="default">
            <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
          </behavior>
        </serviceBehaviors>
      </behaviors>
    </system.serviceModel>
    <appSettings>
        <!-- Service Bus specific app setings for messaging connections -->
        <add key="Microsoft.ServiceBus.ConnectionString"
            value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey="YOUR_SAS_KEY"/>
    </appSettings>
</configuration>
```

## <a name="step-4-host-hello-rest-based-wcf-service-toouse-azure-relay"></a>Passaggio 4: Host toouse di servizio WCF basato su REST hello Azure inoltro
Questo passaggio viene descritto come toorun un sito web del servizio con un'applicazione console relè WCF. Nell'esempio hello hello procedura, viene fornito un elenco completo del codice hello scritto in questo passaggio.

### <a name="toocreate-a-base-address-for-hello-service"></a>un indirizzo di base per il servizio hello toocreate
1. In hello `Main()` dichiarazione di funzione, creare uno spazio dei nomi di variabile toostore hello del progetto. Verificare che tooreplace `yourNamespace` con nome hello dello spazio dei nomi di inoltro hello creato in precedenza.
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    Bus di servizio utilizza il nome di hello del toocreate dello spazio dei nomi, un URI univoco.
2. Creare un `Uri` istanza per l'indirizzo di base hello servizio hello basato sullo spazio dei nomi hello.
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="toocreate-and-configure-hello-web-service-host"></a>toocreate e configurare l'host del servizio web hello
* Creare l'host del servizio web hello, utilizzando l'indirizzo URI hello creato in precedenza in questa sezione.
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    host del servizio Hello è oggetto WCF hello che crea un'istanza di un'applicazione hello host. Questo esempio passa il tipo di hello dell'host si desidera toocreate (un **ImageService**), e anche hello indirizzo in cui si desidera un'applicazione host tooexpose hello.

### <a name="toorun-hello-web-service-host"></a>host del servizio web hello toorun
1. Aprire il servizio di hello.
   
    ```csharp
    host.Open();
    ```
    servizio Hello è in esecuzione.
2. Visualizzare un messaggio che indica che è in esecuzione il servizio hello e come toostop hello del servizio.
   
    ```csharp
    Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. Al termine, chiudere l'host del servizio hello.
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a>Esempio
Hello di esempio seguente include il contratto di servizio hello e l'implementazione dai passaggi precedenti nel servizio di hello di esercitazione e ospita hello in un'applicazione console. Compilare hello seguente di codice in un file eseguibile chiamato ImageListener.exe.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string serviceNamespace = "InsertServiceNamespaceHere";
            Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");

            WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
            host.Open();

            Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
            Console.WriteLine(address + "GetImage");
            Console.WriteLine();
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            host.Close();
        }
    }
}
```

### <a name="compiling-hello-code"></a>La compilazione di codice hello
Dopo aver compilato la soluzione hello, hello in seguito un'applicazione hello toorun:

1. Premere **F5**, o percorso del file eseguibile toohello (ImageListener\bin\Debug\ImageListener.exe), il servizio di hello toorun Sfoglia. Mantenere hello app in esecuzione, come passaggio successivo di tooperform hello è obbligatoria.
2. Copiare e incollare l'indirizzo di hello dal prompt dei comandi di hello in un'immagine di hello toosee browser.
3. Al termine, premere **invio** in app di hello tooclose finestra prompt dei comandi hello.

## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato un'applicazione che utilizza il servizio di inoltro di hello Bus di servizio, vedere hello seguente toolearn articoli più sull'inoltro di Azure:

* [Panoramica dell'architettura del bus di servizio di Azure](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* [Panoramica del servizio di inoltro di Azure](relay-what-is-it.md)
* [Come servizio con .NET di inoltro toouse hello WCF](relay-wcf-dotnet-get-started.md)

[Azure portal]: https://portal.azure.com
