---
title: aaaGet avviato con gli argomenti del Bus di servizio di Azure e le sottoscrizioni | Documenti Microsoft
description: Scrivere un'applicazione console C# che usa gli argomenti e le sottoscrizioni di messaggistica del bus di servizio.
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/30/2017
ms.author: sethm
ms.openlocfilehash: 619d602599d97ecff2ded0681a383b19f1a8b7ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-service-bus-topics"></a><span data-ttu-id="67bd5-103">Introduzione agli argomenti del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="67bd5-103">Get started with Service Bus topics</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="67bd5-104">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="67bd5-104">What will be accomplished</span></span>

<span data-ttu-id="67bd5-105">Questa esercitazione sono trattati hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="67bd5-105">This tutorial covers hello following steps:</span></span>

1. <span data-ttu-id="67bd5-106">Creare uno spazio dei nomi Service Bus, utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="67bd5-106">Create a Service Bus namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="67bd5-107">Creare un argomento del Bus di servizio, utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="67bd5-107">Create a Service Bus topic, using hello Azure portal.</span></span>
3. <span data-ttu-id="67bd5-108">Creare un argomento di toothat sottoscrizione Bus di servizio, utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="67bd5-108">Create a Service Bus subscription toothat topic, using hello Azure portal.</span></span>
4. <span data-ttu-id="67bd5-109">Scrivere un toosend di applicazione console come un argomento di toohello di messaggio.</span><span class="sxs-lookup"><span data-stu-id="67bd5-109">Write a console application toosend a message toohello topic.</span></span>
5. <span data-ttu-id="67bd5-110">Scrivere un tooreceive di applicazione console che il messaggio dalla sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="67bd5-110">Write a console application tooreceive that message from hello subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67bd5-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="67bd5-111">Prerequisites</span></span>

1. <span data-ttu-id="67bd5-112">[Visual Studio 2015 o versione successiva](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="67bd5-112">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="67bd5-113">esempi di Hello in questa esercitazione usano Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="67bd5-113">hello examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="67bd5-114">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="67bd5-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="67bd5-115">1. Creare uno spazio dei nomi utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="67bd5-115">1. Create a namespace using hello Azure portal</span></span>

<span data-ttu-id="67bd5-116">Se è già stato creato uno spazio dei nomi di messaggistica del Bus di servizio, passare toohello [creare un argomento tramite il portale di Azure hello](#2-create-a-topic-using-the-azure-portal) sezione.</span><span class="sxs-lookup"><span data-stu-id="67bd5-116">If you have already created a Service Bus Messaging namespace, jump toohello [Create a topic using hello Azure portal](#2-create-a-topic-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-topic-using-hello-azure-portal"></a><span data-ttu-id="67bd5-117">2. Creazione di un argomento tramite hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="67bd5-117">2. Create a topic using hello Azure portal</span></span>

1. <span data-ttu-id="67bd5-118">Accesso toohello [portale di Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="67bd5-118">Log on toohello [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="67bd5-119">Nel riquadro di spostamento a sinistra di hello del portale di hello, fare clic su **Bus di servizio** (se non viene visualizzato **Bus di servizio**, fare clic su **più servizi**).</span><span class="sxs-lookup"><span data-stu-id="67bd5-119">In hello left navigation pane of hello portal, click **Service Bus** (if you don't see **Service Bus**, click **More services**).</span></span>
3. <span data-ttu-id="67bd5-120">Fare clic su spazio dei nomi hello in cui si desidera argomento hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="67bd5-120">Click hello namespace in which you would like toocreate hello topic.</span></span> <span data-ttu-id="67bd5-121">pannello della panoramica Hello dello spazio dei nomi viene visualizzato:</span><span class="sxs-lookup"><span data-stu-id="67bd5-121">hello namespace overview blade appears:</span></span>
   
    ![Creare un argomento][createtopic1]
4. <span data-ttu-id="67bd5-123">In hello **dello spazio dei nomi Service Bus** pannello, fare clic su **argomenti**, quindi fare clic su **Aggiungi argomento**.</span><span class="sxs-lookup"><span data-stu-id="67bd5-123">In hello **Service Bus namespace** blade, click **Topics**, then click **Add topic**.</span></span>
   
    ![Selezionare gli argomenti][createtopic2]
5. <span data-ttu-id="67bd5-125">Immettere un nome per l'argomento hello e deselezionare hello **abilitare il partizionamento** opzione.</span><span class="sxs-lookup"><span data-stu-id="67bd5-125">Enter a name for hello topic, and uncheck hello **Enable partitioning** option.</span></span> <span data-ttu-id="67bd5-126">Lasciare hello altre opzioni con valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="67bd5-126">Leave hello other options with their default values.</span></span>
   
    ![Selezionare Nuovo][createtopic3]
6. <span data-ttu-id="67bd5-128">Nella parte inferiore di hello del pannello hello, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="67bd5-128">At hello bottom of hello blade, click **Create**.</span></span>

## <a name="3-create-a-subscription-toohello-topic"></a><span data-ttu-id="67bd5-129">3. Creazione di un argomento toohello sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="67bd5-129">3. Create a subscription toohello topic</span></span>

1. <span data-ttu-id="67bd5-130">Nel riquadro risorse portale hello, fare clic su spazio dei nomi hello creato nel passaggio 1, quindi fare clic sul nome di argomento hello creato nel passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="67bd5-130">In hello portal resources pane, click hello namespace you created in step 1, then click name of hello topic you created in step 2.</span></span>
2. <span data-ttu-id="67bd5-131">Top hello del riquadro Panoramica hello, fare clic su hello segno più accanto troppo**sottoscrizione** tooadd un argomento toothis di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="67bd5-131">A hello top of hello overview pane, click hello plus sign next too**Subscription** tooadd a subscription toothis topic.</span></span>

    ![Creare la sottoscrizione][createtopic4]

3. <span data-ttu-id="67bd5-133">Immettere un nome per la sottoscrizione di hello.</span><span class="sxs-lookup"><span data-stu-id="67bd5-133">Enter a name for hello subscription.</span></span> <span data-ttu-id="67bd5-134">Lasciare hello altre opzioni con valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="67bd5-134">Leave hello other options with their default values.</span></span>

## <a name="4-send-messages-toohello-topic"></a><span data-ttu-id="67bd5-135">4. Inviare l'argomento toohello messaggi</span><span class="sxs-lookup"><span data-stu-id="67bd5-135">4. Send messages toohello topic</span></span>

<span data-ttu-id="67bd5-136">argomento toohello messaggi toosend è scrivere un'applicazione console c# con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="67bd5-136">toosend messages toohello topic, we write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="67bd5-137">Creare un'applicazione console</span><span class="sxs-lookup"><span data-stu-id="67bd5-137">Create a console application</span></span>

<span data-ttu-id="67bd5-138">Avviare Visual Studio e creare un nuovo progetto **App console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="67bd5-138">Launch Visual Studio and create a new **Console app (.NET Framework)** project.</span></span>

### <a name="add-hello-service-bus-nuget-package"></a><span data-ttu-id="67bd5-139">Aggiungere il pacchetto NuGet di Service Bus hello</span><span class="sxs-lookup"><span data-stu-id="67bd5-139">Add hello Service Bus NuGet package</span></span>

1. <span data-ttu-id="67bd5-140">Fare clic sul progetto hello appena creato e selezionare **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="67bd5-140">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="67bd5-141">Fare clic su hello **Sfoglia** scheda, cercare **Microsoft Azure Service Bus**, quindi selezionare hello **Windowsazure** elemento.</span><span class="sxs-lookup"><span data-stu-id="67bd5-141">Click hello **Browse** tab, search for **Microsoft Azure Service Bus**, and then select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="67bd5-142">Fare clic su **installare** toocomplete hello installazione, quindi chiudere questa finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="67bd5-142">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>
   
    ![Selezionare un pacchetto NuGet][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-topic"></a><span data-ttu-id="67bd5-144">Scrivere alcuni toosend codice un argomento toohello messaggio</span><span class="sxs-lookup"><span data-stu-id="67bd5-144">Write some code toosend a message toohello topic</span></span>

1. <span data-ttu-id="67bd5-145">Aggiungere il seguente hello `using` top toohello istruzione del file Program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="67bd5-145">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="67bd5-146">Aggiungere i seguenti toohello codice hello `Main` metodo.</span><span class="sxs-lookup"><span data-stu-id="67bd5-146">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="67bd5-147">Set hello `connectionString` connessione toohello variabile stringa ottenuto durante la creazione dello spazio dei nomi hello e impostare `topicName` toohello nome utilizzato per la creazione di hello argomento.</span><span class="sxs-lookup"><span data-stu-id="67bd5-147">Set hello `connectionString` variable toohello connection string that you obtained when creating hello namespace, and set `topicName` toohello name that you used when creating hello topic.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="67bd5-148">Ecco l'aspetto che avrà il file Program.cs.</span><span class="sxs-lookup"><span data-stu-id="67bd5-148">Here is what your Program.cs file should look like.</span></span>
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using Microsoft.ServiceBus.Messaging;

    namespace tsend
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";
                var topicName = "<your topic name>";

                var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
                var message = new BrokeredMessage("This is a test message!");

                Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
                Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

                client.Send(message);

                Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. <span data-ttu-id="67bd5-149">Esegui programma hello e verifica hello portale di Azure: fare clic sul nome dell'argomento nello spazio dei nomi hello hello **Panoramica** blade.</span><span class="sxs-lookup"><span data-stu-id="67bd5-149">Run hello program, and check hello Azure portal: click hello name of your topic in hello namespace **Overview** blade.</span></span> <span data-ttu-id="67bd5-150">argomento Hello **Essentials** pannello viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="67bd5-150">hello topic **Essentials** blade is displayed.</span></span> <span data-ttu-id="67bd5-151">In hello delle sottoscrizioni elencate nella parte inferiore di hello della pannello hello, si noti che hello **numero messaggi** valore per ogni sottoscrizione deve essere 1.</span><span class="sxs-lookup"><span data-stu-id="67bd5-151">In hello subscription(s) listed near hello bottom of hello blade, notice that hello **Message Count** value for each subscription should now be 1.</span></span> <span data-ttu-id="67bd5-152">Ogni volta che si esegue l'applicazione mittente hello senza recuperare messaggi hello (come descritto nella sezione successiva hello), questo valore incrementato di 1.</span><span class="sxs-lookup"><span data-stu-id="67bd5-152">Each time you run hello sender application without retrieving hello messages (as described in hello next section), this value increases by 1.</span></span> <span data-ttu-id="67bd5-153">Si noti inoltre che dimensioni correnti di hello di hello incrementi di argomento hello **corrente** valore hello **Essentials** pannello ogni volta che l'applicazione hello aggiunge una messaggio toohello argomento o sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="67bd5-153">Also note that hello current size of hello topic increments hello **Current** value on hello **Essentials** blade each time hello app adds a message toohello topic/subscription.</span></span>
   
      ![Dimensioni dei messaggi][topic-message]

## <a name="5-receive-messages-from-hello-subscription"></a><span data-ttu-id="67bd5-155">5. Ricevere messaggi dalla sottoscrizione hello</span><span class="sxs-lookup"><span data-stu-id="67bd5-155">5. Receive messages from hello subscription</span></span>

1. <span data-ttu-id="67bd5-156">tooreceive hello o messaggi appena inviato, creare una nuova applicazione console e aggiungere un pacchetto NuGet di Service Bus toohello riferimento, applicazione mittente precedente toohello simile.</span><span class="sxs-lookup"><span data-stu-id="67bd5-156">tooreceive hello message or messages you just sent, create a new console application and add a reference toohello Service Bus NuGet package, similar toohello previous sender application.</span></span>
2. <span data-ttu-id="67bd5-157">Aggiungere il seguente hello `using` top toohello istruzione del file Program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="67bd5-157">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="67bd5-158">Aggiungere i seguenti toohello codice hello `Main` metodo.</span><span class="sxs-lookup"><span data-stu-id="67bd5-158">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="67bd5-159">Set hello `connectionString` connessione toohello variabile stringa ottenuto durante la creazione dello spazio dei nomi hello e impostare `topicName` toohello nome utilizzato per la creazione di hello argomento.</span><span class="sxs-lookup"><span data-stu-id="67bd5-159">Set hello `connectionString` variable toohello connection string you obtained when creating hello namespace, and set `topicName` toohello name that you used when creating hello topic.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="67bd5-160">Ecco l'aspetto che avrà il file Program.cs:</span><span class="sxs-lookup"><span data-stu-id="67bd5-160">Here is what your Program.cs file should look like:</span></span>
   
    ```csharp
    using System;
    using Microsoft.ServiceBus.Messaging;
   
    namespace GettingStartedWithTopics
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";;
          var topicName = "<your topic name>";
   
          var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
          client.OnMessage(message =>
          {
            Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
            Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
          });

          Console.WriteLine("Press ENTER tooexit program");   
          Console.ReadLine();
        }
      }
    }
    ```
4. <span data-ttu-id="67bd5-161">Eseguire il programma hello e controllare di nuovo portale hello.</span><span class="sxs-lookup"><span data-stu-id="67bd5-161">Run hello program, and check hello portal again.</span></span> <span data-ttu-id="67bd5-162">Si noti che hello **numero messaggi** e **corrente** ora sono valori 0.</span><span class="sxs-lookup"><span data-stu-id="67bd5-162">Notice that hello **Message Count** and **Current** values are now 0.</span></span>
   
    ![Lunghezza argomento][topic-message-receive]

<span data-ttu-id="67bd5-164">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="67bd5-164">Congratulations!</span></span> <span data-ttu-id="67bd5-165">Sono stati creati un argomento e una sottoscrizione ed è stato inviato un messaggio che è stato quindi ricevuto.</span><span class="sxs-lookup"><span data-stu-id="67bd5-165">You have now created a topic and subscription, sent a message, and received that message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67bd5-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="67bd5-166">Next steps</span></span>

<span data-ttu-id="67bd5-167">Estrarre il nostro [repository GitHub con campioni](https://github.com/Azure/azure-service-bus/tree/master/samples) che illustrano alcune delle più avanzate funzionalità di messaggistica del Bus di servizio hello.</span><span class="sxs-lookup"><span data-stu-id="67bd5-167">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of hello more advanced features of Service Bus messaging.</span></span>

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/nuget-package.png
[topic-message]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message.png
[topic-message-receive]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message-receive.png
[createtopic1]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic1.png
[createtopic2]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic2.png
[createtopic3]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic3.png
[createtopic4]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic4.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
[azure-portal]: https://portal.azure.com
