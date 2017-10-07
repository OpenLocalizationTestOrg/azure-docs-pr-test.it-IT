---
title: aaaNotification hub - architettura Push Enterprise
description: Indicazioni sull'uso di Hub di notifica di Azure in un ambiente aziendale
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 903023e9-9347-442a-924b-663af85e05c6
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c3afb83de1ba0882bf99e10f38cca40cb42d07a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-push-architectural-guidance"></a>Guida all'architettura push aziendale
Le aziende sono oggi gradualmente mobile per la creazione di applicazioni per dispositivi mobili per uno propri utenti finali (esterno) o per i dipendenti hello (interni). Hanno i sistemi back-end esistente sul posto sia esso un mainframe o alcune applicazioni LoB a cui devono essere integrati in hello architettura delle applicazioni mobili. Questa Guida verrà presentati come procedure toodo questa integrazione consigliando le soluzioni possibili scenari toocommon.

Un requisito di frequente è per l'invio di push agli utenti di toohello notifica tramite le applicazioni per dispositivi mobili quando si verifica un evento di interesse nei sistemi back-end hello. Ad esempio, un cliente bank con app di servizi bancari hello bank sul proprio iPhone richiede una notifica quando viene effettuato un addebito sopra una certa quantità dal proprio account o una rete Intranet in cui un dipendente dal reparto finanziario che dispone di un'app di approvazione del budget sul suo Windows Phone richiede toobe toobe una notifica quando si riceve una richiesta di approvazione.

conto bancario Hello o l'elaborazione di approvazione è toobe probabilmente eseguito in un sistema back-end che deve avviare un utente toohello push. Potrebbero essere presenti più tali back-end devono compilare tutti i sistemi hello stesso tipo di push tooimplement logica quando un evento è attiva una notifica. complessità Hello qui si trova in diversi sistemi back-end con un sistema di push singolo in cui hello gli utenti finali possono hanno sottoscritto le notifiche toodifferent e possono anche essere più applicazioni per dispositivi mobili, ad esempio nel caso di hello di App per dispositivi mobili intranet di integrazione in un'applicazione per dispositivi mobili può essere notifiche tooreceive da più tali sistemi back-end. i sistemi back-end di Hello non conosce o la necessità di tooknow di push semantica/tecnologia qui una soluzione comune tradizionalmente toointroduce un componente che esegue il polling dei sistemi back-end hello per tutti gli eventi di interesse e responsabile per l'invio di messaggi push hello toohello client.
Di seguito verranno descritti in una soluzione migliore utilizzando Azure Service Bus - modello di argomento o una sottoscrizione che consentiranno di ridurre la complessità di hello durante la creazione di soluzioni hello scalabile.

Ecco architettura generale di hello della soluzione hello (generalizzata con più App per dispositivi mobili ma ugualmente applicabili quando è presente solo un'app per dispositivi mobili)

## <a name="architecture"></a>Architettura
![][1]

informazione di chiave Hello in questo diagramma dell'architettura è Bus di servizio di Azure che fornisce un modello di programmazione argomenti/sottoscrizioni (più su di esso in [programmazione di Service Bus Pub/Sub]). il ricevitore Hello, che in questo caso, è back-end Mobile hello (in genere [servizio Mobile di Azure], che verrà avviata un'App per dispositivi mobili toohello push) non ricevono messaggi direttamente da sistemi back-end hello ma invece non è disponibile un livello di astrazione intermedio fornito da [Azure Service Bus] che consente di back-end mobile tooreceive messaggi da uno o più sistemi back-end. Un argomento del Bus di servizio deve toobe creato per ogni hello sistemi back-end, ad esempio Account, h, Finance che sono fondamentalmente "argomenti" di interesse che avvierà toobe i messaggi inviati come notifica push. i sistemi back-end Hello invierà messaggi argomenti toothese. Un back-end Mobile possibile sottoscrivere tooone o più di tali argomenti tramite la creazione di una sottoscrizione del Bus di servizio. Questo darà hello back-end mobile tooreceive una notifica dal sistema back-end corrispondente hello. Back-end mobile continua toolisten per i messaggi nelle sottoscrizioni e non appena arriva un messaggio, si trasforma e Invia come hub di notifica tooits di notifica. Gli hub di notifica infine recapita app per dispositivi mobili toohello messaggio hello. Componenti chiave hello toosummarize, sono presenti:

1. Sistema back-end (sistemi LoB/legacy)
   * Crea un argomento del bus di servizio
   * Invia un messaggio
2. Back-end Mobile
   * Crea una sottoscrizione al servizio
   * Riceve un messaggio (dal sistema back-end)
   * Invia notifica tooclients (tramite Hub di notifica di Azure)
3. Applicazione per dispositivi mobili
   * Riceve e visualizza la notifica

### <a name="benefits"></a>Vantaggi:
1. Hello separazione tra mittente (sistemi back-end) e al destinatario di hello (app/servizio mobile tramite Hub di notifica) consente ai sistemi back-end aggiuntivi viene integrati con modifiche minime.
2. In questo modo anche scenario hello di più App per dispositivi mobili da tooreceive in grado di eventi da uno o più sistemi back-end.  

## <a name="sample"></a>Esempio:
### <a name="prerequisites"></a>Prerequisiti
È consigliabile completare hello seguenti esercitazioni toofamiliarize con i concetti di hello, nonché operazioni di creazione e configurazione più comuni:

1. [programmazione di Service Bus Pub/Sub] -dettagli hello di utilizzo con Service Bus argomenti/sottoscrizioni, illustra come toocreate uno spazio dei nomi toocontain argomenti/sottoscrizioni, come toosend & ricevere messaggi da essi.
2. [Gli hub di notifica - esercitazione universali di Windows] -questo spiega come tooset fino a un'applicazione Windows Store e usare tooregister gli hub di notifica e quindi ricevere le notifiche.

### <a name="sample-code"></a>Codice di esempio
il codice di esempio completo di Hello è disponibile all'indirizzo [degli esempi di Hub di notifica]. Il codice è suddiviso in tre componenti:

1. **EnterprisePushBackendSystem**
   
    a. Questo progetto usa hello *Windowsazure* pacchetto Nuget e si basa su [programmazione di Service Bus Pub/Sub].
   
    b. Si tratta di un semplice in c# console app toosimulate un sistema LoB che avvia toobe messaggio hello recapitati toohello app per dispositivi mobili.
   
        static void Main(string[] args)
        {
            string connectionString =
                CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello topic where we will send notifications
            CreateTopic(connectionString);
   
            // Send message
            SendMessage(connectionString);
        }
   
    c. `CreateTopic`è argomento del Bus di servizio utilizzato toocreate hello in cui Microsoft invierà i messaggi.
   
        public static void CreateTopic(string connectionString)
        {
            // Create hello topic if it does not exist already
   
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.TopicExists(sampleTopic))
            {
                namespaceManager.CreateTopic(sampleTopic);
            }
        }
   
    d. `SendMessage`viene utilizzato toosend hello messaggi toothis argomento del Bus di servizio. Qui stiamo semplicemente inviando un set di argomento toohello messaggi casuale periodicamente a scopo di hello dell'esempio hello. Nella realtà, sarebbe presente un sistema back-end che invia i messaggi quando si verifica un evento.
   
        public static void SendMessage(string connectionString)
        {
            TopicClient client =
                TopicClient.CreateFromConnectionString(connectionString, sampleTopic);
   
            // Sends random messages every 10 seconds toohello topic
            string[] messages =
            {
                "Employee Id '{0}' has joined.",
                "Employee Id '{0}' has left.",
                "Employee Id '{0}' has switched tooa different team."
            };
   
            while (true)
            {
                Random rnd = new Random();
                string employeeId = rnd.Next(10000, 99999).ToString();
                string notification = String.Format(messages[rnd.Next(0,messages.Length)], employeeId);
   
                // Send Notification
                BrokeredMessage message = new BrokeredMessage(notification);
                client.Send(message);
   
                Console.WriteLine("{0} Message sent - '{1}'", DateTime.Now, notification);
   
                System.Threading.Thread.Sleep(new TimeSpan(0, 0, 10));
            }
        }
2. **ReceiveAndSendNotification**
   
    a. Questo progetto usa hello *Windowsazure* e *Microsoft.Web.WebJobs.Publish* Nuget pacchetti e si basa sul [programmazione di Service Bus Pub/Sub].
   
    b. Si tratta di un'altra console app c# che verranno eseguiti come un [processo Web di Azure] perché ha toorun continuamente toolisten per i messaggi generati dal hello LoB/sistemi back-end. L'app sarà parte del back-end Mobile.
   
        static void Main(string[] args)
        {
            string connectionString =
                     CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello subscription which will receive messages
            CreateSubscription(connectionString);
   
            // Receive message
            ReceiveMessageAndSendNotification(connectionString);
        }
   
    c. `CreateSubscription`è utilizzato toocreate una sottoscrizione del Bus di servizio per l'argomento hello in cui il sistema di back-end hello verrà inviati i messaggi. A seconda dello scenario di business hello, questo componente creerà una o più sottoscrizioni toocorresponding argomenti (ad esempio, alcuni può ricevere messaggi dal sistema delle risorse Umane, alcune da sistema Finance e così via)
   
        static void CreateSubscription(string connectionString)
        {
            // Create hello subscription if it does not exist already
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.SubscriptionExists(sampleTopic, sampleSubscription))
            {
                namespaceManager.CreateSubscription(sampleTopic, sampleSubscription);
            }
        }
   
    d. ReceiveMessageAndSendNotification è il messaggio hello tooread utilizzato da un argomento di hello utilizzando la relativa sottoscrizione e se ha esito positivo hello leggere quindi creare un toohello toobe inviate notifiche (nello scenario di esempio hello una notifica di tipo avviso popup nativo di Windows) per dispositivi mobili applicazione che utilizza gli hub di notifica di Azure.
   
        static void ReceiveMessageAndSendNotification(string connectionString)
        {
            // Initialize hello Notification Hub
            string hubConnectionString = CloudConfigurationManager.GetSetting
                    ("Microsoft.NotificationHub.ConnectionString");
            hub = NotificationHubClient.CreateClientFromConnectionString
                    (hubConnectionString, "enterprisepushservicehub");
   
            SubscriptionClient Client =
                SubscriptionClient.CreateFromConnectionString
                        (connectionString, sampleTopic, sampleSubscription);
   
            Client.Receive();
   
            // Continuously process messages received from hello subscription
            while (true)
            {
                BrokeredMessage message = Client.Receive();
                var toastMessage = @"<toast><visual><binding template=""ToastText01""><text id=""1"">{messagepayload}</text></binding></visual></toast>";
   
                if (message != null)
                {
                    try
                    {
                        Console.WriteLine(message.MessageId);
                        Console.WriteLine(message.SequenceNumber);
                        string messageBody = message.GetBody<string>();
                        Console.WriteLine("Body: " + messageBody + "\n");
   
                        toastMessage = toastMessage.Replace("{messagepayload}", messageBody);
                        SendNotificationAsync(toastMessage);
   
                        // Remove message from subscription
                        message.Complete();
                    }
                    catch (Exception)
                    {
                        // Indicate a problem, unlock message in subscription
                        message.Abandon();
                    }
                }
            }
        }
        static async void SendNotificationAsync(string message)
        {
            await hub.SendWindowsNativeNotificationAsync(message);
        }
   
    e. Per la pubblicazione come un **processo Web**, fare clic con il pulsante destro sulla soluzione hello in Visual Studio e selezionare **pubblica come processo Web**
   
    ![][2]
   
    f. Selezionare il profilo di pubblicazione e creare un nuovo sito Web di Azure, se non esiste già che ospiterà il processo Web e dopo aver sito Web di hello quindi **pubblica**.
   
    ![][3]
   
    g. Configurare hello "Eseguire continuamente" toobe di processo in modo che quando si accede toohello [portale di Azure classico] dovrebbe essere simile alla seguente hello:
   
    ![][4]
3. **EnterprisePushMobileApp**
   
    a. Si tratta di un'applicazione Windows Store che riceverà le notifiche di tipo avviso popup dall'esecuzione di processi Web hello come parte di back-end per dispositivi mobili e visualizzarli. Si basa su quanto riportato in [Gli hub di notifica - esercitazione universali di Windows].  
   
    b. Verificare che l'applicazione notifiche di tipo avviso popup tooreceive abilitato.
   
    c. Verificare che hello dopo il codice di registrazione di hub di notifica viene chiamato all'avvio dell'applicazione hello (dopo la sostituzione di hello *HubName* e *DefaultListenSharedAccessSignature*:
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("[HubName]", "[DefaultListenSharedAccessSignature]");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

### <a name="running-sample"></a>Esecuzione di esempio:
1. Verificare che il processo Web venga eseguita correttamente e pianificata troppo "esecuzione continua".
2. Eseguire hello **EnterprisePushMobileApp** che verrà avviata l'app di Windows Store hello.
3. Eseguire hello **EnterprisePushBackendSystem** applicazione console che consente di simulare back-end LoB hello e inizierà a inviare messaggi ed è necessario verificare le notifiche di tipo avviso popup visualizzato hello seguente:
   
    ![][5]
4. messaggi hello inviati originariamente tooService argomenti del Bus di cui è stato monitorato per le sottoscrizioni del Bus di servizio nel processo Web. Una volta ricevuto un messaggio, una notifica creata e inviata toohello app per dispositivi mobili. È possibile esaminare hello processo Web registra tooconfirm hello elaborazione quando si passa toohello collegano log [portale di Azure classico] per il processo Web:
   
    ![][6]

<!-- Images -->
[1]: ./media/notification-hubs-enterprise-push-architecture/architecture.png
[2]: ./media/notification-hubs-enterprise-push-architecture/WebJobsContextMenu.png
[3]: ./media/notification-hubs-enterprise-push-architecture/PublishAsWebJob.png
[4]: ./media/notification-hubs-enterprise-push-architecture/WebJob.png
[5]: ./media/notification-hubs-enterprise-push-architecture/Notifications.png
[6]: ./media/notification-hubs-enterprise-push-architecture/WebJobsLog.png

<!-- Links -->
[degli esempi di Hub di notifica]: https://github.com/Azure/azure-notificationhubs-samples
[servizio Mobile di Azure]: http://azure.microsoft.com/documentation/services/mobile-services/
[Azure Service Bus]: http://azure.microsoft.com/documentation/articles/fundamentals-service-bus-hybrid-solutions/
[programmazione di Service Bus Pub/Sub]: http://azure.microsoft.com/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/
[processo Web di Azure]: http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/
[Gli hub di notifica - esercitazione universali di Windows]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/
[portale di Azure classico]: https://manage.windowsazure.com/
