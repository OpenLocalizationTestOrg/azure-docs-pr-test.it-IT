---
title: Introduzione alle code del bus di servizio di Azure | Microsoft Docs
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
ms.openlocfilehash: 99a377db6341d90d263b98e14227db61dd9beabd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-service-bus-queues"></a><span data-ttu-id="ce1f8-103">Introduzione alle code del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="ce1f8-103">Get started with Service Bus queues</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="ce1f8-104">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="ce1f8-104">What will be accomplished</span></span>
<span data-ttu-id="ce1f8-105">Questa esercitazione illustra i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ce1f8-105">This tutorial covers the following steps:</span></span>

1. <span data-ttu-id="ce1f8-106">Creare uno spazio dei nomi del bus di servizio usando il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ce1f8-106">Create a Service Bus namespace, using the Azure portal.</span></span>
2. <span data-ttu-id="ce1f8-107">Creare una coda del bus di servizio usando il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ce1f8-107">Create a Service Bus queue, using the Azure portal.</span></span>
3. <span data-ttu-id="ce1f8-108">Scrivere un'applicazione console per inviare un messaggio.</span><span class="sxs-lookup"><span data-stu-id="ce1f8-108">Write a console application to send a message.</span></span>
4. <span data-ttu-id="ce1f8-109">Scrivere un'applicazione console per ricevere i messaggi inviati nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="ce1f8-109">Write a console application to receive the messages sent in the previous step.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce1f8-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ce1f8-110">Prerequisites</span></span>
1. <span data-ttu-id="ce1f8-111">[Visual Studio 2015 o versione successiva](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="ce1f8-111">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="ce1f8-112">Negli esempi di questa esercitazione viene usato Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="ce1f8-112">The examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="ce1f8-113">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ce1f8-113">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a><span data-ttu-id="ce1f8-114">1. Creare uno spazio dei nomi tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ce1f8-114">1. Create a namespace using the Azure portal</span></span>
<span data-ttu-id="ce1f8-115">Se è già stato creato uno spazio dei nomi di messaggistica del bus di servizio, passare alla sezione [Creare una coda usando il portale di Azure](#2-create-a-queue-using-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="ce1f8-115">If you've already created a Service Bus Messaging namespace, jump to the [Create a queue using the Azure portal](#2-create-a-queue-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-queue-using-the-azure-portal"></a><span data-ttu-id="ce1f8-116">2. Creare una coda usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ce1f8-116">2. Create a queue using the Azure portal</span></span>
<span data-ttu-id="ce1f8-117">Se è già stata creata una coda del bus di servizio, passare alla sezione [Inviare messaggi alla coda](#3-send-messages-to-the-queue).</span><span class="sxs-lookup"><span data-stu-id="ce1f8-117">If you have already created a Service Bus queue, jump to the [Send messages to the queue](#3-send-messages-to-the-queue) section.</span></span>

[!INCLUDE [service-bus-create-queue-portal](../../includes/service-bus-create-queue-portal.md)]

## <a name="3-send-messages-to-the-queue"></a><span data-ttu-id="ce1f8-118">3. Inviare messaggi alla coda</span><span class="sxs-lookup"><span data-stu-id="ce1f8-118">3. Send messages to the queue</span></span>
<span data-ttu-id="ce1f8-119">Per inviare messaggi alla coda, si scrive un'applicazione console C# in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ce1f8-119">To send messages to the queue, we write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="ce1f8-120">Creare un'applicazione console</span><span class="sxs-lookup"><span data-stu-id="ce1f8-120">Create a console application</span></span>

<span data-ttu-id="ce1f8-121">Avviare Visual Studio e creare un nuovo progetto **App console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="ce1f8-121">Launch Visual Studio and create a new **Console app (.NET Framework)** project.</span></span>

### <a name="add-the-service-bus-nuget-package"></a><span data-ttu-id="ce1f8-122">Aggiungere il pacchetto NuGet del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="ce1f8-122">Add the Service Bus NuGet package</span></span>
1. <span data-ttu-id="ce1f8-123">Fare clic con il pulsante destro del mouse sul progetto appena creato e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ce1f8-123">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="ce1f8-124">Fare clic sulla scheda **Esplora**, cercare **Bus di servizio di Microsoft Azure** e quindi selezionare l'elemento **WindowsAzure.ServiceBus**.</span><span class="sxs-lookup"><span data-stu-id="ce1f8-124">Click the **Browse** tab, search for **Microsoft Azure Service Bus**, and then select the **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="ce1f8-125">Fare clic su **Installa** per completare l'installazione, quindi chiudere questa finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="ce1f8-125">Click **Install** to complete the installation, then close this dialog box.</span></span>
   
    ![Selezionare un pacchetto NuGet][nuget-pkg]

### <a name="write-some-code-to-send-a-message-to-the-queue"></a><span data-ttu-id="ce1f8-127">Scrivere il codice per inviare un messaggio alla coda</span><span class="sxs-lookup"><span data-stu-id="ce1f8-127">Write some code to send a message to the queue</span></span>
1. <span data-ttu-id="ce1f8-128">Aggiungere l'istruzione `using` seguente all'inizio del file Program.cs.</span><span class="sxs-lookup"><span data-stu-id="ce1f8-128">Add the following `using` statement to the top of the Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="ce1f8-129">Aggiungere il codice seguente al metodo `Main` .</span><span class="sxs-lookup"><span data-stu-id="ce1f8-129">Add the following code to the `Main` method.</span></span> <span data-ttu-id="ce1f8-130">Impostare la variabile `connectionString` sulla stessa stringa di connessione ottenuta al momento della creazione dello spazio dei nomi e impostare `queueName` sul nome della coda usato durante la creazione della coda.</span><span class="sxs-lookup"><span data-stu-id="ce1f8-130">Set the `connectionString` variable to the connection string that you obtained when creating the namespace, and set `queueName` to the queue name that you used when creating the queue.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER to exit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="ce1f8-131">Ecco l'aspetto che avrà il file Program.cs.</span><span class="sxs-lookup"><span data-stu-id="ce1f8-131">Here is what your Program.cs file should look like.</span></span>
   
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

                Console.WriteLine("Message successfully sent! Press ENTER to exit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. <span data-ttu-id="ce1f8-132">Eseguire il programma e controllare il portale di Azure: fare clic sul nome della coda nel pannello **Panoramica** dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="ce1f8-132">Run the program, and check the Azure portal: click the name of your queue in the namespace **Overview** blade.</span></span> <span data-ttu-id="ce1f8-133">Viene visualizzato il pannello **Informazioni di base** della coda.</span><span class="sxs-lookup"><span data-stu-id="ce1f8-133">The queue **Essentials** blade is displayed.</span></span> <span data-ttu-id="ce1f8-134">Si noti che ora il valore di **Numero di messaggi attivi** è 1.</span><span class="sxs-lookup"><span data-stu-id="ce1f8-134">Notice that the **Active Message Count** value should now be 1.</span></span> <span data-ttu-id="ce1f8-135">Ogni volta che si avvia l'applicazione mittente senza recuperare i messaggi, questo valore aumenta di 1.</span><span class="sxs-lookup"><span data-stu-id="ce1f8-135">Each time you run the sender application without retrieving the messages, this value increases by 1.</span></span> <span data-ttu-id="ce1f8-136">Tenere anche presente che la dimensione corrente della coda aumenta ogni volta che l'app aggiunge un messaggio alla coda.</span><span class="sxs-lookup"><span data-stu-id="ce1f8-136">Also note that the current size of the queue increments each time the app adds a message to the queue.</span></span>
   
      ![Dimensioni dei messaggi][queue-message]

## <a name="4-receive-messages-from-the-queue"></a><span data-ttu-id="ce1f8-138">4. Ricezione di messaggi dalla coda</span><span class="sxs-lookup"><span data-stu-id="ce1f8-138">4. Receive messages from the queue</span></span>

1. <span data-ttu-id="ce1f8-139">Per ricevere i messaggi inviati, creare una nuova applicazione console e aggiungere un riferimento al pacchetto NuGet del bus di servizio, come per l'applicazione mittente precedente.</span><span class="sxs-lookup"><span data-stu-id="ce1f8-139">To receive the messages you just sent, create a new console application and add a reference to the Service Bus NuGet package, similar to the previous sender application.</span></span>
2. <span data-ttu-id="ce1f8-140">Aggiungere l'istruzione `using` seguente all'inizio del file Program.cs.</span><span class="sxs-lookup"><span data-stu-id="ce1f8-140">Add the following `using` statement to the top of the Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="ce1f8-141">Aggiungere il codice seguente al metodo `Main` .</span><span class="sxs-lookup"><span data-stu-id="ce1f8-141">Add the following code to the `Main` method.</span></span> <span data-ttu-id="ce1f8-142">Impostare la variabile `connectionString` sulla stessa stringa di connessione ottenuta al momento della creazione dello spazio dei nomi e impostare `queueName` sul nome della coda usato durante la creazione della coda.</span><span class="sxs-lookup"><span data-stu-id="ce1f8-142">Set the `connectionString` variable to the connection string that was obtained when creating the namespace, and set `queueName` to the queue name that you used when creating the queue.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER to exit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="ce1f8-143">Ecco l'aspetto che avrà il file Program.cs:</span><span class="sxs-lookup"><span data-stu-id="ce1f8-143">Here is what your Program.cs file should look like:</span></span>
   
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

          Console.WriteLine("Press ENTER to exit program");   
          Console.ReadLine();
        }
      }
    }
    ```
4. <span data-ttu-id="ce1f8-144">Eseguire il programma e verificare di nuovo il portale.</span><span class="sxs-lookup"><span data-stu-id="ce1f8-144">Run the program, and check the portal again.</span></span> <span data-ttu-id="ce1f8-145">Si noti che ora i valori di **Numero di messaggi attivi** e di **Corrente** sono pari a 0.</span><span class="sxs-lookup"><span data-stu-id="ce1f8-145">Notice that the **Active Message Count** and **Current** values are now 0.</span></span>
   
    ![Lunghezza coda][queue-message-receive]

<span data-ttu-id="ce1f8-147">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="ce1f8-147">Congratulations!</span></span> <span data-ttu-id="ce1f8-148">È stata creata una coda ed è stato inviato e ricevuto un messaggio.</span><span class="sxs-lookup"><span data-stu-id="ce1f8-148">You have now created a queue, sent a message, and received a message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce1f8-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ce1f8-149">Next steps</span></span>

<span data-ttu-id="ce1f8-150">Vedere il [repository GitHub con esempi](https://github.com/Azure/azure-service-bus/tree/master/samples) che illustrano alcune delle funzionalità più avanzate della messaggistica del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="ce1f8-150">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of the more advanced features of Service Bus messaging.</span></span>

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-get-started-with-queues/nuget-package.png
[queue-message]: ./media/service-bus-dotnet-get-started-with-queues/queue-message.png
[queue-message-receive]: ./media/service-bus-dotnet-get-started-with-queues/queue-message-receive.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
