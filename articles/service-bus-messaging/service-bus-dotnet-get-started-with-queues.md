---
title: aaaGet avviato con le code di Service Bus di Azure | Documenti Microsoft
description: Scrivere un'applicazione console C# che usa le code di messaggistica del bus di servizio.
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 68a34c00-5600-43f6-bbcc-fea599d500da
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/26/2017
ms.author: sethm
ms.openlocfilehash: eaa362ab0eabd2427977398c1deab5dc00105ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-service-bus-queues"></a><span data-ttu-id="c649c-103">Introduzione alle code del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="c649c-103">Get started with Service Bus queues</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="c649c-104">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="c649c-104">What will be accomplished</span></span>
<span data-ttu-id="c649c-105">Questa esercitazione sono trattati hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c649c-105">This tutorial covers hello following steps:</span></span>

1. <span data-ttu-id="c649c-106">Creare uno spazio dei nomi Service Bus, utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c649c-106">Create a Service Bus namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="c649c-107">Creare una coda di Service Bus, utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c649c-107">Create a Service Bus queue, using hello Azure portal.</span></span>
3. <span data-ttu-id="c649c-108">Scrivere un messaggio a un toosend di applicazione console.</span><span class="sxs-lookup"><span data-stu-id="c649c-108">Write a console application toosend a message.</span></span>
4. <span data-ttu-id="c649c-109">Scrivere un hello tooreceive di applicazione console messaggi inviati nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="c649c-109">Write a console application tooreceive hello messages sent in hello previous step.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c649c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c649c-110">Prerequisites</span></span>
1. <span data-ttu-id="c649c-111">[Visual Studio 2015 o versione successiva](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="c649c-111">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="c649c-112">esempi di Hello in questa esercitazione usano Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="c649c-112">hello examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="c649c-113">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c649c-113">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="c649c-114">1. Creare uno spazio dei nomi utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c649c-114">1. Create a namespace using hello Azure portal</span></span>
<span data-ttu-id="c649c-115">Se è già stato creato uno spazio dei nomi di messaggistica del Bus di servizio, passare toohello [creare una coda utilizzando il portale di Azure hello](#2-create-a-queue-using-the-azure-portal) sezione.</span><span class="sxs-lookup"><span data-stu-id="c649c-115">If you've already created a Service Bus Messaging namespace, jump toohello [Create a queue using hello Azure portal](#2-create-a-queue-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-queue-using-hello-azure-portal"></a><span data-ttu-id="c649c-116">2. Creare una coda utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c649c-116">2. Create a queue using hello Azure portal</span></span>
<span data-ttu-id="c649c-117">Se è stato già creato una coda del Bus di servizio, passare toohello [coda di invio messaggi toohello](#3-send-messages-to-the-queue) sezione.</span><span class="sxs-lookup"><span data-stu-id="c649c-117">If you have already created a Service Bus queue, jump toohello [Send messages toohello queue](#3-send-messages-to-the-queue) section.</span></span>

[!INCLUDE [service-bus-create-queue-portal](../../includes/service-bus-create-queue-portal.md)]

## <a name="3-send-messages-toohello-queue"></a><span data-ttu-id="c649c-118">3. Messaggi toohello coda di invio</span><span class="sxs-lookup"><span data-stu-id="c649c-118">3. Send messages toohello queue</span></span>
<span data-ttu-id="c649c-119">coda di toohello toosend messaggi, è scrivere un'applicazione console c# con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c649c-119">toosend messages toohello queue, we write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="c649c-120">Creare un'applicazione console</span><span class="sxs-lookup"><span data-stu-id="c649c-120">Create a console application</span></span>

<span data-ttu-id="c649c-121">Avviare Visual Studio e creare un nuovo progetto **App console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="c649c-121">Launch Visual Studio and create a new **Console app (.NET Framework)** project.</span></span>

### <a name="add-hello-service-bus-nuget-package"></a><span data-ttu-id="c649c-122">Aggiungere il pacchetto NuGet di Service Bus hello</span><span class="sxs-lookup"><span data-stu-id="c649c-122">Add hello Service Bus NuGet package</span></span>
1. <span data-ttu-id="c649c-123">Fare clic sul progetto hello appena creato e selezionare **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="c649c-123">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="c649c-124">Fare clic su hello **Sfoglia** scheda, cercare **Microsoft Azure Service Bus**, quindi selezionare hello **Windowsazure** elemento.</span><span class="sxs-lookup"><span data-stu-id="c649c-124">Click hello **Browse** tab, search for **Microsoft Azure Service Bus**, and then select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="c649c-125">Fare clic su **installare** toocomplete hello installazione, quindi chiudere questa finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="c649c-125">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>
   
    ![Selezionare un pacchetto NuGet][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-queue"></a><span data-ttu-id="c649c-127">Scrittura di una coda di messaggi toohello alcuni toosend di codice</span><span class="sxs-lookup"><span data-stu-id="c649c-127">Write some code toosend a message toohello queue</span></span>
1. <span data-ttu-id="c649c-128">Aggiungere il seguente hello `using` top toohello istruzione del file Program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="c649c-128">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="c649c-129">Aggiungere i seguenti toohello codice hello `Main` metodo.</span><span class="sxs-lookup"><span data-stu-id="c649c-129">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="c649c-130">Set hello `connectionString` connessione toohello variabile stringa ottenuto durante la creazione dello spazio dei nomi hello e impostare `queueName` toohello della coda utilizzata durante la creazione della coda di hello.</span><span class="sxs-lookup"><span data-stu-id="c649c-130">Set hello `connectionString` variable toohello connection string that you obtained when creating hello namespace, and set `queueName` toohello queue name that you used when creating hello queue.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="c649c-131">Ecco l'aspetto che avrà il file Program.cs.</span><span class="sxs-lookup"><span data-stu-id="c649c-131">Here is what your Program.cs file should look like.</span></span>
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using Microsoft.ServiceBus.Messaging;

    namespace qsend
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";
                var queueName = "<your queue name>";

                var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
                var message = new BrokeredMessage("This is a test message!");

                Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

                client.Send(message);

                Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. <span data-ttu-id="c649c-132">Esegui programma hello e verifica hello portale di Azure: fare clic sul nome della coda nello spazio dei nomi hello hello **Panoramica** blade.</span><span class="sxs-lookup"><span data-stu-id="c649c-132">Run hello program, and check hello Azure portal: click hello name of your queue in hello namespace **Overview** blade.</span></span> <span data-ttu-id="c649c-133">coda Hello **Essentials** pannello viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="c649c-133">hello queue **Essentials** blade is displayed.</span></span> <span data-ttu-id="c649c-134">Si noti che hello **il numero di messaggi attivi** valore dovrebbe essere 1.</span><span class="sxs-lookup"><span data-stu-id="c649c-134">Notice that hello **Active Message Count** value should now be 1.</span></span> <span data-ttu-id="c649c-135">Ogni volta che si esegue l'applicazione mittente hello senza recuperare i messaggi hello, questo valore incrementato di 1.</span><span class="sxs-lookup"><span data-stu-id="c649c-135">Each time you run hello sender application without retrieving hello messages, this value increases by 1.</span></span> <span data-ttu-id="c649c-136">Si noti che dimensioni correnti di hello della coda di hello viene incrementato a ogni applicazione hello ora aggiunge inoltre una coda di messaggi toohello.</span><span class="sxs-lookup"><span data-stu-id="c649c-136">Also note that hello current size of hello queue increments each time hello app adds a message toohello queue.</span></span>
   
      ![Dimensioni dei messaggi][queue-message]

## <a name="4-receive-messages-from-hello-queue"></a><span data-ttu-id="c649c-138">4. Ricevere messaggi dalla coda hello</span><span class="sxs-lookup"><span data-stu-id="c649c-138">4. Receive messages from hello queue</span></span>

1. <span data-ttu-id="c649c-139">messaggi hello tooreceive appena inviato, creare una nuova applicazione console e aggiungere un pacchetto NuGet di Service Bus toohello riferimento, applicazione mittente precedente toohello simile.</span><span class="sxs-lookup"><span data-stu-id="c649c-139">tooreceive hello messages you just sent, create a new console application and add a reference toohello Service Bus NuGet package, similar toohello previous sender application.</span></span>
2. <span data-ttu-id="c649c-140">Aggiungere il seguente hello `using` top toohello istruzione del file Program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="c649c-140">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="c649c-141">Aggiungere i seguenti toohello codice hello `Main` metodo.</span><span class="sxs-lookup"><span data-stu-id="c649c-141">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="c649c-142">Set hello `connectionString` toohello variabile stringa di connessione è stato ottenuto durante la creazione dello spazio dei nomi hello e impostare `queueName` toohello della coda utilizzata durante la creazione della coda di hello.</span><span class="sxs-lookup"><span data-stu-id="c649c-142">Set hello `connectionString` variable toohello connection string that was obtained when creating hello namespace, and set `queueName` toohello queue name that you used when creating hello queue.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="c649c-143">Ecco l'aspetto che avrà il file Program.cs:</span><span class="sxs-lookup"><span data-stu-id="c649c-143">Here is what your Program.cs file should look like:</span></span>
   
    ```csharp
    using System;
    using Microsoft.ServiceBus.Messaging;
   
    namespace GettingStartedWithQueues
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";;
          var queueName = "<your queue name>";
   
          var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
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
4. <span data-ttu-id="c649c-144">Eseguire il programma hello e controllare di nuovo portale hello.</span><span class="sxs-lookup"><span data-stu-id="c649c-144">Run hello program, and check hello portal again.</span></span> <span data-ttu-id="c649c-145">Si noti che hello **il numero di messaggi attivi** e **corrente** ora sono valori 0.</span><span class="sxs-lookup"><span data-stu-id="c649c-145">Notice that hello **Active Message Count** and **Current** values are now 0.</span></span>
   
    ![Lunghezza coda][queue-message-receive]

<span data-ttu-id="c649c-147">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="c649c-147">Congratulations!</span></span> <span data-ttu-id="c649c-148">È stata creata una coda ed è stato inviato e ricevuto un messaggio.</span><span class="sxs-lookup"><span data-stu-id="c649c-148">You have now created a queue, sent a message, and received a message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c649c-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c649c-149">Next steps</span></span>

<span data-ttu-id="c649c-150">Estrarre il nostro [repository GitHub con campioni](https://github.com/Azure/azure-service-bus/tree/master/samples) che illustrano alcune delle più avanzate funzionalità di messaggistica del Bus di servizio hello.</span><span class="sxs-lookup"><span data-stu-id="c649c-150">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of hello more advanced features of Service Bus messaging.</span></span>

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-get-started-with-queues/nuget-package.png
[queue-message]: ./media/service-bus-dotnet-get-started-with-queues/queue-message.png
[queue-message-receive]: ./media/service-bus-dotnet-get-started-with-queues/queue-message-receive.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
