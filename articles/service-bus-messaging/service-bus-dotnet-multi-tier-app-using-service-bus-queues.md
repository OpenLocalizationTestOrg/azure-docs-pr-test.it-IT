---
title: applicazione multilivello aaa.NET utilizzando Azure Service Bus | Documenti Microsoft
description: "Un'esercitazione .NET che consente di sviluppare un'applicazione a più livelli in Azure che utilizza toocommunicate code Service Bus tra livelli."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1b8608ca-aa5a-4700-b400-54d65b02615c
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 04/11/2017
ms.author: sethm
ms.openlocfilehash: 485910ff1d3b8b0a709ee14ede32e57cf873829a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="net-multi-tier-application-using-azure-service-bus-queues"></a>Applicazione .NET multilivello che usa code del bus di servizio
## <a name="introduction"></a>Introduzione
Sviluppo per Microsoft Azure è semplice con Visual Studio e hello gratuito di Azure SDK per .NET. In questa esercitazione illustra hello passaggi toocreate un'applicazione che utilizza più risorse di Azure in esecuzione nell'ambiente locale.

Si apprenderà seguente hello:

* Come tooenable del computer per lo sviluppo di Azure con un singolo scaricare e installare.
* Come toouse toodevelop di Visual Studio per Azure.
* Come toocreate un'applicazione a più livelli in Azure usando i ruoli web e di lavoro.
* Come toocommunicate tra livelli mediante le code del Bus di servizio.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

In questa esercitazione si sarà compilare ed eseguire un'applicazione multilivello hello in un servizio cloud di Azure. front-end Hello è un ruolo web ASP.NET MVC e back-end hello è un ruolo di lavoro che utilizza una coda del Bus di servizio. È possibile creare hello stesso multilivello con front-end hello come progetto di applicazione web, che viene distribuito tooan sito Web di Azure invece di un servizio cloud. È anche possibile provare hello [un'applicazione in locale/cloud ibrida .NET](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) esercitazione.

Hello cattura di schermata seguente mostra un'applicazione hello completata.

![][0]

## <a name="scenario-overview-inter-role-communication"></a>Informazioni generali sullo scenario: comunicazione tra ruoli
toosubmit un ordine per l'elaborazione, componente dell'interfaccia utente front-end hello, in esecuzione nel ruolo web hello devono interagire con la logica di livello intermedio hello in esecuzione nel ruolo di lavoro hello. In questo esempio utilizza la messaggistica di Service Bus per la comunicazione tra i livelli di hello hello.

Uso del Bus di servizio Messaggistica tra i livelli intermedi e web hello separa i due componenti. Al contrario di hello toodirect messaggistica (ovvero, TCP o HTTP), livello web non si connette intermedio toohello direttamente. invece inserisce le unità di lavoro, come i messaggi nel Bus di servizio, che li mantiene fino al livello intermedio hello tooconsume pronto in modo affidabile ed elaborarle.

Bus di servizio offre due entità toosupport negoziata messaggistica: code e argomenti. Con le code, ogni messaggio inviato toohello coda viene utilizzata da un singolo ricevitore. Gli argomenti supportano modello hello pubblicazione/sottoscrizione in cui ogni messaggio pubblicato viene reso disponibile tooa sottoscrizione registrata con argomento hello. Ogni sottoscrizione mantiene in modo logico la propria coda di messaggi. Le sottoscrizioni possono essere configurate anche con regole dei filtri che limitano il set di hello di messaggi passati a hello sottoscrizione coda toothose che corrispondono al filtro hello. Hello esempio seguente usa le code del Bus di servizio.

![][1]

Questo meccanismo di comunicazione presenta alcuni vantaggi rispetto alla messaggistica diretta:

* **Disaccoppiamento temporaneo.** Con modello di messaggistica asincrona di hello, producer e consumer non è necessario online all'indirizzo hello contemporaneamente. Bus di servizio archivia in modo affidabile i messaggi hello finché consumer non è pronto a riceverli. In questo modo i componenti di hello di toobe applicazione hello distribuita disconnesso, sia volontariamente, ad esempio, per la manutenzione o a causa di arresto anomalo del componente tooa, senza alcun impatto sul sistema nel suo complesso. Inoltre, hello utilizzano l'applicazione potrebbe essere necessario solo toocome online durante determinate ore del giorno hello.
* **Livellamento del carico.** In molte applicazioni, il carico del sistema varia nel tempo, mentre il tempo di elaborazione di hello necessario per ogni unità di lavoro è in genere costante. Interposizione messaggio producer e consumer una coda significa che hello utilizzo applicazione (worker hello) solo esigenze toobe provisioning tooaccommodate di carico medio invece di un carico di picco. profondità Hello della coda di hello aumentano e i contratti in base alla variazione carico in ingresso hello. In questo modo direttamente money in termini di quantità hello infrastruttura richiesto tooservice hello carico dell'applicazione.
* **Bilanciamento del carico.** Come aumentare del carico, altri processi di lavoro è possibile aggiungere tooread dalla coda hello. Ogni messaggio viene elaborato da un solo hello di processi di lavoro. Inoltre, il bilanciamento del carico basato su pull consente l'utilizzo ottimale delle macchine lavoro hello anche se le macchine di lavoro si differenziano in termini di potenza di elaborazione, come verrà estraggono i messaggi alla propria velocità massima. Questo modello viene spesso definito hello *consumer concorrente* modello.
  
  ![][2]

Hello le sezioni seguenti viene illustrato il codice hello che implementa questa architettura.

## <a name="set-up-hello-development-environment"></a>Configurare un ambiente di sviluppo hello
Prima di iniziare lo sviluppo di applicazioni Azure, Scarica gli strumenti di hello e configurare l'ambiente di sviluppo.

1. Installare hello Azure SDK per .NET da hello SDK [pagina di download](https://azure.microsoft.com/downloads/).
2. In hello **.NET** colonna, fare clic sulla versione di hello di [Visual Studio](http://www.visualstudio.com) in uso. Hello i passaggi in questa esercitazione usare Visual Studio 2015, ma funzionano anche con Visual Studio 2017.
3. Quando viene chiesto di toorun o salvare installer hello, fare clic su **eseguire**.
4. In hello **installazione guidata piattaforma Web**, fare clic su **installare** e continuare l'installazione di hello.
5. Al termine dell'installazione di hello, sarà necessario tutto il necessario toostart toodevelop hello app. Hello SDK include strumenti che consentono di sviluppare facilmente applicazioni Azure in Visual Studio.

## <a name="create-a-namespace"></a>Creare uno spazio dei nomi
passaggio successivo Hello è toocreate uno spazio dei nomi di servizio e ottenere una chiave di firma di accesso condiviso (SAS). Uno spazio dei nomi fornisce un limite per ogni applicazione esposta tramite il bus di servizio. Una chiave di firma di accesso condiviso viene generata dal sistema hello quando viene creato uno spazio dei nomi. combinazione di Hello di spazio dei nomi e la chiave di firma di accesso condiviso fornisce le credenziali di hello per applicazione tooan accesso tooauthenticate di Bus di servizio.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-web-role"></a>Creare un ruolo web
In questa sezione, si compila front-end di hello dell'applicazione. Creare innanzitutto le pagine di hello visualizzato dall'applicazione.
Successivamente, aggiungere il codice che invia gli elementi della coda del Bus di servizio tooa e visualizza le informazioni di stato coda hello.

### <a name="create-hello-project"></a>Creare il progetto hello
1. Con privilegi di amministratore, avviare Visual Studio: hello rapida **Visual Studio** sull'icona di programma e quindi fare clic su **Esegui come amministratore**. emulatore di calcolo di Azure Hello, descritto più avanti in questo articolo, è necessario che è possibile avviare Visual Studio con privilegi di amministratore.
   
   In Visual Studio, su hello **File** menu, fare clic su **New**, quindi fare clic su **progetto**.
2. Da **Modelli installati** in **Visual C#** fare clic su **Cloud** e quindi su **Servizio cloud di Azure**. Progetto hello nome **MultiTierApp**. Fare quindi clic su **OK**.
   
   ![][9]
3. Dai ruoli **.NET Framework 4.5** fare doppio clic su **Ruolo Web ASP.NET**.
   
   ![][10]
4. Passare il mouse su **WebRole1** in **soluzione servizio Cloud di Azure**, fare clic sull'icona di matita hello e rinominare il ruolo di web hello troppo**FrontendWebRole**. Fare quindi clic su **OK**. Assicurarsi di immettere "Frontend" con una 'e' minuscola, non "FrontEnd".
   
   ![][11]
5. Da hello **nuovo progetto ASP.NET** della finestra di dialogo hello **selezionare un modello** elenco, fare clic su **MVC**.
   
   ![][12]
6. Ancora in hello **nuovo progetto ASP.NET** finestra di dialogo fare clic su hello **Modifica autenticazione** pulsante. In hello **Modifica autenticazione** la finestra di dialogo, fare clic su **Nessuna autenticazione**, quindi fare clic su **OK**. Per questa esercitazione si distribuisce un'applicazione che non richiede l'accesso utente.
   
    ![][16]
7. In hello **nuovo progetto ASP.NET** la finestra di dialogo, fare clic su **OK** progetto hello toocreate.
8. In **Esplora**, in hello **FrontendWebRole** del progetto, fare doppio clic su **riferimenti**, quindi fare clic su **Gestisci pacchetti NuGet**.
9. Fare clic su hello **Sfoglia** tab, quindi cercare `Microsoft Azure Service Bus`. Seleziona hello **Windowsazure** del pacchetto, fare clic su **installare**e accettare le condizioni di hello d'uso.
   
   ![][13]
   
   Si noti che hello e obbligatori per l'assembly client fa riferimento a questo punto sono stati aggiunti alcuni nuovi file di codice.
10. In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Modelli**, quindi scegliere **Aggiungi** e infine **Classe**. In hello **nome** casella, il nome del tipo hello **Onlineorder**. Fare quindi clic su **Aggiungi**.

### <a name="write-hello-code-for-your-web-role"></a>Scrittura di codice hello per il ruolo web
In questa sezione è creare hello varie pagine visualizzato dall'applicazione.

1. Nel file di Onlineorder hello in Visual Studio, sostituire la definizione dello spazio dei nomi esistente con hello seguente codice:
   
   ```csharp
   namespace FrontendWebRole.Models
   {
       public class OnlineOrder
       {
           public string Customer { get; set; }
           public string Product { get; set; }
       }
   }
   ```
2. In **Esplora soluzioni** fare doppio clic su **Controllers\HomeController.cs**. Aggiungere il seguente hello **utilizzando** istruzioni nella parte superiore di hello di hello file tooinclude hello gli spazi dei nomi per il modello appena creato, nonché il Bus di servizio.
   
   ```csharp
   using FrontendWebRole.Models;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   ```
3. Anche nel file di hello HomeController. cs in Visual Studio, sostituire la definizione dello spazio dei nomi esistente con hello seguente codice. Questo codice contiene metodi per la gestione di presentazione hello della coda toohello degli elementi.
   
   ```csharp
   namespace FrontendWebRole.Controllers
   {
       public class HomeController : Controller
       {
           public ActionResult Index()
           {
               // Simply redirect tooSubmit, since Submit will serve as the
               // front page of this application.
               return RedirectToAction("Submit");
           }
   
           public ActionResult About()
           {
               return View();
           }
   
           // GET: /Home/Submit.
           // Controller method for a view you will create for hello submission
           // form.
           public ActionResult Submit()
           {
               // Will put code for displaying queue message count here.
   
               return View();
           }
   
           // POST: /Home/Submit.
           // Controller method for handling submissions from hello submission
           // form.
           [HttpPost]
           // Attribute toohelp prevent cross-site scripting attacks and
           // cross-site request forgery.  
           [ValidateAntiForgeryToken]
           public ActionResult Submit(OnlineOrder order)
           {
               if (ModelState.IsValid)
               {
                   // Will put code for submitting tooqueue here.
   
                   return RedirectToAction("Submit");
               }
               else
               {
                   return View(order);
               }
           }
       }
   }
   ```
4. Da hello **compilare** menu, fare clic su **Compila soluzione** accuratezza hello tootest del lavoro svolto finora.
5. A questo punto, creare vista hello per hello `Submit()` metodo creato in precedenza. Fare doppio clic all'interno di hello `Submit()` metodo (overload hello del `Submit()` che non accetta parametri), quindi scegliere **Aggiungi visualizzazione**.
   
   ![][14]
6. Una finestra di dialogo viene visualizzata per la creazione di visualizzazione hello. In hello **modello** scegliere **crea**. In hello **classe modello** elenco, fare clic su hello **OnlineOrder** classe.
   
   ![][15]
7. Fare clic su **Aggiungi**.
8. A questo punto, modificare il nome di hello visualizzato dell'applicazione. In **Esplora**, fare doppio clic su di **Views\Shared\\layout. cshtml** tooopen del file nell'editor di Visual Studio hello.
9. Sostituire tutte le occorrenze di **My ASP.NET Application** con **LITWARE'S Products**.
10. Rimuovere hello **Home**, **su**, e **contatto** collegamenti. Eliminare il codice evidenziato hello:
    
    ![][28]
11. Infine, modificare hello invio pagina tooinclude alcune informazioni sulla coda hello. In **Esplora**, fare doppio clic su di **Views\Home\Submit.cshtml** tooopen del file nell'editor di Visual Studio hello. Aggiungere hello successiva riga dopo `<h2>Submit</h2>`. Per il momento, hello `ViewBag.MessageCount` è vuoto. Il valore verrà inserito successivamente.
    
    ```html
    <p>Current number of orders in queue waiting toobe processed: @ViewBag.MessageCount</p>
    ```
12. L'interfaccia utente è stata implementata. È possibile premere **F5** toorun l'applicazione e verificare che l'aspetto di come previsto.
    
    ![][17]

### <a name="write-hello-code-for-submitting-items-tooa-service-bus-queue"></a>Scrittura di codice hello per l'invio di elementi della coda del Bus di servizio tooa
A questo punto, aggiungere codice per l'invio a coda tooa degli elementi. Creare prima di tutto una classe contenente le informazioni di connessione della coda del bus di servizio. Inizializzare quindi la connessione da Global.aspx.cs. Infine, aggiornare il codice di invio hello creato in precedenza nella coda di Service Bus tooa HomeController.cs tooactually invia gli elementi.

1. In **Esplora**, fare doppio clic su **FrontendWebRole** (progetto hello pulsante destro del mouse, non il ruolo hello). Fare clic su **Aggiungi**, quindi su **Classe**.
2. Nome classe hello **QueueConnector.cs**. Fare clic su **Aggiungi** classe hello toocreate.
3. A questo punto, aggiungere il codice che incapsula le informazioni di connessione hello e inizializza coda di Service Bus tooa connessione hello. Sostituire hello l'intero contenuto di QueueConnector.cs con hello seguente di codice e immettere i valori per `your Service Bus namespace` (il nome dello spazio dei nomi) e `yourKey`, ovvero hello **chiave primaria** ottenuto in precedenza da hello Azure portale.
   
   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Web;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   
   namespace FrontendWebRole
   {
       public static class QueueConnector
       {
           // Thread-safe. Recommended that you cache rather than recreating it
           // on every request.
           public static QueueClient OrdersQueueClient;
   
           // Obtain these values from hello portal.
           public const string Namespace = "your Service Bus namespace";
   
           // hello name of your queue.
           public const string QueueName = "OrdersQueue";
   
           public static NamespaceManager CreateNamespaceManager()
           {
               // Create hello namespace manager which gives you access to
               // management operations.
               var uri = ServiceBusEnvironment.CreateServiceUri(
                   "sb", Namespace, String.Empty);
               var tP = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                   "RootManageSharedAccessKey", "yourKey");
               return new NamespaceManager(uri, tP);
           }
   
           public static void Initialize()
           {
               // Using Http toobe friendly with outbound firewalls.
               ServiceBusEnvironment.SystemConnectivity.Mode =
                   ConnectivityMode.Http;
   
               // Create hello namespace manager which gives you access to
               // management operations.
               var namespaceManager = CreateNamespaceManager();
   
               // Create hello queue if it does not exist already.
               if (!namespaceManager.QueueExists(QueueName))
               {
                   namespaceManager.CreateQueue(QueueName);
               }
   
               // Get a client toohello queue.
               var messagingFactory = MessagingFactory.Create(
                   namespaceManager.Address,
                   namespaceManager.Settings.TokenProvider);
               OrdersQueueClient = messagingFactory.CreateQueueClient(
                   "OrdersQueue");
           }
       }
   }
   ```
4. Assicurarsi che venga chiamato il metodo **Initialize**. In **Esplora soluzioni** fare doppio clic su **Global.asax\Global.asax.cs**.
5. Aggiungere hello successiva riga di codice alla fine hello hello **Application_Start** metodo.
   
   ```csharp
   FrontendWebRole.QueueConnector.Initialize();
   ```
6. Infine, aggiornare il codice di web hello creato in precedenza, per inviare gli elementi toohello coda. In **Esplora soluzioni** fare doppio clic su **Controllers\HomeController.cs**.
7. Hello aggiornamento `Submit()` metodo (overload hello che non accetta parametri) come indicato di seguito tooget hello numero messaggi per coda hello.
   
   ```csharp
   public ActionResult Submit()
   {
       // Get a NamespaceManager which allows you tooperform management and
       // diagnostic operations on your Service Bus queues.
       var namespaceManager = QueueConnector.CreateNamespaceManager();
   
       // Get hello queue, and obtain hello message count.
       var queue = namespaceManager.GetQueue(QueueConnector.QueueName);
       ViewBag.MessageCount = queue.MessageCount;
   
       return View();
   }
   ```
8. Hello aggiornamento `Submit(OnlineOrder order)` metodo (hello dell'overload che accetta un parametro) come indicato di seguito toosubmit ordine coda toohello informazioni.
   
   ```csharp
   public ActionResult Submit(OnlineOrder order)
   {
       if (ModelState.IsValid)
       {
           // Create a message from hello order.
           var message = new BrokeredMessage(order);
   
           // Submit hello order.
           QueueConnector.OrdersQueueClient.Send(message);
           return RedirectToAction("Submit");
       }
       else
       {
           return View(order);
       }
   }
   ```
9. È ora possibile eseguire nuovamente l'applicazione hello. Ogni volta che si invia un ordine, aumenta il numero di messaggi hello.
   
   ![][18]

## <a name="create-hello-worker-role"></a>Creare il ruolo di lavoro hello
Si creerà ora ruolo di lavoro hello che elabora gli invii di ordine di hello. Questo esempio viene utilizzato hello **ruolo di lavoro con coda di Service Bus** il modello di progetto di Visual Studio. Le credenziali necessarie hello già ottenuto dal portale hello.

1. Verificare che si è connessi a Visual Studio tooyour account Azure.
2. In Visual Studio, in **Esplora** destro la **ruoli** cartella hello **MultiTierApp** progetto.
3. Fare clic su **Aggiungi**, quindi su **Nuovo progetto di ruolo di lavoro**. Hello **Aggiungi nuovo progetto di ruolo** viene visualizzata la finestra di dialogo.
   
   ![][26]
4. In hello **Aggiungi nuovo progetto di ruolo** la finestra di dialogo, fare clic su **ruolo di lavoro con coda di Service Bus**.
   
   ![][23]
5. In hello **nome** casella, il progetto di hello nome **OrderProcessingRole**. Fare quindi clic su **Aggiungi**.
6. Copiare una stringa di connessione hello ottenuto nel passaggio 9 di blocco per Appunti toohello sezione "Creare uno spazio dei nomi del Bus di servizio" hello.
7. In **Esplora**, hello rapida **OrderProcessingRole** creato nel passaggio 5 (assicurarsi che si fa clic su **OrderProcessingRole** in **Ruoli**, e non hello classe). Fare quindi clic su **Proprietà**.
8. In hello **impostazioni** scheda di hello **proprietà** la finestra di dialogo, fare clic all'interno di hello **valore** casella **Microsoft.ServiceBus.ConnectionString**, quindi incollare il valore di endpoint hello copiato nel passaggio 6.
   
   ![][25]
9. Creare un **OnlineOrder** classe toorepresent hello ordini elaborati dalla coda hello. È possibile riutilizzare una classe creata in precedenza. In **Esplora**, hello rapida **OrderProcessingRole** classe (icona del pulsante destro del mouse hello classe, non il ruolo hello). Fare clic su **Aggiungi**, quindi su **Elemento esistente**.
10. Individuare la sottocartella toohello per **FrontendWebRole\Models**e quindi fare doppio clic su **Onlineorder** tooadd è toothis progetto.
11. In **WorkerRole.cs**, modificare il valore di hello di hello **QueueName** variabile `"ProcessingQueue"` troppo`"OrdersQueue"` come illustrato nel seguente codice hello.
    
    ```csharp
    // hello name of your queue.
    const string QueueName = "OrdersQueue";
    ```
12. Aggiungere hello seguente istruzione using nella parte superiore di hello del file WorkerRole.cs hello.
    
    ```csharp
    using FrontendWebRole.Models;
    ```
13. In hello `Run()` funzione, all'interno di hello `OnMessage()` chiamare, sostituire il contenuto di hello di hello `try` clausola con hello seguente codice.
    
    ```csharp
    Trace.WriteLine("Processing", receivedMessage.SequenceNumber.ToString());
    // View hello message as an OnlineOrder.
    OnlineOrder order = receivedMessage.GetBody<OnlineOrder>();
    Trace.WriteLine(order.Customer + ": " + order.Product, "ProcessingMessage");
    receivedMessage.Complete();
    ```
14. È stata completata l'applicazione hello. È possibile testare un'applicazione hello completo facendo clic con il progetto MultiTierApp hello in Esplora soluzioni selezionare **imposta come progetto di avvio**e quindi premendo F5. Si noti che il numero di messaggi non aumenta perché il ruolo di lavoro hello elabora gli elementi dalla coda hello e li contrassegna come completata. È possibile visualizzare l'output di traccia hello del ruolo di lavoro visualizzando hello interfaccia utente emulatore di calcolo di Azure. È possibile farlo facendo clic sull'icona di emulatore hello nell'area di notifica hello della barra delle applicazioni e selezionando **Mostra interfaccia utente di emulatore di calcolo**.
    
    ![][19]
    
    ![][20]

## <a name="next-steps"></a>Passaggi successivi
toolearn ulteriori informazioni su Service Bus, vedere hello seguenti risorse:  

* [Documentazione sul bus di servizio di Azure][sbdocs]  
* [Pagina del servizio Bus di servizio][sbacom]  
* [Come tooUse code di Service Bus][sbacomqhowto]  

toolearn ulteriori informazioni su scenari a più livelli, vedere:  

* [Applicazione .NET multilivello con tabelle, code e BLOB di archiviazione di Azure][mutitierstorage]  

[0]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[1]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-100.png
[2]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-101.png
[9]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-10.png
[10]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-11.png
[11]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-02.png
[12]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-12.png
[13]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-13.png
[14]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-33.png
[15]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-34.png
[16]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-14.png
[17]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[18]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app2.png

[19]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-38.png
[20]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-39.png
[23]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRole1.png
[25]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRoleProperties.png
[26]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBNewWorkerRole.png
[28]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-40.png

[sbdocs]: /azure/service-bus-messaging/  
[sbacom]: https://azure.microsoft.com/services/service-bus/  
[sbacomqhowto]: service-bus-dotnet-get-started-with-queues.md  
[mutitierstorage]: https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36
