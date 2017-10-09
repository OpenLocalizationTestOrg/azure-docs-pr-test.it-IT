---
title: gli hub di eventi di aaaSend tooAzure eventi usando hello .NET Framework | Documenti Microsoft
description: Iniziare l'invio di eventi tooEvent hub utilizzando hello .NET Framework
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
ms.openlocfilehash: 05514546a6094096e4a3c800db058190076de80a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-hello-net-framework"></a><span data-ttu-id="f9503-103">Inviare gli eventi di hub di eventi tooAzure utilizzando hello .NET Framework</span><span class="sxs-lookup"><span data-stu-id="f9503-103">Send events tooAzure Event Hubs using hello .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="f9503-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="f9503-104">Introduction</span></span>

<span data-ttu-id="f9503-105">Hub eventi è un servizio che consente di elaborare grandi quantità di dati di telemetria sugli eventi da applicazioni e dispositivi connessi.</span><span class="sxs-lookup"><span data-stu-id="f9503-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="f9503-106">Dopo aver raccolto i dati in hub eventi, è possibile archiviare i dati di hello utilizzando un cluster di archiviazione o trasformare tramite un provider analitica in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="f9503-106">After you collect data into Event Hubs, you can store hello data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="f9503-107">Questa funzionalità di raccolta e l'elaborazione di eventi su larga scala è un componente fondamentale di architetture di applicazioni moderne inclusi hello Internet delle cose (IoT).</span><span class="sxs-lookup"><span data-stu-id="f9503-107">This large-scale event collection and processing capability is a key component of modern application architectures including hello Internet of Things (IoT).</span></span>

<span data-ttu-id="f9503-108">Questa esercitazione viene illustrato come hello toouse [portale di Azure](https://portal.azure.com) toocreate un hub eventi.</span><span class="sxs-lookup"><span data-stu-id="f9503-108">This tutorial shows how toouse hello [Azure portal](https://portal.azure.com) toocreate an event hub.</span></span> <span data-ttu-id="f9503-109">Viene inoltre illustrato come hub eventi tooan eventi toosend utilizzando un'applicazione console scritta in c# tramite hello .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="f9503-109">It also shows how toosend events tooan event hub using a console application written in C# using hello .NET Framework.</span></span> <span data-ttu-id="f9503-110">gli eventi di tooreceive utilizzando hello .NET Framework, vedere hello [ricevere gli eventi utilizzando .NET Framework hello](event-hubs-dotnet-framework-getstarted-receive-eph.md) articolo oppure fare clic sulla lingua ricevente hello appropriata nella tabella a sinistra di hello del contenuto.</span><span class="sxs-lookup"><span data-stu-id="f9503-110">tooreceive events using hello .NET Framework, see hello [Receive events using hello .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) article, or click hello appropriate receiving language in hello left-hand table of contents.</span></span>

<span data-ttu-id="f9503-111">toocomplete questa esercitazione, è necessario hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="f9503-111">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="f9503-112">[Microsoft Visual Studio 2015 o versione successiva](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="f9503-112">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="f9503-113">le schermate di Hello in questa esercitazione usare Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="f9503-113">hello screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="f9503-114">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="f9503-114">An active Azure account.</span></span> <span data-ttu-id="f9503-115">Se non si ha un account, è possibile crearne uno gratuito in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="f9503-115">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="f9503-116">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="f9503-116">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="f9503-117">Creare uno spazio dei nomi di Hub eventi e un hub eventi</span><span class="sxs-lookup"><span data-stu-id="f9503-117">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="f9503-118">primo passaggio Hello è hello toouse [portale di Azure](https://portal.azure.com) toocreate spazio dei nomi di tipo hub eventi e ottenere hello le credenziali di gestione, l'applicazione deve toocommunicate con hub eventi hello.</span><span class="sxs-lookup"><span data-stu-id="f9503-118">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace of type Event Hubs, and obtain hello management credentials your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="f9503-119">toocreate uno spazio dei nomi e hub eventi, attenersi alla procedura hello in [questo articolo](event-hubs-create.md), quindi procedere con hello seguendo i passaggi in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f9503-119">toocreate a namespace and event hub, follow hello procedure in [this article](event-hubs-create.md), then proceed with hello following steps in this tutorial.</span></span>

## <a name="create-a-sender-console-application"></a><span data-ttu-id="f9503-120">Creare un'applicazione console per il mittente</span><span class="sxs-lookup"><span data-stu-id="f9503-120">Create a sender console application</span></span>

<span data-ttu-id="f9503-121">In questa sezione verrà scritto un'applicazione console di Windows che invia l'hub di eventi tooyour di eventi.</span><span class="sxs-lookup"><span data-stu-id="f9503-121">In this section, you'll write a Windows console app that sends events tooyour event hub.</span></span>

1. <span data-ttu-id="f9503-122">In Visual Studio, creare un nuovo progetto di App Desktop Visual c# utilizzando hello **applicazione Console** modello di progetto.</span><span class="sxs-lookup"><span data-stu-id="f9503-122">In Visual Studio, create a new Visual C# Desktop App project using hello **Console Application** project template.</span></span> <span data-ttu-id="f9503-123">Progetto hello nome **mittente**.</span><span class="sxs-lookup"><span data-stu-id="f9503-123">Name hello project **Sender**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp1.png)
2. <span data-ttu-id="f9503-124">In Esplora soluzioni fare doppio clic su hello **mittente** del progetto e quindi fare clic su **Gestisci pacchetti NuGet per la soluzione**.</span><span class="sxs-lookup"><span data-stu-id="f9503-124">In Solution Explorer, right-click hello **Sender** project, and then click **Manage NuGet Packages for Solution**.</span></span> 
3. <span data-ttu-id="f9503-125">Fare clic su hello **Sfoglia** tab, quindi cercare `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="f9503-125">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="f9503-126">Fare clic su **installare**e accettare le condizioni di hello d'uso.</span><span class="sxs-lookup"><span data-stu-id="f9503-126">Click **Install**, and accept hello terms of use.</span></span> 
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp2.png)
   
    <span data-ttu-id="f9503-127">Visual Studio Scarica, installa e aggiunge un riferimento toohello [pacchetto NuGet della libreria di Azure Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="f9503-127">Visual Studio downloads, installs, and adds a reference toohello [Azure Service Bus library NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span></span>
4. <span data-ttu-id="f9503-128">Aggiungere il seguente hello `using` le istruzioni nella parte superiore di hello di hello **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="f9503-128">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
  ```csharp
  using System.Threading;
  using Microsoft.ServiceBus.Messaging;
  ```
5. <span data-ttu-id="f9503-129">Aggiungere i seguenti campi toohello hello **programma** classe, sostituendo i valori segnaposto hello con nome hello dell'hub eventi hello creato nella sezione precedente hello e stringa di connessione dello spazio dei nomi a livello di hello è stato salvato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f9503-129">Add hello following fields toohello **Program** class, substituting hello placeholder values with hello name of hello event hub you created in hello previous section, and hello namespace-level connection string you saved previously.</span></span>
   
  ```csharp
  static string eventHubName = "{Event Hub name}";
  static string connectionString = "{send connection string}";
  ```
6. <span data-ttu-id="f9503-130">Aggiungere hello seguente metodo toohello **programma** classe:</span><span class="sxs-lookup"><span data-stu-id="f9503-130">Add hello following method toohello **Program** class:</span></span>
   
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
   
  <span data-ttu-id="f9503-131">Questo metodo invia in modo continuo hub di eventi eventi tooyour con un ritardo di 200 ms.</span><span class="sxs-lookup"><span data-stu-id="f9503-131">This method continuously sends events tooyour event hub with a 200-ms delay.</span></span>
7. <span data-ttu-id="f9503-132">Infine, aggiungere hello seguenti righe toohello **Main** metodo:</span><span class="sxs-lookup"><span data-stu-id="f9503-132">Finally, add hello following lines toohello **Main** method:</span></span>
   
  ```csharp
  Console.WriteLine("Press Ctrl-C toostop hello sender process");
  Console.WriteLine("Press Enter toostart now");
  Console.ReadLine();
  SendingRandomMessages();
  ```
8. <span data-ttu-id="f9503-133">Eseguire il programma hello e assicurarsi che non siano presenti errori.</span><span class="sxs-lookup"><span data-stu-id="f9503-133">Run hello program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="f9503-134">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="f9503-134">Congratulations!</span></span> <span data-ttu-id="f9503-135">Hub di eventi tooan messaggi inviati a questo punto.</span><span class="sxs-lookup"><span data-stu-id="f9503-135">You have now sent messages tooan event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9503-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f9503-136">Next steps</span></span>
<span data-ttu-id="f9503-137">Dopo aver creato un'applicazione funzionante che crea un hub eventi e invia i dati, è possibile passare toohello seguenti scenari:</span><span class="sxs-lookup"><span data-stu-id="f9503-137">Now that you've built a working application that creates an event hub and sends data, you can move on toohello following scenarios:</span></span>

* [<span data-ttu-id="f9503-138">Ricezione di eventi utilizzando hello Host processore di eventi</span><span class="sxs-lookup"><span data-stu-id="f9503-138">Receive events using hello Event Processor Host</span></span>](event-hubs-dotnet-framework-getstarted-receive-eph.md)
* <span data-ttu-id="f9503-139">[Event Processor Host reference](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost) (Informazioni di riferimento sull'host processore di eventi)</span><span class="sxs-lookup"><span data-stu-id="f9503-139">[Event Processor Host reference](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)</span></span>
* [<span data-ttu-id="f9503-140">Panoramica di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="f9503-140">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

