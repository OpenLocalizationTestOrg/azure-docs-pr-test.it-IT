---
title: applicazione in locale/cloud ibrida di inoltro WCF (.NET) aaaAzure | Documenti Microsoft
description: Informazioni su come applicazione ibrida toocreate un .NET in locale/cloud tramite Azure un inoltro WCF.
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 9ed02f7c-ebfb-4f39-9c97-b7dc15bcb4c1
ms.service: service-bus-relay
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/14/2017
ms.author: sethm
ms.openlocfilehash: aab8b1dbdc85c4edf7b0ccef0921b69524b2d306
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a>Applicazione ibrida cloud/locale (.NET) usando il servizio d'inoltro WCF di Azure
## <a name="introduction"></a>Introduzione

Questo articolo illustra come toobuild ibrido cloud applicazione con Microsoft Azure e Visual Studio. esercitazione Hello presuppone che si ha alcuna esperienza precedente con Azure. In meno di 30 minuti, si disporrà di un'applicazione che utilizza più risorse di Azure backup e in esecuzione nel cloud hello.

Si acquisiranno le nozioni seguenti:

* Come toocreate o adattare un servizio web esistente per l'utilizzo da una soluzione web.
* Come dati toouse hello Azure WCF Relay service tooshare tra un'applicazione Azure e un servizio web ospitato in un' posizione.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a>Vantaggi del servizio d'inoltro di Azure con soluzioni ibride

Soluzioni di business sono in genere costituite da una combinazione di codice personalizzato scritto tootackle nuovo e requisiti aziendali e le funzionalità esistenti fornito da soluzioni e i sistemi che sono già presenti.

Architetti di soluzioni cloud hello toouse per una gestione più semplice di requisiti di scalabilità e ridurre i costi operativi sono in avvio. In questo modo, individuano che le risorse di servizio che preferiscono tooleverage come blocchi predefiniti per le relative soluzioni sono all'interno di firewall aziendale hello e all'esterno di facile raggiungono per l'accesso dalla soluzione di cloud hello. Molti servizi interni non vengono compilati o ospitati in modo che essi possono essere facilmente esposti perimetrale alla rete aziendale hello.

[Inoltro Azure](https://azure.microsoft.com/services/service-bus/) è progettato per hello caso d'uso di servizi web di Windows Communication Foundation (WCF) esistente e rendere tali servizi in modo sicuro accessibile toosolutions che risiedono all'esterno di perimetrale aziendale hello senza infrastruttura della rete aziendale toohello modifiche intrusiva. Tali servizi di inoltro sono ospitate all'interno all'ambiente esistente, ma viene delegato in attesa di servizio in arrivo sessioni e richieste toohello inoltro ospitato su cloud. Il servizio d'inoltro di Azure protegge anche quei servizi dall'accesso non autorizzato tramite l'autenticazione con [firma di accesso condiviso](../service-bus-messaging/service-bus-sas.md).

## <a name="solution-scenario"></a>Scenario della soluzione
In questa esercitazione si creerà un sito Web ASP.NET che consente di toosee un elenco di prodotti nella pagina di inventario del prodotto hello.

![][0]

esercitazione Hello presuppone che si dispone di informazioni sui prodotti in un sistema locale esistente e che utilizza Azure inoltro tooreach in tale sistema. Tale operazione viene simulata da un servizio Web eseguito in una semplice applicazione console ed è supportata da un insieme di prodotti in memoria. Si verrà toorun in grado di questa applicazione console nel proprio computer e la distribuzione di ruolo web hello in Azure. In questo modo, si noterà come ruolo web hello in esecuzione in Data Center di Azure hello verrà effettivamente chiamato nel computer, anche se il computer verrà quasi certamente sono protetti da almeno un firewall e un livello di translation (NAT) indirizzo di rete.

## <a name="set-up-hello-development-environment"></a>Configurare un ambiente di sviluppo hello

Prima di iniziare lo sviluppo di applicazioni Azure, scaricare gli strumenti di hello e configurare l'ambiente di sviluppo:

1. Installare hello Azure SDK per .NET da hello SDK [pagina di download](https://azure.microsoft.com/downloads/).
2. In hello **.NET** colonna, fare clic sulla versione di hello di [Visual Studio](http://www.visualstudio.com) in uso. Hello i passaggi in questa esercitazione usare Visual Studio 2015, ma funzionano anche con Visual Studio 2017.
3. Quando viene chiesto di toorun o salvare installer hello, fare clic su **eseguire**.
4. In hello **installazione guidata piattaforma Web**, fare clic su **installare** e continuare l'installazione di hello.
5. Al termine dell'installazione di hello, sarà necessario tutto il necessario toostart toodevelop hello app. Hello SDK include strumenti che consentono di sviluppare facilmente applicazioni Azure in Visual Studio.

## <a name="create-a-namespace"></a>Creare uno spazio dei nomi

utilizzando toobegin hello le funzionalità di inoltro in Azure, è innanzitutto necessario creare uno spazio dei nomi del servizio. Uno spazio dei nomi funge da contenitore di ambito in cui indirizzare le risorse di Azure nell'applicazione. Seguire hello [le istruzioni qui](relay-create-namespace-portal.md) toocreate uno spazio dei nomi di inoltro.

## <a name="create-an-on-premises-server"></a>Creare un server locale

In primo luogo, si creerà un sistema di catalogo prodotti locale fittizio. Sarà piuttosto semplice. si noterà come rappresenta un sistema di catalogo locale effettivo del prodotto con una superficie completa del servizio che si sta tentando di toointegrate.

Questo progetto è un'applicazione console Visual Studio e utilizza hello [pacchetto NuGet di Azure Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude hello le librerie del Bus di servizio e le impostazioni di configurazione.

### <a name="create-hello-project"></a>Creare il progetto hello

1. Usando privilegi di amministratore, avviare Microsoft Visual. In tal caso, fare doppio clic sull'icona di programma Visual Studio hello toodo e quindi fare clic su **Esegui come amministratore**.
2. In Visual Studio, su hello **File** menu, fare clic su **New**, quindi fare clic su **progetto**.
3. Da **Modelli installati** in **Visual C#** fare clic su **App console (.NET Framework)**. In hello **nome** casella, il nome del tipo hello **ProductsServer**:

   ![][11]
4. Fare clic su **OK** toocreate hello **ProductsServer** progetto.
5. Se Gestione di pacchetti hello NuGet per Visual Studio è già stato installato, ignorare toohello successivo. In caso contrario, visitare il sito [NuGet][NuGet] e fare clic su [Install NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) (Installa NuGet). Seguire hello richieste tooinstall hello di gestione pacchetti NuGet, quindi riavviare Visual Studio.
6. In Esplora soluzioni fare doppio clic su hello **ProductsServer** del progetto, quindi fare clic su **Gestisci pacchetti NuGet**.
7. Fare clic su hello **Sfoglia** tab, quindi cercare `Microsoft Azure Service Bus`. Seleziona hello **Windowsazure** pacchetto.
8. Fare clic su **installare**e accettare le condizioni di hello d'uso.

   ![][13]

   Si noti che hello necessari assembly client fa riferimento a questo punto.
8. Aggiungere una nuova classe per il contratto dei prodotti. In Esplora soluzioni fare doppio clic su hello **ProductsServer** sul progetto e scegliere **Aggiungi**, quindi fare clic su **classe**.
9. In hello **nome** casella, il nome del tipo hello **ProductsContract.cs**. Fare quindi clic su **Aggiungi**.
10. In **ProductsContract.cs**, sostituire definizione dello spazio dei nomi di hello con hello seguente di codice, che definisce il contratto di hello del servizio di hello.

    ```csharp
    namespace ProductsServer
    {
        using System.Collections.Generic;
        using System.Runtime.Serialization;
        using System.ServiceModel;

        // Define hello data contract for hello service
        [DataContract]
        // Declare hello serializable properties.
        public class ProductData
        {
            [DataMember]
            public string Id { get; set; }
            [DataMember]
            public string Name { get; set; }
            [DataMember]
            public string Quantity { get; set; }
        }

        // Define hello service contract.
        [ServiceContract]
        interface IProducts
        {
            [OperationContract]
            IList<ProductData> GetProducts();

        }

        interface IProductsChannel : IProducts, IClientChannel
        {
        }
    }
    ```
11. In Program.cs, sostituire hello seguente di codice che aggiunge il servizio di profilo hello e l'host di hello per tale definizione dello spazio dei nomi hello.

    ```csharp
    namespace ProductsServer
    {
        using System;
        using System.Linq;
        using System.Collections.Generic;
        using System.ServiceModel;

        // Implement hello IProducts interface.
        class ProductsService : IProducts
        {

            // Populate array of products for display on website
            ProductData[] products =
                new []
                    {
                        new ProductData{ Id = "1", Name = "Rock",
                                         Quantity = "1"},
                        new ProductData{ Id = "2", Name = "Paper",
                                         Quantity = "3"},
                        new ProductData{ Id = "3", Name = "Scissors",
                                         Quantity = "5"},
                        new ProductData{ Id = "4", Name = "Well",
                                         Quantity = "2500"},
                    };

            // Display a message in hello service console application
            // when hello list of products is retrieved.
            public IList<ProductData> GetProducts()
            {
                Console.WriteLine("GetProducts called.");
                return products;
            }

        }

        class Program
        {
            // Define hello Main() function in hello service application.
            static void Main(string[] args)
            {
                var sh = new ServiceHost(typeof(ProductsService));
                sh.Open();

                Console.WriteLine("Press ENTER tooclose");
                Console.ReadLine();

                sh.Close();
            }
        }
    }
    ```
12. In Esplora soluzioni fare doppio clic su hello **app** tooopen del file nell'editor di Visual Studio hello. Nella parte inferiore di hello di hello `<system.ServiceModel>` elemento (ma si trovano all'interno `<system.ServiceModel>`), aggiungere hello seguente codice XML. Tooreplace assicurarsi di essere *yourServiceNamespace* con nome hello dello spazio dei nomi, e *yourKey* con la chiave di firma di accesso condiviso hello recuperati in precedenza dal portale hello:

    ```xml
    <system.serviceModel>
    ...
      <services>
         <service name="ProductsServer.ProductsService">
           <endpoint address="sb://yourServiceNamespace.servicebus.windows.net/products" binding="netTcpRelayBinding" contract="ProductsServer.IProducts" behaviorConfiguration="products"/>
         </service>
      </services>
      <behaviors>
         <endpointBehaviors>
           <behavior name="products">
             <transportClientEndpointBehavior>
                <tokenProvider>
                   <sharedAccessSignature keyName="RootManageSharedAccessKey" key="yourKey" />
                </tokenProvider>
             </transportClientEndpointBehavior>
           </behavior>
         </endpointBehaviors>
      </behaviors>
    </system.serviceModel>
    ```
13. Ancora in App. config, hello `<appSettings>` elemento, valore di stringa di connessione hello sostituire la stringa di connessione hello ottenuto dal portale hello in precedenza.

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. Premere **Ctrl + MAIUSC + B** o da hello **compilare** menu, fare clic su **Compila soluzione** toobuild hello applicazione e verificare la correttezza hello del lavoro finora.

## <a name="create-an-aspnet-application"></a>Creare un'applicazione ASP.NET

In questa sezione si creerà una semplice applicazione ASP.NET per visualizzare i dati recuperati dal servizio dei prodotti.

### <a name="create-hello-project"></a>Creare il progetto hello

1. Assicurarsi che Visual Studio sia in esecuzione con privilegi di amministratore.
2. In Visual Studio, su hello **File** menu, fare clic su **New**, quindi fare clic su **progetto**.
3. Da **Modelli installati** in **Visual C#** fare clic su **Applicazione Web ASP.NET (.NET Framework)**. Progetto hello nome **ProductsPortal**. Fare quindi clic su **OK**.

   ![][15]

4. Da hello **modelli ASP.NET** elenco hello **nuova applicazione Web ASP.NET** finestra di dialogo, fare clic su **MVC**.

   ![][16]

6. Fare clic su hello **Modifica autenticazione** pulsante. In hello **Modifica autenticazione** finestra di dialogo, verificare che **Nessuna autenticazione** sia selezionata e quindi fare clic su **OK**. Per questa esercitazione si distribuisce un'app che non richiede l'accesso utente.

    ![][18]

7. In hello **nuova applicazione Web ASP.NET** finestra di dialogo, fare clic su **OK** toocreate hello MVC app.
8. A questo punto è necessario configurare le risorse di Azure per una nuova app Web. Seguire i passaggi hello hello [pubblicare tooAzure sezione di questo articolo](../app-service-web/app-service-web-get-started-dotnet.md). Restituire toothis esercitazione, quindi procedere toohello successivo.
10. In Esplora soluzioni fare clic con il pulsante destro del mouse su **Modelli**, scegliere **Aggiungi** e infine fare clic su **Classe**. In hello **nome** casella, il nome del tipo hello **Product.cs**. Fare quindi clic su **Aggiungi**.

    ![][17]

### <a name="modify-hello-web-application"></a>Modificare un'applicazione web hello

1. Nel file di Product.cs hello in Visual Studio, sostituire la definizione dello spazio dei nomi esistente hello con hello seguente codice.

   ```csharp
    // Declare properties for hello products inventory.
    namespace ProductsWeb.Models
    {
       public class Product
       {
           public string Id { get; set; }
           public string Name { get; set; }
           public string Quantity { get; set; }
       }
    }
    ```
2. In Esplora soluzioni espandere hello **controller** cartella, quindi fare doppio clic su hello **HomeController.cs** file tooopen in Visual Studio.
3. In **HomeController.cs**, sostituire la definizione dello spazio dei nomi esistente hello con hello seguente codice.

    ```csharp
    namespace ProductsWeb.Controllers
    {
        using System.Collections.Generic;
        using System.Web.Mvc;
        using Models;

        public class HomeController : Controller
        {
            // Return a view of hello products inventory.
            public ActionResult Index(string Identifier, string ProductName)
            {
                var products = new List<Product>
                    {new Product {Id = Identifier, Name = ProductName}};
                return View(products);
            }
         }
    }
    ```
4. In Esplora soluzioni, espandere cartella Views\Shared hello, quindi fare doppio clic su **layout. cshtml** tooopen nell'editor di Visual Studio hello.
5. Modificare tutte le occorrenze di **applicazione ASP.NET** troppo**prodotti di LITWARE**.
6. Rimuovere hello **Home**, **su**, e **contatto** collegamenti. Nell'esempio seguente di hello, eliminare il codice di hello evidenziato.

    ![][41]

7. In Esplora soluzioni, espandere cartella Views\Home hello, quindi fare doppio clic su **cshtml** tooopen nell'editor di Visual Studio hello. Sostituire hello l'intero contenuto del file hello con hello seguente codice.

   ```html
   @model IEnumerable<ProductsWeb.Models.Product>

   @{
            ViewBag.Title = "Index";
   }

   <h2>Prod Inventory</h2>

   <table>
             <tr>
                 <th>
                     @Html.DisplayNameFor(model => model.Name)
                 </th>
                 <th></th>
                 <th>
                     @Html.DisplayNameFor(model => model.Quantity)
                 </th>
             </tr>

   @foreach (var item in Model) {
             <tr>
                 <td>
                     @Html.DisplayFor(modelItem => item.Name)
                 </td>
                 <td>
                     @Html.DisplayFor(modelItem => item.Quantity)
                 </td>
             </tr>
   }

   </table>
   ```
8. accuratezza hello tooverify del lavoro svolto finora, è possibile premere **Ctrl + MAIUSC + B** progetto hello toobuild.

### <a name="run-hello-app-locally"></a>Eseguire app hello in locale

Eseguire tooverify applicazione hello del corretto funzionamento.

1. Verificare che **ProductsPortal** progetto attivo hello. Nome del progetto hello in Esplora soluzioni e scegliere **imposta come progetto di avvio**.
2. In Visual Studio premere **F5**.
3. L'applicazione dovrebbe risultare in esecuzione in un browser.

   ![][21]

## <a name="put-hello-pieces-together"></a>Unire parti hello

passaggio successivo Hello è toohook backup hello ai prodotti server locali con hello applicazione ASP.NET.

1. Se non è già aperto, in Visual Studio aprire nuovamente hello **ProductsPortal** progetto creato in hello [creare un'applicazione ASP.NET](#create-an-aspnet-application) sezione.
2. Passaggio toohello simile nella sezione "Creare un Server locale" hello, aggiungere riferimenti al progetto toohello pacchetto NuGet hello. In Esplora soluzioni fare doppio clic su hello **ProductsPortal** del progetto, quindi fare clic su **Gestisci pacchetti NuGet**.
3. Ricerca di "Bus di servizio" e seleziona hello **Windowsazure** elemento. Quindi completare l'installazione di hello e chiudere questa finestra di dialogo.
4. In Esplora soluzioni fare doppio clic su hello **ProductsPortal** del progetto, quindi fare clic su **Aggiungi**, quindi **elemento esistente**.
5. Passare toohello **ProductsContract.cs** file hello **ProductsServer** progetto console. Fare clic su toohighlight ProductsContract.cs. Fare clic su hello freccia giù accanto troppo**Aggiungi**, quindi fare clic su **Aggiungi come collegamento**.

   ![][24]

6. Aprire quindi hello **HomeController.cs** file nell'editor di Visual Studio hello e sostituire definizione dello spazio dei nomi hello con hello seguente codice. Tooreplace assicurarsi di essere *yourServiceNamespace* con nome hello dello spazio dei nomi del servizio, e *yourKey* con la chiave di firma di accesso condiviso. In questo modo hello client toocall hello servizio locale, restituendo hello risultato della chiamata di hello.

   ```csharp
   namespace ProductsWeb.Controllers
   {
       using System.Linq;
       using System.ServiceModel;
       using System.Web.Mvc;
       using Microsoft.ServiceBus;
       using Models;
       using ProductsServer;

       public class HomeController : Controller
       {
           // Declare hello channel factory.
           static ChannelFactory<IProductsChannel> channelFactory;

           static HomeController()
           {
               // Create shared access signature token credentials for authentication.
               channelFactory = new ChannelFactory<IProductsChannel>(new NetTcpRelayBinding(),
                   "sb://yourServiceNamespace.servicebus.windows.net/products");
               channelFactory.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior {
                   TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                       "RootManageSharedAccessKey", "yourKey") });
           }

           public ActionResult Index()
           {
               using (IProductsChannel channel = channelFactory.CreateChannel())
               {
                   // Return a view of hello products inventory.
                   return this.View(from prod in channel.GetProducts()
                                    select
                                        new Product { Id = prod.Id, Name = prod.Name,
                                            Quantity = prod.Quantity });
               }
           }
       }
   }
   ```
7. In Esplora soluzioni fare doppio clic su hello **ProductsPortal** soluzione (assicurarsi che tooright clic hello, non il progetto hello). Scegliere **Aggiungi**, quindi fare clic su **Progetto esistente**.
8. Passare toohello **ProductsServer** del progetto, quindi fare doppio clic su hello **ProductsServer.csproj** tooadd file di soluzione è.
9. **ProductsServer** devono essere eseguite nei dati di hello toodisplay ordine nella **ProductsPortal**. In Esplora soluzioni fare doppio clic su hello **ProductsPortal** soluzione e fare clic su **proprietà**. Hello **pagine delle proprietà** viene visualizzata la finestra di dialogo.
10. Sul lato sinistro di hello, fare clic su **progetto di avvio**. Sul lato destro di hello, fare clic su **più progetti di avvio**. Verificare che **ProductsServer** e **ProductsPortal** viene visualizzato, nell'ordine specificato, con **avviare** impostata come azione hello per entrambi.

      ![][25]

11. Ancora in hello **proprietà** la finestra di dialogo, fare clic su **dipendenze progetto** sul lato sinistro hello.
12. In hello **progetti** elenco, fare clic su **ProductsServer**. Verificare che **ProductsPortal** non sia selezionato.
13. In hello **progetti** elenco, fare clic su **ProductsPortal**. Assicurarsi che **ProductsServer** sia selezionato.

    ![][26]

14. Fare clic su **OK** in hello **pagine delle proprietà** la finestra di dialogo.

## <a name="run-hello-project-locally"></a>Eseguire il progetto hello in locale

l'applicazione hello tootest localmente, in Visual Studio premere **F5**. server locale Hello (**ProductsServer**) deve iniziare prima, quindi hello **ProductsPortal** deve avviare l'applicazione in una finestra del browser. Questa volta, si noterà che l'inventario del prodotto hello Elenca i dati recuperati da hello prodotto del servizio nel sistema locale.

![][10]

Premere **aggiornamento** su hello **ProductsPortal** pagina. Ogni volta che si aggiorna la pagina hello, si noterà hello server app viene visualizzato un messaggio quando `GetProducts()` da **ProductsServer** viene chiamato.

Chiudere entrambe le applicazioni prima del passaggio successivo toohello di procedere.

## <a name="deploy-hello-productsportal-project-tooan-azure-web-app"></a>Distribuire l'applicazione web di Azure di hello ProductsPortal progetto tooan

passaggio successivo Hello è toorepublish hello Azure Web app **ProductsPortal** front-end. Hello seguenti:

1. In Esplora soluzioni fare doppio clic su hello **ProductsPortal** del progetto e fare clic su **pubblica**. Quindi, fare clic su **pubblica** su hello **pubblica** pagina.

  > [!NOTE]
  > Si potrebbe visualizzare un messaggio di errore nella finestra del browser hello quando hello **ProductsPortal** progetto web viene avviato automaticamente dopo la distribuzione di hello. È previsto e si verifica perché hello **ProductsServer** applicazione non è ancora in esecuzione.
>
>

2. Copia URL hello di hello distribuite app web, è necessario hello URL nel passaggio successivo hello. È anche possibile ottenere l'URL dalla finestra attività di servizio App di Azure hello in Visual Studio:

  ![][9]

3. Chiudere hello toostop finestra del browser di hello in esecuzione dell'applicazione.

### <a name="set-productsportal-as-web-app"></a>Impostare ProductsPortal come app Web

Prima di un'applicazione hello in esecuzione nel cloud hello, è necessario assicurarsi che **ProductsPortal** viene avviato dall'interno di Visual Studio come un'app web.

1. In Visual Studio, fare doppio clic su hello **ProductsPortal** del progetto e quindi fare clic su **proprietà**.
2. Nella colonna sinistra hello, fare clic su **Web**.
3. In hello **azione di avvio** fare clic su hello **Avvia URL** pulsante e immettere nella casella di testo hello hello URL per l'app web distribuiti in precedenza; ad esempio, `http://productsportal1234567890.azurewebsites.net/`.

    ![][27]

4. Da hello **File** menu in Visual Studio, fare clic su **Salva tutto**.
5. Dal menu Compila di hello in Visual Studio, fare clic su **Ricompila soluzione**.

## <a name="run-hello-application"></a>Eseguire un'applicazione hello

1. Premere F5 toobuild ed eseguire un'applicazione hello. server locale Hello (hello **ProductsServer** applicazione console) deve iniziare prima, quindi hello **ProductsPortal** deve avviare l'applicazione in una finestra del browser, come illustrato nella seguente schermata hello ripresa. Si noti nuovamente che l'inventario del prodotto hello Elenca i dati recuperati da hello prodotto del servizio nel sistema locale e li visualizza nell'app web hello. Controllare toomake URL hello assicurarsi che **ProductsPortal** è in esecuzione nel cloud di hello, come un'app web di Azure.

   ![][1]

   > [!IMPORTANT]
   > Hello **ProductsServer** applicazione console deve essere in esecuzione e in grado di tooserve hello dati toohello **ProductsPortal** dell'applicazione. Se il browser hello viene visualizzato un errore, attendere alcuni secondi altre per **ProductsServer** tooload e hello di visualizzazione seguenti del messaggio. Premere quindi **aggiornamento** nel browser hello.
   >
   >

   ![][37]
2. Nel browser hello, premere **aggiornamento** su hello **ProductsPortal** pagina. Ogni volta che si aggiorna la pagina hello, si noterà hello server app viene visualizzato un messaggio quando `GetProducts()` da **ProductsServer** viene chiamato.

    ![][38]

## <a name="next-steps"></a>Passaggi successivi

toolearn ulteriori informazioni sull'inoltro di Azure, vedere hello seguenti risorse:  

* [Che cos'è il servizio di inoltro di Azure?](relay-what-is-it.md)  
* [La modalità di inoltro toouse](service-bus-dotnet-how-to-use-relay.md)  

[0]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hybrid.png
[1]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[NuGet]: http://nuget.org

[11]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-con-1.png
[13]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-13.png
[15]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-2.png
[16]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-4.png
[17]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-7.png
[18]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-5.png
[9]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-9.png
[10]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App3.png

[21]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App1.png
[24]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-12.png
[25]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-13.png
[26]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-14.png
[27]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-8.png

[36]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[37]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service1.png
[38]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service2.png
[41]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-40.png
[43]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-hybrid-43.png
