---
title: 'Hub di notifica: architettura push aziendale'
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
ms.openlocfilehash: ae7c1c9644ecfe7fe4ad6e332cc0683a3b5df22f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="enterprise-push-architectural-guidance"></a><span data-ttu-id="db476-103">Guida all'architettura push aziendale</span><span class="sxs-lookup"><span data-stu-id="db476-103">Enterprise push architectural guidance</span></span>
<span data-ttu-id="db476-104">Al giorno d'oggi, le aziende stanno gradualmente passando alla creazione di applicazioni per dispositivi mobili sia per gli utenti finali (esterni) che per i dipendenti (interni).</span><span class="sxs-lookup"><span data-stu-id="db476-104">Enterprises today are gradually moving towards creating mobile applications for either their end users (external) or for the employees (internal).</span></span> <span data-ttu-id="db476-105">Le aziende dispongono di sistemi back-end già esistenti, ovvero mainframe o applicazioni LoB che è necessario integrare nell'architettura delle applicazioni per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="db476-105">They have existing backend systems in place be it mainframes or some LoB applications which must be integrated into the mobile application architecture.</span></span> <span data-ttu-id="db476-106">In questa Guida verrà illustrato come eseguire questa integrazione nel modo migliore possibile, fornendo possibili soluzioni per scenari comuni.</span><span class="sxs-lookup"><span data-stu-id="db476-106">This guide will talk about how best to do this integration recommending possible solution to common scenarios.</span></span>

<span data-ttu-id="db476-107">Una richiesta frequente riguarda l'invio di notifiche push agli utenti tramite l'applicazione per dispositivi mobili in uso quando si verifica un evento di interesse nei sistemi back-end.</span><span class="sxs-lookup"><span data-stu-id="db476-107">A frequent requirement is for sending push notification to the users through their mobile application when an event of interest occurs in the backend systems.</span></span> <span data-ttu-id="db476-108">Ad esempio,</span><span class="sxs-lookup"><span data-stu-id="db476-108">E.g.</span></span> <span data-ttu-id="db476-109">una cliente di una banca ha installato sul proprio iPhone l'app dei servizi bancari della banca stessa e desidera ricevere una notifica quando sul conto viene effettuato un addebito superiore a un determinato importo. Oppure, in uno scenario intranet, un dipendente del reparto finanziario ha installato sul proprio Windows Phone una app per l'approvazione dei budget e desidera ricevere una notifica quando gli viene inviata una richiesta di approvazione.</span><span class="sxs-lookup"><span data-stu-id="db476-109">a bank customer who has the bank's banking app on her iPhone wants to be notified when a debit is made above a certain amount from her account or an intranet scenario where an employee from finance department who has a budget approval app on his Windows Phone wants to be notified when he gets an approval request.</span></span>

<span data-ttu-id="db476-110">È probabile che l'elaborazione del conto o dell'approvazione venga eseguita in un qualche sistema back-end che deve avviare un'operazione push verso l'utente.</span><span class="sxs-lookup"><span data-stu-id="db476-110">The bank account or approval processing is likely to be done in some backend system which must initiate a push to the user.</span></span> <span data-ttu-id="db476-111">È possibile che siano presenti diversi sistemi back-end che devono eseguire la stessa tipologia di logica per implementare un push quando un evento attiva una notifica.</span><span class="sxs-lookup"><span data-stu-id="db476-111">There may be multiple such backend systems which must all build the same kind of logic to implement push when an event triggers a notification.</span></span> <span data-ttu-id="db476-112">In questo caso la complessità è dovuta alla necessità di integrare numerosi back-end con un singolo sistema di push, dove gli utenti finali possono aver eseguito la sottoscrizione a diverse notifiche e dove possono essere usate più applicazioni mobili, ad esempio nel caso di applicazioni per dispositivi mobili intranet che possono ricevere notifiche da diversi sistemi back-end.</span><span class="sxs-lookup"><span data-stu-id="db476-112">The complexity here lies in integrating several backend systems together with a single push system where the end users may have subscribed to different notifications and there may even be multiple mobile applications e.g. in the case of intranet mobile apps where one mobile application may want to receive notifications from multiple such backend systems.</span></span> <span data-ttu-id="db476-113">I sistemi back-end non conoscono o non hanno necessità di conoscere la semantica e/o la tecnologia di push. Per questo motivo, una soluzione comunemente usata fino ad ora consiste nell'introdurre un componente che esegue il polling dei sistemi back-end per qualsiasi evento di interesse ed è responsabile dell'invio di messaggi push al client.</span><span class="sxs-lookup"><span data-stu-id="db476-113">The backend systems do not know or need to know of push semantics/technology so a common solution here traditionally has been to introduce a component which polls the backend systems for any events of interest and is responsible for sending the push messages to the client.</span></span>
<span data-ttu-id="db476-114">Di seguito viene descritta una soluzione ancora migliore che prevede l'uso del modello Bus di servizio di Azure - Argomento/Sottoscrizione. Tale modello, infatti, riduce la complessità della soluzione e la rende scalabile.</span><span class="sxs-lookup"><span data-stu-id="db476-114">Here we will talk about an even better solution using Azure Service Bus - Topic/Subscription model which will reduce the complexity while making the solution scalable.</span></span>

<span data-ttu-id="db476-115">Di seguito è descritta l'architettura generale della soluzione, descritta con numerose app per dispositivi mobili ma ugualmente applicabile nel caso in cui ne venga usata una soltanto.</span><span class="sxs-lookup"><span data-stu-id="db476-115">Here is the general architecture of the solution (generalized with multiple mobile apps but equally applicable when there is only one mobile app)</span></span>

## <a name="architecture"></a><span data-ttu-id="db476-116">Architettura</span><span class="sxs-lookup"><span data-stu-id="db476-116">Architecture</span></span>
![][1]

<span data-ttu-id="db476-117">L'elemento chiave di questo diagramma dell'architettura è il bus di servizio di Azure, che fornisce un modello di programmazione di tipo argomenti/sottoscrizioni. Per altre informazioni su tale modello, vedere [Come usare gli argomenti e le sottoscrizioni del bus di servizio].</span><span class="sxs-lookup"><span data-stu-id="db476-117">The key piece in this architectural diagram is Azure Service Bus which provides a topics/subscriptions programming model (more on it at [Service Bus Pub/Sub programming]).</span></span> <span data-ttu-id="db476-118">Il ricevitore, in questo caso il back-end Mobile (in genere [Servizi mobili di Azure], che avvia un'operazione push alle app per dispositivi mobili), non riceve messaggi direttamente dai sistemi back-end. È disponibile invece un livello di astrazione intermedio fornito dal [bus di servizio di Azure] che consente al back-end Mobile di ricevere messaggi da uno o più sistemi back-end.</span><span class="sxs-lookup"><span data-stu-id="db476-118">The receiver, which in this case, is the Mobile backend (typically [Azure Mobile Service], which will initiate a push to the mobile apps) does not receive messages directly from the backend systems but instead we have an intermediate abstraction layer provided by [Azure Service Bus] which enables mobile backend to receive messages from one or more backend systems.</span></span> <span data-ttu-id="db476-119">È necessario creare un argomento del bus di servizio per ciascuno dei sistemi back-end, ad esempio Contabilità, Risorse umane e Finanza. Si tratta fondamentalmente di "argomenti" rilevanti che danno luogo a messaggi da inviare come notifiche push.</span><span class="sxs-lookup"><span data-stu-id="db476-119">A Service Bus Topic needs to be created for each of the backend systems e.g. Account, HR, Finance which are basically "topics" of interest which will initiate messages to be sent as push notification.</span></span> <span data-ttu-id="db476-120">I sistemi back-end invieranno messaggi a questi argomenti.</span><span class="sxs-lookup"><span data-stu-id="db476-120">The backend systems will send messages to these topics.</span></span> <span data-ttu-id="db476-121">Un back-end Mobile può sottoscrivere uno o più di tali argomenti creando una sottoscrizione del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="db476-121">A Mobile Backend can subscribe to one or more such topics by creating a Service Bus subscription.</span></span> <span data-ttu-id="db476-122">Questo autorizza il back-end Mobile a ricevere una notifica dal sistema back-end corrispondente.</span><span class="sxs-lookup"><span data-stu-id="db476-122">This will entitle the mobile backend to receive a notification from the corresponding backend system.</span></span> <span data-ttu-id="db476-123">Il back-end Mobile continua a rimanere in ascolto per rilevare i messaggi inviati alla sottoscrizione e, non appena ne arriva uno, lo invia come notifica all'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="db476-123">Mobile backend continues to listen for messages on their subscriptions and as soon as a message arrives, it turns back and sends it as notification to its notification hub.</span></span> <span data-ttu-id="db476-124">L'hub di notifica invia infine il messaggio all'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="db476-124">Notification hubs then eventually delivers the message to the mobile app.</span></span> <span data-ttu-id="db476-125">Di seguito sono riepilogati i componenti chiave:</span><span class="sxs-lookup"><span data-stu-id="db476-125">So to summarize the key components, we have:</span></span>

1. <span data-ttu-id="db476-126">Sistema back-end (sistemi LoB/legacy)</span><span class="sxs-lookup"><span data-stu-id="db476-126">Backend systems (LoB/Legacy systems)</span></span>
   * <span data-ttu-id="db476-127">Crea un argomento del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="db476-127">Creates Service Bus Topic</span></span>
   * <span data-ttu-id="db476-128">Invia un messaggio</span><span class="sxs-lookup"><span data-stu-id="db476-128">Sends Message</span></span>
2. <span data-ttu-id="db476-129">Back-end Mobile</span><span class="sxs-lookup"><span data-stu-id="db476-129">Mobile backend</span></span>
   * <span data-ttu-id="db476-130">Crea una sottoscrizione al servizio</span><span class="sxs-lookup"><span data-stu-id="db476-130">Creates Service Subscription</span></span>
   * <span data-ttu-id="db476-131">Riceve un messaggio (dal sistema back-end)</span><span class="sxs-lookup"><span data-stu-id="db476-131">Receives Message (from Backend system)</span></span>
   * <span data-ttu-id="db476-132">Invia la notifica al client (tramite Hub di notifica di Azure)</span><span class="sxs-lookup"><span data-stu-id="db476-132">Sends notification to clients (via Azure Notification Hub)</span></span>
3. <span data-ttu-id="db476-133">Applicazione per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="db476-133">Mobile Application</span></span>
   * <span data-ttu-id="db476-134">Riceve e visualizza la notifica</span><span class="sxs-lookup"><span data-stu-id="db476-134">Receives and display notification</span></span>

### <a name="benefits"></a><span data-ttu-id="db476-135">Vantaggi:</span><span class="sxs-lookup"><span data-stu-id="db476-135">Benefits:</span></span>
1. <span data-ttu-id="db476-136">Il disaccoppiamento tra il ricevitore (app/servizio per dispositivi mobili tramite Hub di notifica) e il mittente(sistemi back-end) consente l'integrazione di sistemi back-end aggiuntivi con modifiche minime.</span><span class="sxs-lookup"><span data-stu-id="db476-136">The decoupling between the receiver (mobile app/service via Notification Hub) and sender (backend systems) enables additional backend systems being integrated with minimal change.</span></span>
2. <span data-ttu-id="db476-137">In questo modo, è possibile ricevere eventi da uno o più sistemi back-end anche nello scenario con più app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="db476-137">This also makes the scenario of multiple mobile apps being able to receive events from one or more backend systems.</span></span>  

## <a name="sample"></a><span data-ttu-id="db476-138">Esempio:</span><span class="sxs-lookup"><span data-stu-id="db476-138">Sample:</span></span>
### <a name="prerequisites"></a><span data-ttu-id="db476-139">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="db476-139">Prerequisites</span></span>
<span data-ttu-id="db476-140">È necessario completare le seguenti esercitazioni per acquisire familiarità con i concetti e con i comuni passaggi di creazione e configurazione:</span><span class="sxs-lookup"><span data-stu-id="db476-140">You should complete the following tutorials to familiarize with the concepts as well as common creation & configuration steps:</span></span>

1. <span data-ttu-id="db476-141">[Come usare gli argomenti e le sottoscrizioni del bus di servizio]: viene illustrato nei dettagli l'utilizzo di argomenti/sottoscrizioni del bus di servizio. Viene inoltre mostrato come creare uno spazio dei nomi per contenere argomenti/sottoscrizioni e come inviare e ricevere messaggi da questi ultimi.</span><span class="sxs-lookup"><span data-stu-id="db476-141">[Service Bus Pub/Sub programming] - This explains the details of working with Service Bus Topics/Subscriptions, how to create a namespace to contain topics/subscriptions, how to send & receive messages from them.</span></span>
2. <span data-ttu-id="db476-142">[Introduzione ad Hub di notifica - Esercitazione per Windows Universal] : illustra come configurare un'app di Windows Store e usare Hub di notifica per registrare e quindi ricevere le notifiche.</span><span class="sxs-lookup"><span data-stu-id="db476-142">[Notification Hubs - Windows Universal tutorial] - This explains how to set up a Windows Store app and use Notification Hubs to register and then receive notifications.</span></span>

### <a name="sample-code"></a><span data-ttu-id="db476-143">Codice di esempio</span><span class="sxs-lookup"><span data-stu-id="db476-143">Sample code</span></span>
<span data-ttu-id="db476-144">Il codice completo è disponibile nella pagina relativa agli [esempi di Hub di notifica].</span><span class="sxs-lookup"><span data-stu-id="db476-144">The full sample code is available at [Notification Hub Samples].</span></span> <span data-ttu-id="db476-145">Il codice è suddiviso in tre componenti:</span><span class="sxs-lookup"><span data-stu-id="db476-145">It is split into three components:</span></span>

1. <span data-ttu-id="db476-146">**EnterprisePushBackendSystem**</span><span class="sxs-lookup"><span data-stu-id="db476-146">**EnterprisePushBackendSystem**</span></span>
   
    <span data-ttu-id="db476-147">a.</span><span class="sxs-lookup"><span data-stu-id="db476-147">a.</span></span> <span data-ttu-id="db476-148">Il progetto usa il pacchetto NuGet *WindowsAzure.ServiceBus* ed è basato su quanto riportato in [Come usare gli argomenti e le sottoscrizioni del bus di servizio].</span><span class="sxs-lookup"><span data-stu-id="db476-148">This project uses the *WindowsAzure.ServiceBus* Nuget package and is  based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="db476-149">b.</span><span class="sxs-lookup"><span data-stu-id="db476-149">b.</span></span> <span data-ttu-id="db476-150">Si tratta di una app console C# per simulare un sistema LoB che avvia il messaggio da recapitare all'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="db476-150">This is a simple C# console app to simulate an LoB system which initiates the message to be delivered to the mobile app.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create the topic where we will send notifications
            CreateTopic(connectionString);
   
            // Send message
            SendMessage(connectionString);
        }
   
    <span data-ttu-id="db476-151">c.</span><span class="sxs-lookup"><span data-stu-id="db476-151">c.</span></span> <span data-ttu-id="db476-152">`CreateTopic` viene usato per creare l'argomento del bus di servizio a cui verranno inviati i messaggi.</span><span class="sxs-lookup"><span data-stu-id="db476-152">`CreateTopic` is used to create the Service Bus topic where we will send messages.</span></span>
   
        public static void CreateTopic(string connectionString)
        {
            // Create the topic if it does not exist already
   
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.TopicExists(sampleTopic))
            {
                namespaceManager.CreateTopic(sampleTopic);
            }
        }
   
    <span data-ttu-id="db476-153">d.</span><span class="sxs-lookup"><span data-stu-id="db476-153">d.</span></span> <span data-ttu-id="db476-154">`SendMessage` viene usato per inviare i messaggi a questo argomento del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="db476-154">`SendMessage` is used to send the messages to this Service Bus Topic.</span></span> <span data-ttu-id="db476-155">Ai fini dell'esempio, viene semplicemente inviato, a cadenza periodica, un insieme di messaggi casuali all'argomento.</span><span class="sxs-lookup"><span data-stu-id="db476-155">Here we are simply sending a set of random messages to the topic periodically for the purpose of the sample.</span></span> <span data-ttu-id="db476-156">Nella realtà, sarebbe presente un sistema back-end che invia i messaggi quando si verifica un evento.</span><span class="sxs-lookup"><span data-stu-id="db476-156">Normally there will be a backend system which will send messages when an event occurs.</span></span>
   
        public static void SendMessage(string connectionString)
        {
            TopicClient client =
                TopicClient.CreateFromConnectionString(connectionString, sampleTopic);
   
            // Sends random messages every 10 seconds to the topic
            string[] messages =
            {
                "Employee Id '{0}' has joined.",
                "Employee Id '{0}' has left.",
                "Employee Id '{0}' has switched to a different team."
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
2. <span data-ttu-id="db476-157">**ReceiveAndSendNotification**</span><span class="sxs-lookup"><span data-stu-id="db476-157">**ReceiveAndSendNotification**</span></span>
   
    <span data-ttu-id="db476-158">a.</span><span class="sxs-lookup"><span data-stu-id="db476-158">a.</span></span> <span data-ttu-id="db476-159">Il progetto usa i pacchetti NuGet *WindowsAzure.ServiceBus* e *Microsoft.Web.WebJobs.Publish* ed è basato su quanto riportato in [Come usare gli argomenti e le sottoscrizioni del bus di servizio].</span><span class="sxs-lookup"><span data-stu-id="db476-159">This project uses the *WindowsAzure.ServiceBus* and *Microsoft.Web.WebJobs.Publish* Nuget packages and is based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="db476-160">b.</span><span class="sxs-lookup"><span data-stu-id="db476-160">b.</span></span> <span data-ttu-id="db476-161">Si tratta di un'altra app console C# che verrà eseguita come processo [Web di Azure]. Questa app deve infatti essere eseguita continuamente per ascoltare i messaggi dei sistemi LOB/back-end.</span><span class="sxs-lookup"><span data-stu-id="db476-161">This is another C# console app which we will run as an [Azure WebJob] since it has to run continuously to listen for messages from the LoB/backend systems.</span></span> <span data-ttu-id="db476-162">L'app sarà parte del back-end Mobile.</span><span class="sxs-lookup"><span data-stu-id="db476-162">This will be part of your Mobile backend.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                     CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create the subscription which will receive messages
            CreateSubscription(connectionString);
   
            // Receive message
            ReceiveMessageAndSendNotification(connectionString);
        }
   
    <span data-ttu-id="db476-163">c.</span><span class="sxs-lookup"><span data-stu-id="db476-163">c.</span></span> <span data-ttu-id="db476-164">`CreateSubscription` viene usato per creare una sottoscrizione del bus di servizio per l'argomento in cui il sistema back-end invierà i messaggi.</span><span class="sxs-lookup"><span data-stu-id="db476-164">`CreateSubscription` is used to create a Service Bus subscription for the topic where the backend system will send messages.</span></span> <span data-ttu-id="db476-165">A seconda dello scenario aziendale, questo argomento crea una o più sottoscrizioni agli argomenti corrispondenti. Può, ad esempio, ricevere messaggi dal sistema Risorse umane, dal sistema Finanza e così via.</span><span class="sxs-lookup"><span data-stu-id="db476-165">Depending on the business scenario, this component will create one or more subscriptions to corresponding topics (e.g. some may be receiving messages from HR system, some from Finance system, and so on)</span></span>
   
        static void CreateSubscription(string connectionString)
        {
            // Create the subscription if it does not exist already
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.SubscriptionExists(sampleTopic, sampleSubscription))
            {
                namespaceManager.CreateSubscription(sampleTopic, sampleSubscription);
            }
        }
   
    <span data-ttu-id="db476-166">d.</span><span class="sxs-lookup"><span data-stu-id="db476-166">d.</span></span> <span data-ttu-id="db476-167">ReceiveMessageAndSendNotification viene usato per leggere il messaggio inviato dall'argomento usando la relativa sottoscrizione. Se l'operazione di lettura ha esito positivo, viene creata una notifica (nello scenario di esempio una notifica di tipo avviso popup nativo di Windows) da inviare all'applicazione mobile tramite gli hub di notifica di Windows.</span><span class="sxs-lookup"><span data-stu-id="db476-167">ReceiveMessageAndSendNotification is used to read the message from the topic using its subscription and if the read is successful then craft a notification (in the sample scenario a Windows native toast notification) to be sent to the mobile application using Azure Notification Hubs.</span></span>
   
        static void ReceiveMessageAndSendNotification(string connectionString)
        {
            // Initialize the Notification Hub
            string hubConnectionString = CloudConfigurationManager.GetSetting
                    ("Microsoft.NotificationHub.ConnectionString");
            hub = NotificationHubClient.CreateClientFromConnectionString
                    (hubConnectionString, "enterprisepushservicehub");
   
            SubscriptionClient Client =
                SubscriptionClient.CreateFromConnectionString
                        (connectionString, sampleTopic, sampleSubscription);
   
            Client.Receive();
   
            // Continuously process messages received from the subscription
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
   
    <span data-ttu-id="db476-168">e.</span><span class="sxs-lookup"><span data-stu-id="db476-168">e.</span></span> <span data-ttu-id="db476-169">Per pubblicare questo elemento come **processo Web**, in Visual Studio fare clic con il pulsante destro del mouse sulla soluzione e selezionare **Pubblica come processo Web di Azure**</span><span class="sxs-lookup"><span data-stu-id="db476-169">For publishing this as a **WebJob**, right click on the solution in Visual Studio and select **Publish as WebJob**</span></span>
   
    ![][2]
   
    <span data-ttu-id="db476-170">f.</span><span class="sxs-lookup"><span data-stu-id="db476-170">f.</span></span> <span data-ttu-id="db476-171">Selezionare il proprio profilo di pubblicazione e, se non è già presente, creare un nuovo sito Web di Azure che ospiterà questo processo Web, quindi fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="db476-171">Select your publishing profile and create a new Azure WebSite if it doesnt exist already which will host this WebJob and once you have the WebSite then **Publish**.</span></span>
   
    ![][3]
   
    <span data-ttu-id="db476-172">g.</span><span class="sxs-lookup"><span data-stu-id="db476-172">g.</span></span> <span data-ttu-id="db476-173">Configurare il processo per l'esecuzione continua, in modo che, quando si accede al [portale di Azure classico] , venga visualizzata una schermata simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="db476-173">Configure the job to be "Run Continuously" so that when you log in to the [Azure Classic Portal] you should see something like the following:</span></span>
   
    ![][4]
3. <span data-ttu-id="db476-174">**EnterprisePushMobileApp**</span><span class="sxs-lookup"><span data-stu-id="db476-174">**EnterprisePushMobileApp**</span></span>
   
    <span data-ttu-id="db476-175">a.</span><span class="sxs-lookup"><span data-stu-id="db476-175">a.</span></span> <span data-ttu-id="db476-176">Si tratta di un'applicazione Windows Store che riceve notifiche di tipo avviso popup dal processo Web in esecuzione come parte del back-end Mobile e le visualizza.</span><span class="sxs-lookup"><span data-stu-id="db476-176">This is a Windows Store application which will receive toast notifications from the WebJob running as part of your Mobile backend and display it.</span></span> <span data-ttu-id="db476-177">Si basa su quanto riportato in [Introduzione ad Hub di notifica - Esercitazione per Windows Universal].</span><span class="sxs-lookup"><span data-stu-id="db476-177">This is based on [Notification Hubs - Windows Universal tutorial].</span></span>  
   
    <span data-ttu-id="db476-178">b.</span><span class="sxs-lookup"><span data-stu-id="db476-178">b.</span></span> <span data-ttu-id="db476-179">Verificare che l'applicazione sia abilitata alla ricezione di notifiche di tipo avviso popup.</span><span class="sxs-lookup"><span data-stu-id="db476-179">Ensure that your application is enabled to receive toast notifications.</span></span>
   
    <span data-ttu-id="db476-180">c.</span><span class="sxs-lookup"><span data-stu-id="db476-180">c.</span></span> <span data-ttu-id="db476-181">Assicurarsi che all'avvio dell'app, dopo aver sostituito *HubName* e *DefaultListenSharedAccessSignature*, venga chiamato il seguente codice di registrazione di Hub di notifica:</span><span class="sxs-lookup"><span data-stu-id="db476-181">Ensure that the following Notification Hubs registration code is being called at the App start up (after replacing the *HubName* and *DefaultListenSharedAccessSignature*:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("[HubName]", "[DefaultListenSharedAccessSignature]");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays the registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

### <a name="running-sample"></a><span data-ttu-id="db476-182">Esecuzione di esempio:</span><span class="sxs-lookup"><span data-stu-id="db476-182">Running sample:</span></span>
1. <span data-ttu-id="db476-183">Assicurarsi che il processo Web venga eseguito correttamente e che sia pianificato per l'esecuzione continua.</span><span class="sxs-lookup"><span data-stu-id="db476-183">Ensure that your WebJob is running successfully and scheduled to "Run Continuously".</span></span>
2. <span data-ttu-id="db476-184">Eseguire **EnterprisePushMobileApp** che avvierà l'app di Windows Store.</span><span class="sxs-lookup"><span data-stu-id="db476-184">Run the **EnterprisePushMobileApp** which will start the Windows Store app.</span></span>
3. <span data-ttu-id="db476-185">Eseguire l'applicazione console **EnterprisePushBackendSystem** che simula il back-end LOB e avvia l'invio di messaggi. Verranno visualizzate notifiche di tipo avviso popup simili alle seguenti:</span><span class="sxs-lookup"><span data-stu-id="db476-185">Run the **EnterprisePushBackendSystem** console application which will simulate the LoB backend and will start sending messages and you should see toast notifications appearing like the following:</span></span>
   
    ![][5]
4. <span data-ttu-id="db476-186">All'inizio i messaggi sono stati inviati ad argomenti del bus di servizio, operazione monitorata da sottoscrizioni del bus di servizio nel processo Web.</span><span class="sxs-lookup"><span data-stu-id="db476-186">The messages were originally sent to Service Bus topics which was being monitored by Service Bus subscriptions in your Web Job.</span></span> <span data-ttu-id="db476-187">Una volta ricevuto un messaggio, è stata creata una notifica che è stata inviata all'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="db476-187">Once a message was received, a notification was created and sent to the mobile app.</span></span> <span data-ttu-id="db476-188">Per confermare l'elaborazione, è possibile esaminare i log del processo Web, selezionando il collegamento Log in relazione al processo Web nel [portale di Azure classico] :</span><span class="sxs-lookup"><span data-stu-id="db476-188">You can look through the WebJob logs to confirm the processing when you go to the Logs link in [Azure Classic Portal] for your Web Job:</span></span>
   
    ![][6]

<!-- Images -->
[1]: ./media/notification-hubs-enterprise-push-architecture/architecture.png
[2]: ./media/notification-hubs-enterprise-push-architecture/WebJobsContextMenu.png
[3]: ./media/notification-hubs-enterprise-push-architecture/PublishAsWebJob.png
[4]: ./media/notification-hubs-enterprise-push-architecture/WebJob.png
[5]: ./media/notification-hubs-enterprise-push-architecture/Notifications.png
[6]: ./media/notification-hubs-enterprise-push-architecture/WebJobsLog.png

<!-- Links -->
<span data-ttu-id="db476-189">[esempi di Hub di notifica]: https://github.com/Azure/azure-notificationhubs-samples</span><span class="sxs-lookup"><span data-stu-id="db476-189">[Notification Hub Samples]: https://github.com/Azure/azure-notificationhubs-samples</span></span>
<span data-ttu-id="db476-190">[Servizi mobili di Azure]: http://azure.microsoft.com/documentation/services/mobile-services/</span><span class="sxs-lookup"><span data-stu-id="db476-190">[Azure Mobile Service]: http://azure.microsoft.com/documentation/services/mobile-services/</span></span>
<span data-ttu-id="db476-191">[bus di servizio di Azure]: http://azure.microsoft.com/documentation/articles/fundamentals-service-bus-hybrid-solutions/</span><span class="sxs-lookup"><span data-stu-id="db476-191">[Azure Service Bus]: http://azure.microsoft.com/documentation/articles/fundamentals-service-bus-hybrid-solutions/</span></span>
<span data-ttu-id="db476-192">[Come usare gli argomenti e le sottoscrizioni del bus di servizio]: http://azure.microsoft.com/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/</span><span class="sxs-lookup"><span data-stu-id="db476-192">[Service Bus Pub/Sub programming]: http://azure.microsoft.com/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/</span></span>
<span data-ttu-id="db476-193">[Web di Azure]: http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/</span><span class="sxs-lookup"><span data-stu-id="db476-193">[Azure WebJob]: http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/</span></span>
<span data-ttu-id="db476-194">[Introduzione ad Hub di notifica - Esercitazione per Windows Universal]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span><span class="sxs-lookup"><span data-stu-id="db476-194">[Notification Hubs - Windows Universal tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span></span>
<span data-ttu-id="db476-195">[portale di Azure classico]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="db476-195">[Azure Classic Portal]: https://manage.windowsazure.com/</span></span>
