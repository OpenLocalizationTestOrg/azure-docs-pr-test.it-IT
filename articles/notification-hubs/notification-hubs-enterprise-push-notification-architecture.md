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
# <a name="enterprise-push-architectural-guidance"></a><span data-ttu-id="f46a2-103">Guida all'architettura push aziendale</span><span class="sxs-lookup"><span data-stu-id="f46a2-103">Enterprise push architectural guidance</span></span>
<span data-ttu-id="f46a2-104">Le aziende sono oggi gradualmente mobile per la creazione di applicazioni per dispositivi mobili per uno propri utenti finali (esterno) o per i dipendenti hello (interni).</span><span class="sxs-lookup"><span data-stu-id="f46a2-104">Enterprises today are gradually moving towards creating mobile applications for either their end users (external) or for hello employees (internal).</span></span> <span data-ttu-id="f46a2-105">Hanno i sistemi back-end esistente sul posto sia esso un mainframe o alcune applicazioni LoB a cui devono essere integrati in hello architettura delle applicazioni mobili.</span><span class="sxs-lookup"><span data-stu-id="f46a2-105">They have existing backend systems in place be it mainframes or some LoB applications which must be integrated into hello mobile application architecture.</span></span> <span data-ttu-id="f46a2-106">Questa Guida verrà presentati come procedure toodo questa integrazione consigliando le soluzioni possibili scenari toocommon.</span><span class="sxs-lookup"><span data-stu-id="f46a2-106">This guide will talk about how best toodo this integration recommending possible solution toocommon scenarios.</span></span>

<span data-ttu-id="f46a2-107">Un requisito di frequente è per l'invio di push agli utenti di toohello notifica tramite le applicazioni per dispositivi mobili quando si verifica un evento di interesse nei sistemi back-end hello.</span><span class="sxs-lookup"><span data-stu-id="f46a2-107">A frequent requirement is for sending push notification toohello users through their mobile application when an event of interest occurs in hello backend systems.</span></span> <span data-ttu-id="f46a2-108">Ad esempio,</span><span class="sxs-lookup"><span data-stu-id="f46a2-108">E.g.</span></span> <span data-ttu-id="f46a2-109">un cliente bank con app di servizi bancari hello bank sul proprio iPhone richiede una notifica quando viene effettuato un addebito sopra una certa quantità dal proprio account o una rete Intranet in cui un dipendente dal reparto finanziario che dispone di un'app di approvazione del budget sul suo Windows Phone richiede toobe toobe una notifica quando si riceve una richiesta di approvazione.</span><span class="sxs-lookup"><span data-stu-id="f46a2-109">a bank customer who has hello bank's banking app on her iPhone wants toobe notified when a debit is made above a certain amount from her account or an intranet scenario where an employee from finance department who has a budget approval app on his Windows Phone wants toobe notified when he gets an approval request.</span></span>

<span data-ttu-id="f46a2-110">conto bancario Hello o l'elaborazione di approvazione è toobe probabilmente eseguito in un sistema back-end che deve avviare un utente toohello push.</span><span class="sxs-lookup"><span data-stu-id="f46a2-110">hello bank account or approval processing is likely toobe done in some backend system which must initiate a push toohello user.</span></span> <span data-ttu-id="f46a2-111">Potrebbero essere presenti più tali back-end devono compilare tutti i sistemi hello stesso tipo di push tooimplement logica quando un evento è attiva una notifica.</span><span class="sxs-lookup"><span data-stu-id="f46a2-111">There may be multiple such backend systems which must all build hello same kind of logic tooimplement push when an event triggers a notification.</span></span> <span data-ttu-id="f46a2-112">complessità Hello qui si trova in diversi sistemi back-end con un sistema di push singolo in cui hello gli utenti finali possono hanno sottoscritto le notifiche toodifferent e possono anche essere più applicazioni per dispositivi mobili, ad esempio nel caso di hello di App per dispositivi mobili intranet di integrazione in un'applicazione per dispositivi mobili può essere notifiche tooreceive da più tali sistemi back-end.</span><span class="sxs-lookup"><span data-stu-id="f46a2-112">hello complexity here lies in integrating several backend systems together with a single push system where hello end users may have subscribed toodifferent notifications and there may even be multiple mobile applications e.g. in hello case of intranet mobile apps where one mobile application may want tooreceive notifications from multiple such backend systems.</span></span> <span data-ttu-id="f46a2-113">i sistemi back-end di Hello non conosce o la necessità di tooknow di push semantica/tecnologia qui una soluzione comune tradizionalmente toointroduce un componente che esegue il polling dei sistemi back-end hello per tutti gli eventi di interesse e responsabile per l'invio di messaggi push hello toohello client.</span><span class="sxs-lookup"><span data-stu-id="f46a2-113">hello backend systems do not know or need tooknow of push semantics/technology so a common solution here traditionally has been toointroduce a component which polls hello backend systems for any events of interest and is responsible for sending hello push messages toohello client.</span></span>
<span data-ttu-id="f46a2-114">Di seguito verranno descritti in una soluzione migliore utilizzando Azure Service Bus - modello di argomento o una sottoscrizione che consentiranno di ridurre la complessità di hello durante la creazione di soluzioni hello scalabile.</span><span class="sxs-lookup"><span data-stu-id="f46a2-114">Here we will talk about an even better solution using Azure Service Bus - Topic/Subscription model which will reduce hello complexity while making hello solution scalable.</span></span>

<span data-ttu-id="f46a2-115">Ecco architettura generale di hello della soluzione hello (generalizzata con più App per dispositivi mobili ma ugualmente applicabili quando è presente solo un'app per dispositivi mobili)</span><span class="sxs-lookup"><span data-stu-id="f46a2-115">Here is hello general architecture of hello solution (generalized with multiple mobile apps but equally applicable when there is only one mobile app)</span></span>

## <a name="architecture"></a><span data-ttu-id="f46a2-116">Architettura</span><span class="sxs-lookup"><span data-stu-id="f46a2-116">Architecture</span></span>
![][1]

<span data-ttu-id="f46a2-117">informazione di chiave Hello in questo diagramma dell'architettura è Bus di servizio di Azure che fornisce un modello di programmazione argomenti/sottoscrizioni (più su di esso in [programmazione di Service Bus Pub/Sub]).</span><span class="sxs-lookup"><span data-stu-id="f46a2-117">hello key piece in this architectural diagram is Azure Service Bus which provides a topics/subscriptions programming model (more on it at [Service Bus Pub/Sub programming]).</span></span> <span data-ttu-id="f46a2-118">il ricevitore Hello, che in questo caso, è back-end Mobile hello (in genere [servizio Mobile di Azure], che verrà avviata un'App per dispositivi mobili toohello push) non ricevono messaggi direttamente da sistemi back-end hello ma invece non è disponibile un livello di astrazione intermedio fornito da [Azure Service Bus] che consente di back-end mobile tooreceive messaggi da uno o più sistemi back-end.</span><span class="sxs-lookup"><span data-stu-id="f46a2-118">hello receiver, which in this case, is hello Mobile backend (typically [Azure Mobile Service], which will initiate a push toohello mobile apps) does not receive messages directly from hello backend systems but instead we have an intermediate abstraction layer provided by [Azure Service Bus] which enables mobile backend tooreceive messages from one or more backend systems.</span></span> <span data-ttu-id="f46a2-119">Un argomento del Bus di servizio deve toobe creato per ogni hello sistemi back-end, ad esempio Account, h, Finance che sono fondamentalmente "argomenti" di interesse che avvierà toobe i messaggi inviati come notifica push.</span><span class="sxs-lookup"><span data-stu-id="f46a2-119">A Service Bus Topic needs toobe created for each of hello backend systems e.g. Account, HR, Finance which are basically "topics" of interest which will initiate messages toobe sent as push notification.</span></span> <span data-ttu-id="f46a2-120">i sistemi back-end Hello invierà messaggi argomenti toothese.</span><span class="sxs-lookup"><span data-stu-id="f46a2-120">hello backend systems will send messages toothese topics.</span></span> <span data-ttu-id="f46a2-121">Un back-end Mobile possibile sottoscrivere tooone o più di tali argomenti tramite la creazione di una sottoscrizione del Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="f46a2-121">A Mobile Backend can subscribe tooone or more such topics by creating a Service Bus subscription.</span></span> <span data-ttu-id="f46a2-122">Questo darà hello back-end mobile tooreceive una notifica dal sistema back-end corrispondente hello.</span><span class="sxs-lookup"><span data-stu-id="f46a2-122">This will entitle hello mobile backend tooreceive a notification from hello corresponding backend system.</span></span> <span data-ttu-id="f46a2-123">Back-end mobile continua toolisten per i messaggi nelle sottoscrizioni e non appena arriva un messaggio, si trasforma e Invia come hub di notifica tooits di notifica.</span><span class="sxs-lookup"><span data-stu-id="f46a2-123">Mobile backend continues toolisten for messages on their subscriptions and as soon as a message arrives, it turns back and sends it as notification tooits notification hub.</span></span> <span data-ttu-id="f46a2-124">Gli hub di notifica infine recapita app per dispositivi mobili toohello messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="f46a2-124">Notification hubs then eventually delivers hello message toohello mobile app.</span></span> <span data-ttu-id="f46a2-125">Componenti chiave hello toosummarize, sono presenti:</span><span class="sxs-lookup"><span data-stu-id="f46a2-125">So toosummarize hello key components, we have:</span></span>

1. <span data-ttu-id="f46a2-126">Sistema back-end (sistemi LoB/legacy)</span><span class="sxs-lookup"><span data-stu-id="f46a2-126">Backend systems (LoB/Legacy systems)</span></span>
   * <span data-ttu-id="f46a2-127">Crea un argomento del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="f46a2-127">Creates Service Bus Topic</span></span>
   * <span data-ttu-id="f46a2-128">Invia un messaggio</span><span class="sxs-lookup"><span data-stu-id="f46a2-128">Sends Message</span></span>
2. <span data-ttu-id="f46a2-129">Back-end Mobile</span><span class="sxs-lookup"><span data-stu-id="f46a2-129">Mobile backend</span></span>
   * <span data-ttu-id="f46a2-130">Crea una sottoscrizione al servizio</span><span class="sxs-lookup"><span data-stu-id="f46a2-130">Creates Service Subscription</span></span>
   * <span data-ttu-id="f46a2-131">Riceve un messaggio (dal sistema back-end)</span><span class="sxs-lookup"><span data-stu-id="f46a2-131">Receives Message (from Backend system)</span></span>
   * <span data-ttu-id="f46a2-132">Invia notifica tooclients (tramite Hub di notifica di Azure)</span><span class="sxs-lookup"><span data-stu-id="f46a2-132">Sends notification tooclients (via Azure Notification Hub)</span></span>
3. <span data-ttu-id="f46a2-133">Applicazione per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="f46a2-133">Mobile Application</span></span>
   * <span data-ttu-id="f46a2-134">Riceve e visualizza la notifica</span><span class="sxs-lookup"><span data-stu-id="f46a2-134">Receives and display notification</span></span>

### <a name="benefits"></a><span data-ttu-id="f46a2-135">Vantaggi:</span><span class="sxs-lookup"><span data-stu-id="f46a2-135">Benefits:</span></span>
1. <span data-ttu-id="f46a2-136">Hello separazione tra mittente (sistemi back-end) e al destinatario di hello (app/servizio mobile tramite Hub di notifica) consente ai sistemi back-end aggiuntivi viene integrati con modifiche minime.</span><span class="sxs-lookup"><span data-stu-id="f46a2-136">hello decoupling between hello receiver (mobile app/service via Notification Hub) and sender (backend systems) enables additional backend systems being integrated with minimal change.</span></span>
2. <span data-ttu-id="f46a2-137">In questo modo anche scenario hello di più App per dispositivi mobili da tooreceive in grado di eventi da uno o più sistemi back-end.</span><span class="sxs-lookup"><span data-stu-id="f46a2-137">This also makes hello scenario of multiple mobile apps being able tooreceive events from one or more backend systems.</span></span>  

## <a name="sample"></a><span data-ttu-id="f46a2-138">Esempio:</span><span class="sxs-lookup"><span data-stu-id="f46a2-138">Sample:</span></span>
### <a name="prerequisites"></a><span data-ttu-id="f46a2-139">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f46a2-139">Prerequisites</span></span>
<span data-ttu-id="f46a2-140">È consigliabile completare hello seguenti esercitazioni toofamiliarize con i concetti di hello, nonché operazioni di creazione e configurazione più comuni:</span><span class="sxs-lookup"><span data-stu-id="f46a2-140">You should complete hello following tutorials toofamiliarize with hello concepts as well as common creation & configuration steps:</span></span>

1. <span data-ttu-id="f46a2-141">[programmazione di Service Bus Pub/Sub] -dettagli hello di utilizzo con Service Bus argomenti/sottoscrizioni, illustra come toocreate uno spazio dei nomi toocontain argomenti/sottoscrizioni, come toosend & ricevere messaggi da essi.</span><span class="sxs-lookup"><span data-stu-id="f46a2-141">[Service Bus Pub/Sub programming] - This explains hello details of working with Service Bus Topics/Subscriptions, how toocreate a namespace toocontain topics/subscriptions, how toosend & receive messages from them.</span></span>
2. <span data-ttu-id="f46a2-142">[Gli hub di notifica - esercitazione universali di Windows] -questo spiega come tooset fino a un'applicazione Windows Store e usare tooregister gli hub di notifica e quindi ricevere le notifiche.</span><span class="sxs-lookup"><span data-stu-id="f46a2-142">[Notification Hubs - Windows Universal tutorial] - This explains how tooset up a Windows Store app and use Notification Hubs tooregister and then receive notifications.</span></span>

### <a name="sample-code"></a><span data-ttu-id="f46a2-143">Codice di esempio</span><span class="sxs-lookup"><span data-stu-id="f46a2-143">Sample code</span></span>
<span data-ttu-id="f46a2-144">il codice di esempio completo di Hello è disponibile all'indirizzo [degli esempi di Hub di notifica].</span><span class="sxs-lookup"><span data-stu-id="f46a2-144">hello full sample code is available at [Notification Hub Samples].</span></span> <span data-ttu-id="f46a2-145">Il codice è suddiviso in tre componenti:</span><span class="sxs-lookup"><span data-stu-id="f46a2-145">It is split into three components:</span></span>

1. <span data-ttu-id="f46a2-146">**EnterprisePushBackendSystem**</span><span class="sxs-lookup"><span data-stu-id="f46a2-146">**EnterprisePushBackendSystem**</span></span>
   
    <span data-ttu-id="f46a2-147">a.</span><span class="sxs-lookup"><span data-stu-id="f46a2-147">a.</span></span> <span data-ttu-id="f46a2-148">Questo progetto usa hello *Windowsazure* pacchetto Nuget e si basa su [programmazione di Service Bus Pub/Sub].</span><span class="sxs-lookup"><span data-stu-id="f46a2-148">This project uses hello *WindowsAzure.ServiceBus* Nuget package and is  based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="f46a2-149">b.</span><span class="sxs-lookup"><span data-stu-id="f46a2-149">b.</span></span> <span data-ttu-id="f46a2-150">Si tratta di un semplice in c# console app toosimulate un sistema LoB che avvia toobe messaggio hello recapitati toohello app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="f46a2-150">This is a simple C# console app toosimulate an LoB system which initiates hello message toobe delivered toohello mobile app.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello topic where we will send notifications
            CreateTopic(connectionString);
   
            // Send message
            SendMessage(connectionString);
        }
   
    <span data-ttu-id="f46a2-151">c.</span><span class="sxs-lookup"><span data-stu-id="f46a2-151">c.</span></span> <span data-ttu-id="f46a2-152">`CreateTopic`è argomento del Bus di servizio utilizzato toocreate hello in cui Microsoft invierà i messaggi.</span><span class="sxs-lookup"><span data-stu-id="f46a2-152">`CreateTopic` is used toocreate hello Service Bus topic where we will send messages.</span></span>
   
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
   
    <span data-ttu-id="f46a2-153">d.</span><span class="sxs-lookup"><span data-stu-id="f46a2-153">d.</span></span> <span data-ttu-id="f46a2-154">`SendMessage`viene utilizzato toosend hello messaggi toothis argomento del Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="f46a2-154">`SendMessage` is used toosend hello messages toothis Service Bus Topic.</span></span> <span data-ttu-id="f46a2-155">Qui stiamo semplicemente inviando un set di argomento toohello messaggi casuale periodicamente a scopo di hello dell'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="f46a2-155">Here we are simply sending a set of random messages toohello topic periodically for hello purpose of hello sample.</span></span> <span data-ttu-id="f46a2-156">Nella realtà, sarebbe presente un sistema back-end che invia i messaggi quando si verifica un evento.</span><span class="sxs-lookup"><span data-stu-id="f46a2-156">Normally there will be a backend system which will send messages when an event occurs.</span></span>
   
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
2. <span data-ttu-id="f46a2-157">**ReceiveAndSendNotification**</span><span class="sxs-lookup"><span data-stu-id="f46a2-157">**ReceiveAndSendNotification**</span></span>
   
    <span data-ttu-id="f46a2-158">a.</span><span class="sxs-lookup"><span data-stu-id="f46a2-158">a.</span></span> <span data-ttu-id="f46a2-159">Questo progetto usa hello *Windowsazure* e *Microsoft.Web.WebJobs.Publish* Nuget pacchetti e si basa sul [programmazione di Service Bus Pub/Sub].</span><span class="sxs-lookup"><span data-stu-id="f46a2-159">This project uses hello *WindowsAzure.ServiceBus* and *Microsoft.Web.WebJobs.Publish* Nuget packages and is based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="f46a2-160">b.</span><span class="sxs-lookup"><span data-stu-id="f46a2-160">b.</span></span> <span data-ttu-id="f46a2-161">Si tratta di un'altra console app c# che verranno eseguiti come un [processo Web di Azure] perché ha toorun continuamente toolisten per i messaggi generati dal hello LoB/sistemi back-end.</span><span class="sxs-lookup"><span data-stu-id="f46a2-161">This is another C# console app which we will run as an [Azure WebJob] since it has toorun continuously toolisten for messages from hello LoB/backend systems.</span></span> <span data-ttu-id="f46a2-162">L'app sarà parte del back-end Mobile.</span><span class="sxs-lookup"><span data-stu-id="f46a2-162">This will be part of your Mobile backend.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                     CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello subscription which will receive messages
            CreateSubscription(connectionString);
   
            // Receive message
            ReceiveMessageAndSendNotification(connectionString);
        }
   
    <span data-ttu-id="f46a2-163">c.</span><span class="sxs-lookup"><span data-stu-id="f46a2-163">c.</span></span> <span data-ttu-id="f46a2-164">`CreateSubscription`è utilizzato toocreate una sottoscrizione del Bus di servizio per l'argomento hello in cui il sistema di back-end hello verrà inviati i messaggi.</span><span class="sxs-lookup"><span data-stu-id="f46a2-164">`CreateSubscription` is used toocreate a Service Bus subscription for hello topic where hello backend system will send messages.</span></span> <span data-ttu-id="f46a2-165">A seconda dello scenario di business hello, questo componente creerà una o più sottoscrizioni toocorresponding argomenti (ad esempio, alcuni può ricevere messaggi dal sistema delle risorse Umane, alcune da sistema Finance e così via)</span><span class="sxs-lookup"><span data-stu-id="f46a2-165">Depending on hello business scenario, this component will create one or more subscriptions toocorresponding topics (e.g. some may be receiving messages from HR system, some from Finance system, and so on)</span></span>
   
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
   
    <span data-ttu-id="f46a2-166">d.</span><span class="sxs-lookup"><span data-stu-id="f46a2-166">d.</span></span> <span data-ttu-id="f46a2-167">ReceiveMessageAndSendNotification è il messaggio hello tooread utilizzato da un argomento di hello utilizzando la relativa sottoscrizione e se ha esito positivo hello leggere quindi creare un toohello toobe inviate notifiche (nello scenario di esempio hello una notifica di tipo avviso popup nativo di Windows) per dispositivi mobili applicazione che utilizza gli hub di notifica di Azure.</span><span class="sxs-lookup"><span data-stu-id="f46a2-167">ReceiveMessageAndSendNotification is used tooread hello message from hello topic using its subscription and if hello read is successful then craft a notification (in hello sample scenario a Windows native toast notification) toobe sent toohello mobile application using Azure Notification Hubs.</span></span>
   
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
   
    <span data-ttu-id="f46a2-168">e.</span><span class="sxs-lookup"><span data-stu-id="f46a2-168">e.</span></span> <span data-ttu-id="f46a2-169">Per la pubblicazione come un **processo Web**, fare clic con il pulsante destro sulla soluzione hello in Visual Studio e selezionare **pubblica come processo Web**</span><span class="sxs-lookup"><span data-stu-id="f46a2-169">For publishing this as a **WebJob**, right click on hello solution in Visual Studio and select **Publish as WebJob**</span></span>
   
    ![][2]
   
    <span data-ttu-id="f46a2-170">f.</span><span class="sxs-lookup"><span data-stu-id="f46a2-170">f.</span></span> <span data-ttu-id="f46a2-171">Selezionare il profilo di pubblicazione e creare un nuovo sito Web di Azure, se non esiste già che ospiterà il processo Web e dopo aver sito Web di hello quindi **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="f46a2-171">Select your publishing profile and create a new Azure WebSite if it doesnt exist already which will host this WebJob and once you have hello WebSite then **Publish**.</span></span>
   
    ![][3]
   
    <span data-ttu-id="f46a2-172">g.</span><span class="sxs-lookup"><span data-stu-id="f46a2-172">g.</span></span> <span data-ttu-id="f46a2-173">Configurare hello "Eseguire continuamente" toobe di processo in modo che quando si accede toohello [portale di Azure classico] dovrebbe essere simile alla seguente hello:</span><span class="sxs-lookup"><span data-stu-id="f46a2-173">Configure hello job toobe "Run Continuously" so that when you log in toohello [Azure Classic Portal] you should see something like hello following:</span></span>
   
    ![][4]
3. <span data-ttu-id="f46a2-174">**EnterprisePushMobileApp**</span><span class="sxs-lookup"><span data-stu-id="f46a2-174">**EnterprisePushMobileApp**</span></span>
   
    <span data-ttu-id="f46a2-175">a.</span><span class="sxs-lookup"><span data-stu-id="f46a2-175">a.</span></span> <span data-ttu-id="f46a2-176">Si tratta di un'applicazione Windows Store che riceverà le notifiche di tipo avviso popup dall'esecuzione di processi Web hello come parte di back-end per dispositivi mobili e visualizzarli.</span><span class="sxs-lookup"><span data-stu-id="f46a2-176">This is a Windows Store application which will receive toast notifications from hello WebJob running as part of your Mobile backend and display it.</span></span> <span data-ttu-id="f46a2-177">Si basa su quanto riportato in [Gli hub di notifica - esercitazione universali di Windows].</span><span class="sxs-lookup"><span data-stu-id="f46a2-177">This is based on [Notification Hubs - Windows Universal tutorial].</span></span>  
   
    <span data-ttu-id="f46a2-178">b.</span><span class="sxs-lookup"><span data-stu-id="f46a2-178">b.</span></span> <span data-ttu-id="f46a2-179">Verificare che l'applicazione notifiche di tipo avviso popup tooreceive abilitato.</span><span class="sxs-lookup"><span data-stu-id="f46a2-179">Ensure that your application is enabled tooreceive toast notifications.</span></span>
   
    <span data-ttu-id="f46a2-180">c.</span><span class="sxs-lookup"><span data-stu-id="f46a2-180">c.</span></span> <span data-ttu-id="f46a2-181">Verificare che hello dopo il codice di registrazione di hub di notifica viene chiamato all'avvio dell'applicazione hello (dopo la sostituzione di hello *HubName* e *DefaultListenSharedAccessSignature*:</span><span class="sxs-lookup"><span data-stu-id="f46a2-181">Ensure that hello following Notification Hubs registration code is being called at hello App start up (after replacing hello *HubName* and *DefaultListenSharedAccessSignature*:</span></span>
   
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

### <a name="running-sample"></a><span data-ttu-id="f46a2-182">Esecuzione di esempio:</span><span class="sxs-lookup"><span data-stu-id="f46a2-182">Running sample:</span></span>
1. <span data-ttu-id="f46a2-183">Verificare che il processo Web venga eseguita correttamente e pianificata troppo "esecuzione continua".</span><span class="sxs-lookup"><span data-stu-id="f46a2-183">Ensure that your WebJob is running successfully and scheduled too"Run Continuously".</span></span>
2. <span data-ttu-id="f46a2-184">Eseguire hello **EnterprisePushMobileApp** che verrà avviata l'app di Windows Store hello.</span><span class="sxs-lookup"><span data-stu-id="f46a2-184">Run hello **EnterprisePushMobileApp** which will start hello Windows Store app.</span></span>
3. <span data-ttu-id="f46a2-185">Eseguire hello **EnterprisePushBackendSystem** applicazione console che consente di simulare back-end LoB hello e inizierà a inviare messaggi ed è necessario verificare le notifiche di tipo avviso popup visualizzato hello seguente:</span><span class="sxs-lookup"><span data-stu-id="f46a2-185">Run hello **EnterprisePushBackendSystem** console application which will simulate hello LoB backend and will start sending messages and you should see toast notifications appearing like hello following:</span></span>
   
    ![][5]
4. <span data-ttu-id="f46a2-186">messaggi hello inviati originariamente tooService argomenti del Bus di cui è stato monitorato per le sottoscrizioni del Bus di servizio nel processo Web.</span><span class="sxs-lookup"><span data-stu-id="f46a2-186">hello messages were originally sent tooService Bus topics which was being monitored by Service Bus subscriptions in your Web Job.</span></span> <span data-ttu-id="f46a2-187">Una volta ricevuto un messaggio, una notifica creata e inviata toohello app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="f46a2-187">Once a message was received, a notification was created and sent toohello mobile app.</span></span> <span data-ttu-id="f46a2-188">È possibile esaminare hello processo Web registra tooconfirm hello elaborazione quando si passa toohello collegano log [portale di Azure classico] per il processo Web:</span><span class="sxs-lookup"><span data-stu-id="f46a2-188">You can look through hello WebJob logs tooconfirm hello processing when you go toohello Logs link in [Azure Classic Portal] for your Web Job:</span></span>
   
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
