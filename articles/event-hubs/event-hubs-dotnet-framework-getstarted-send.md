---
title: Inviare eventi a Hub eventi di Azure usando .NET Framework | Documentazione Microsoft
description: Iniziare a inviare eventi a Hub eventi usando .NET Framework
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4974bd3-2a79-48a1-aa3b-8ee2d6655b28
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/12/2017
ms.author: sethm
ms.openlocfilehash: 4eb0e7bcc14722010121c2a5945509d6ed736f4f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="send-events-to-azure-event-hubs-using-the-net-framework"></a><span data-ttu-id="fa6c2-103">Inviare eventi a Hub eventi di Azure usando .NET Framework</span><span class="sxs-lookup"><span data-stu-id="fa6c2-103">Send events to Azure Event Hubs using the .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="fa6c2-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="fa6c2-104">Introduction</span></span>

<span data-ttu-id="fa6c2-105">Hub eventi è un servizio che consente di elaborare grandi quantità di dati di telemetria sugli eventi da applicazioni e dispositivi connessi.</span><span class="sxs-lookup"><span data-stu-id="fa6c2-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="fa6c2-106">Dopo aver raccolto i dati in Hub eventi, è possibile archiviarli usando un cluster di archiviazione o trasformarli usando un provider di analisi in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="fa6c2-106">After you collect data into Event Hubs, you can store the data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="fa6c2-107">Questa funzionalità di elaborazione e raccolta di eventi su vasta scala rappresenta un componente chiave delle moderne architetture di applicazioni, tra cui Internet delle cose (IoT).</span><span class="sxs-lookup"><span data-stu-id="fa6c2-107">This large-scale event collection and processing capability is a key component of modern application architectures including the Internet of Things (IoT).</span></span>

<span data-ttu-id="fa6c2-108">Questa esercitazione illustra come usare il [portale di Azure](https://portal.azure.com) per creare un hub eventi.</span><span class="sxs-lookup"><span data-stu-id="fa6c2-108">This tutorial shows how to use the [Azure portal](https://portal.azure.com) to create an event hub.</span></span> <span data-ttu-id="fa6c2-109">Descrive anche come inviare eventi a un hub eventi usando un'applicazione console scritta in C# con .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="fa6c2-109">It also shows how to send events to an event hub using a console application written in C# using the .NET Framework.</span></span> <span data-ttu-id="fa6c2-110">Per ricevere eventi usando .NET Framework, vedere l'articolo [Receive events using the .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) (Ricevere eventi usando .NET Framework) o fare clic sul linguaggio di ricezione appropriato nel sommario a sinistra.</span><span class="sxs-lookup"><span data-stu-id="fa6c2-110">To receive events using the .NET Framework, see the [Receive events using the .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) article, or click the appropriate receiving language in the left-hand table of contents.</span></span>

<span data-ttu-id="fa6c2-111">Per completare questa esercitazione è necessario soddisfare i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="fa6c2-111">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="fa6c2-112">[Microsoft Visual Studio 2015 o versione successiva](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="fa6c2-112">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="fa6c2-113">Gli screenshot in questa esercitazione illustrano Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="fa6c2-113">The screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="fa6c2-114">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="fa6c2-114">An active Azure account.</span></span> <span data-ttu-id="fa6c2-115">Se non si ha un account, è possibile crearne uno gratuito in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="fa6c2-115">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="fa6c2-116">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="fa6c2-116">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="fa6c2-117">Creare uno spazio dei nomi di Hub eventi e un hub eventi</span><span class="sxs-lookup"><span data-stu-id="fa6c2-117">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="fa6c2-118">Il primo passaggio consiste nell'usare il [portale di Azure](https://portal.azure.com) per creare uno spazio dei nomi di tipo Hub eventi e ottenere le credenziali di gestione necessarie all'applicazione per comunicare con l'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="fa6c2-118">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace of type Event Hubs, and obtain the management credentials your application needs to communicate with the event hub.</span></span> <span data-ttu-id="fa6c2-119">Per creare uno spazio dei nomi e un hub eventi, seguire la procedura descritta in [questo articolo](event-hubs-create.md) e quindi procedere con i passaggi seguenti di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="fa6c2-119">To create a namespace and event hub, follow the procedure in [this article](event-hubs-create.md), then proceed with the following steps in this tutorial.</span></span>

## <a name="create-a-sender-console-application"></a><span data-ttu-id="fa6c2-120">Creare un'applicazione console per il mittente</span><span class="sxs-lookup"><span data-stu-id="fa6c2-120">Create a sender console application</span></span>

<span data-ttu-id="fa6c2-121">In questa sezione si scriverà un'app console Windows che invia eventi all'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="fa6c2-121">In this section, you'll write a Windows console app that sends events to your event hub.</span></span>

1. <span data-ttu-id="fa6c2-122">In Visual Studio creare un nuovo progetto di app desktop di Visual C# usando il modello di progetto **Applicazione console** .</span><span class="sxs-lookup"><span data-stu-id="fa6c2-122">In Visual Studio, create a new Visual C# Desktop App project using the **Console Application** project template.</span></span> <span data-ttu-id="fa6c2-123">Assegnare al progetto il nome **Sender**.</span><span class="sxs-lookup"><span data-stu-id="fa6c2-123">Name the project **Sender**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp1.png)
2. <span data-ttu-id="fa6c2-124">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto **Sender**, quindi scegliere **Gestisci pacchetti NuGet per la soluzione**.</span><span class="sxs-lookup"><span data-stu-id="fa6c2-124">In Solution Explorer, right-click the **Sender** project, and then click **Manage NuGet Packages for Solution**.</span></span> 
3. <span data-ttu-id="fa6c2-125">Fare clic sulla scheda **Sfoglia** e quindi cercare `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="fa6c2-125">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="fa6c2-126">Fare clic su **Installa**e accettare le condizioni per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="fa6c2-126">Click **Install**, and accept the terms of use.</span></span> 
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp2.png)
   
    <span data-ttu-id="fa6c2-127">Visual Studio scarica e installa il [pacchetto NuGet delle librerie del bus di servizio di Azure](https://www.nuget.org/packages/WindowsAzure.ServiceBus)e aggiunge un riferimento al pacchetto.</span><span class="sxs-lookup"><span data-stu-id="fa6c2-127">Visual Studio downloads, installs, and adds a reference to the [Azure Service Bus library NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span></span>
4. <span data-ttu-id="fa6c2-128">Aggiungere le istruzione `using` seguenti all'inizio del file **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="fa6c2-128">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
  ```csharp
  using System.Threading;
  using Microsoft.ServiceBus.Messaging;
  ```
5. <span data-ttu-id="fa6c2-129">Aggiungere i campi seguenti alla classe **Program**, sostituendo i valori segnaposto con il nome dell'hub eventi creato nella sezione precedente e la stringa di connessione a livello di spazio dei nomi salvata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="fa6c2-129">Add the following fields to the **Program** class, substituting the placeholder values with the name of the event hub you created in the previous section, and the namespace-level connection string you saved previously.</span></span>
   
  ```csharp
  static string eventHubName = "{Event Hub name}";
  static string connectionString = "{send connection string}";
  ```
6. <span data-ttu-id="fa6c2-130">Aggiungere il metodo seguente alla classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="fa6c2-130">Add the following method to the **Program** class:</span></span>
   
  ```csharp
  static void SendingRandomMessages()
  {
      var eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, eventHubName);
      while (true)
      {
          try
          {
              var message = Guid.NewGuid().ToString();
              Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, message);
              eventHubClient.Send(new EventData(Encoding.UTF8.GetBytes(message)));
          }
          catch (Exception exception)
          {
              Console.ForegroundColor = ConsoleColor.Red;
              Console.WriteLine("{0} > Exception: {1}", DateTime.Now, exception.Message);
              Console.ResetColor();
          }
   
          Thread.Sleep(200);
      }
  }
  ```
   
  <span data-ttu-id="fa6c2-131">Questo metodo invia continuamente eventi all'hub eventi con un ritardo di 200 millisecondi.</span><span class="sxs-lookup"><span data-stu-id="fa6c2-131">This method continuously sends events to your event hub with a 200-ms delay.</span></span>
7. <span data-ttu-id="fa6c2-132">Aggiungere infine le righe seguenti al metodo **Main** :</span><span class="sxs-lookup"><span data-stu-id="fa6c2-132">Finally, add the following lines to the **Main** method:</span></span>
   
  ```csharp
  Console.WriteLine("Press Ctrl-C to stop the sender process");
  Console.WriteLine("Press Enter to start now");
  Console.ReadLine();
  SendingRandomMessages();
  ```
8. <span data-ttu-id="fa6c2-133">Eseguire il programma e assicurarsi che non siano presenti errori.</span><span class="sxs-lookup"><span data-stu-id="fa6c2-133">Run the program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="fa6c2-134">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="fa6c2-134">Congratulations!</span></span> <span data-ttu-id="fa6c2-135">Sono stati inviati messaggi a un hub eventi.</span><span class="sxs-lookup"><span data-stu-id="fa6c2-135">You have now sent messages to an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa6c2-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fa6c2-136">Next steps</span></span>
<span data-ttu-id="fa6c2-137">Ora che è stata creata un'applicazione funzionante che crea un hub eventi e invia dati, è possibile passare agli scenari seguenti:</span><span class="sxs-lookup"><span data-stu-id="fa6c2-137">Now that you've built a working application that creates an event hub and sends data, you can move on to the following scenarios:</span></span>

* <span data-ttu-id="fa6c2-138">[Receive events using the Event Processor Host](event-hubs-dotnet-framework-getstarted-receive-eph.md) (Ricevere eventi usando l'host processore di eventi)</span><span class="sxs-lookup"><span data-stu-id="fa6c2-138">[Receive events using the Event Processor Host](event-hubs-dotnet-framework-getstarted-receive-eph.md)</span></span>
* <span data-ttu-id="fa6c2-139">[Event Processor Host reference](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost) (Informazioni di riferimento sull'host processore di eventi)</span><span class="sxs-lookup"><span data-stu-id="fa6c2-139">[Event Processor Host reference](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)</span></span>
* [<span data-ttu-id="fa6c2-140">Panoramica di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="fa6c2-140">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

